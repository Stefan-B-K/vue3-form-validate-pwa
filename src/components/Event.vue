<template>
   <slot></slot>
   <BaseCard style="position: relative">
      <h4>{{ event.title }} ( {{ event.category }})</h4>
      <h5>{{ event.eventDate }}, {{ event.location }} </h5>
      <p>{{ event.description }}</p>
      <h5  v-if="extras.length">Extras: {{ extras }}</h5>
      <p>Pets: {{ !!event.pets ? '✓' : '✕'}}</p>
      <button @click="$emit('delete-event')" class="x-close">Delete</button>
   </BaseCard>
</template>


<script>
export default {
   props: { event: { type: Object, required: true } },
   emits: ['delete-event'],
   computed: {
      extras () {
         const extras = []
         if (this.event.catering) extras.push('Catering')
         if (this.event.music) extras.push('Live Music')
         if (this.event.garden) extras.push('Garden')
         if (this.event.pool) extras.push('Pool')
         return extras.join(', ')
      }
   }
}
</script>


<style scoped>
h4, h5, p {
   margin: 0;
}
.x-close {
   position: absolute;
   bottom: 15px;
   right: 0;
   padding: 5px;
   border: none;
   border-radius: 4px;
   background: transparent;
   color: white;
   font-weight: bolder;
   cursor: pointer;
  font-size: small;
   transition: all 0.2s ease-out;
}

.x-close:hover {
   box-shadow: 0 5px 8px 0 rgba(0, 0, 0, 0.2), 0 4px 10px 0 rgba(0, 0, 0, 0.19);
}

.x-close:active {
   box-shadow: none;
}

.x-close:focus {
   outline: 0;
}
</style>
