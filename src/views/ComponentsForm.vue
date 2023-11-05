<script setup>
import { useField, useForm } from 'vee-validate'
import { object, string, number, boolean, date } from 'yup'
import { reactive, ref } from 'vue'
import { UniqueID } from '../features/UniqueID.js'
import Event from '@/components/Event.vue'

window.addEventListener('offline', () => {})

const showEvents = ref(false)
let database = null
const savedEvents = reactive([])

const categories = reactive([
   'sustainability',
   'nature',
   'animal welfare',
   'housing',
   'education',
   'food',
   'community'
])

const petOptions = reactive([
   { value: 1, label: 'Yes', uuid: UniqueID() },
   { value: 0, label: 'No', uuid: UniqueID() }
])

const today = (new Date()).toISOString().split('T')[0]

const validationSchema = object({
   category: string().nullable().required('Required field'),
   title: string().required('A cool title is required (min 3 letters)').min(3),
   eventDate: date().required('Required field').min(today, 'Future date please!!!'),
   description: string(),
   location: string().required('Required field'),
   pets: number(),
   catering: boolean(),
   music: boolean(),
   garden: boolean(),
   pool: boolean()
})

const { handleSubmit, errors } = useForm({
   validationSchema,
   initialValues: {
      category: null,
      pets: 0,
      catering: false,
      music: false,
      garden: false,
      pool: false
   }
})

const { value: category } = useField('category')
const { value: title } = useField('title')
const { value: eventDate } = useField('eventDate')
const { value: description } = useField('description')
const { value: location } = useField('location')
const { value: pets } = useField('pets')
const { value: catering } = useField('catering')
const { value: music } = useField('music')
const { value: garden } = useField('garden')
const { value: pool } = useField('pool')

const getDatabase = async () => {
   return new Promise((resolve, reject) => {
      if (database) resolve(database)

      let request = window.indexedDB.open('eventsDB', 1)

      request.onerror = event => {
         console.error('ERROR: Unable to open database', event)
         reject('Error')
      }

      request.onsuccess = event => {
         database = event.target.result
         resolve(database)
      }

      request.onupgradeneeded = event => {
         let database = event.target.result
         database.createObjectStore('events', {
            autoIncrement: true,
            keyPath: 'id'
         })
      }
   })
}

const getEventStore = async () => {
   database = await getDatabase()

   return new Promise((resolve, reject) => {
      const transaction = database.transaction('events', 'readonly')
      const store = transaction.objectStore('events')

      let eventList = []

      store.openCursor().onsuccess = event => {
         const cursor = event.target.result
         if (cursor) {
            eventList.push(cursor.value)
            cursor.continue()
         }
      }
      transaction.oncomplete = () => resolve(eventList)
      transaction.onerror = event => reject(event)
   })
}

const saveEvent = async (anEvent) => {
   database = await getDatabase()

   return new Promise((resolve, reject) => {
      const transaction = database.transaction('events', 'readwrite')
      const store = transaction.objectStore('events')

      store.put(anEvent)
      transaction.oncomplete = () => resolve('Event successfully saved.')
      transaction.onerror = event => reject(event)
   })
}

const deleteEvent = async(eventID) => {
   database = await getDatabase()

   return new Promise((resolve, reject) => {
      const transaction = database.transaction('events', 'readwrite')
      const store = transaction.objectStore('events')

      store.delete(eventID)
      transaction.oncomplete = () => {
         const eventIndex = savedEvents.findIndex(event => event.id === eventID)
         savedEvents.splice(eventIndex, 1)
         resolve('Event successfully deleted.')
      }
      transaction.onerror = event => reject(event)
   })
}

const submit = handleSubmit(values => {
   saveEvent(values)
   window.location.reload()
})

getEventStore().then((res, _) => savedEvents.push(...res))

</script>


<template>
   <div>

      <BaseDialog :show="showEvents" @close="showEvents=false" title="My Events">
         <div v-for="event in savedEvents" :key="event.id">
            <Event :event="event" @delete-event="deleteEvent(event.id)"/>
         </div>
      </BaseDialog>

      <div style="display: flex; justify-content: center; align-items: center">
         <h1>Add Event</h1>
         <BaseButton
            @click="showEvents=true"
            type="button"
            class="-fill-gradient">Events
         </BaseButton>
      </div>
      <form @submit.prevent="submit">

         <fieldset>
            <legend>Event info</legend>
            <BaseSelect
               label="Select a category"
               :options="categories"
               v-model="category"
               :uuid="UniqueID()"
               :error="errors.category"
            />

            <BaseInput
               label="Title"
               type="text"
               v-model="title"
               :uuid="UniqueID()"
               :error="errors.title"
            />

            <BaseInput
               label="Date"
               type="date"
               v-model="eventDate"
               :uuid="UniqueID()"
               :error="errors.eventDate"
            />

            <BaseInput
               label="Description"
               type="text"
               v-model="description"
               :uuid="UniqueID()"
               :error="errors.description"
            />
         </fieldset>

         <fieldset>
            <legend>Where is it at?</legend>
            <BaseInput
               label="Location"
               type="text"
               v-model="location"
               :uuid="UniqueID()"
               :error="errors.location"
            />
         </fieldset>

         <fieldset>
            <legend>Are pets allowed?</legend>
            <BaseRadioGroup
               name="pets"
               :options="petOptions"
               v-model="pets"
               :error="errors.pets"
            />
         </fieldset>

         <fieldset>
            <legend>Extras</legend>
            <div id="extras">
               <div>
                  <BaseCheckbox
                     label="Catering"
                     v-model="catering"
                     :uuid="UniqueID()"
                     :error="errors.catering"
                  />
               </div>

               <div>
                  <BaseCheckbox
                     label="Live music"
                     v-model="music"
                     :uuid="UniqueID()"
                     :error="errors.music"
                  />
               </div>

               <div>
                  <BaseCheckbox
                     label="Garden"
                     v-model="garden"
                     :uuid="UniqueID()"
                     :error="errors.garden"
                  />
               </div>

               <div>
                  <BaseCheckbox
                     label="Pool"
                     v-model="pool"
                     :uuid="UniqueID()"
                     :error="errors.pool"
                  />
               </div>
            </div>
         </fieldset>

         <div>
            <BaseButton
               type="submit"
               class="-fill-gradient"
            >
               Submit
            </BaseButton>
         </div>
      </form>
   </div>
</template>

<style scoped>
fieldset {
   border: 0;
   margin-top: 10px;
   padding: 0;
}

legend {
   font-size: 22px;
   font-weight: 700;
   margin: 0;
}

#extras {
   display: flex;
   /*align-items: center;*/
}

@media only screen and (max-width: 450px) {
   #extras {
      display: flex;
      flex-direction: column;
   }
}

</style>
