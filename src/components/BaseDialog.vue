<template>
   <teleport to="body">
      <transition name="backdrop">
         <div v-if="show" @click="tryClose" class="backdrop"></div>
      </transition>
      <transition name="dialog">
         <dialog open v-if="show">
            <header style="display: flex; align-items: center; justify-content: space-around ">
                  <h2>{{ title }}</h2>
                  <BaseButton @click="tryClose" class="-fill-gradient-reverse">Close</BaseButton>
            </header>
            <section>
               <slot></slot>
            </section>
         </dialog>
      </transition>
   </teleport>
</template>

<script>
export default {
   props: {
      show: {
         type: Boolean,
         required: true
      },
      title: {
         type: String,
         required: false
      }
   },
   emits: ['close'],
   methods: {
      tryClose () {
         if (this.fixed) {
            return
         }
         this.$emit('close')
      }
   }
}
</script>

<style scoped>
.backdrop {
   position: fixed;
   top: 0;
   left: 0;
   height: 100vh;
   width: 100%;
   background-color: rgba(0, 0, 0, 0.75);
   z-index: 10;
}

dialog {
   position: fixed;
   top: 10vh;
   left: 10%;
   width: 80%;
   height: 85%;
   z-index: 100;
   border-radius: 12px;
   border: none;
   box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
   padding: 0;
   margin: 0;
   overflow: hidden;
   background-color: white;
}

section {
   height: 75%;
   overflow-y: scroll;
}

header {
   background: linear-gradient(to right, #16c0b0, #84cf6a);
   color: white;
   width: 100%;
   padding: 1rem;
}

header h2 {
   margin: 0;
}

section {
   padding: 1rem;
}

menu {
   padding: 1rem;
   display: flex;
   justify-content: flex-end;
   margin: 0;
}

.backdrop-enter-from,
.backdrop-leave-to {
   background-color: rgba(0, 0, 0, 0);
}

.backdrop-enter-to,
.backdrop-leave-from {
   background-color: rgba(0, 0, 0, 0.7);
}

.backdrop-enter-active {
   transition: all 0.4s ease-out;
}

.backdrop-leave-active {
   transition: all 0.4s ease-in;
}

.dialog-enter-from,
.dialog-leave-to {
   transform: scale(0.7);
   opacity: 0;
}

.dialog-enter-to,
.dialog-leave-from {
   transform: scale(1);
   opacity: 1;
}

.dialog-enter-active {
   transition: all 0.4s ease-out;
}

.dialog-leave-active {
   transition: all 0.4s ease-in;
}

@media (min-width: 768px) {
   dialog {
      left: calc(50% - 20rem);
      width: 40rem;
   }
}
</style>