<template>
   <slot></slot>
   <BaseCard>
      <h4>{{ event.title }} ( {{ event.category }})</h4>
      <h5>{{ event.eventDate }}, {{ event.location }} </h5>
      <p>{{ event.description }}</p>
      <h5  v-if="extras.length">Extras: {{ extras }}</h5>
      <p>Pets: {{ !!event.pets ? '✔' : '✕'}}</p>
   </BaseCard>
</template>


<script>
export default {
   props: { event: { type: Object, required: true } },
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


</style>
