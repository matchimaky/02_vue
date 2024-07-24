<script setup lang="ts">
import EventCard from '@/components/EventCard.vue'
import Event from '@/types/Event'
import CategoryOrganizer from '@/components/CategoryOrganizer.vue'
import { ref, onMounted } from 'vue'
import EventService from '@/services/EventService'

const events = ref<Event[]>(null)

onMounted(() => {
  EventService.getEvents()
    .then((response) => {
      events.value = response.data
    })
    .catch((error) => {
      console.error('There was an error!', error)
    })
})
</script>

<template>
  <div class="events">
    <h1>Events For Good</h1>
    <!-- new element -->
    <EventCard v-for="event in events" key="event.id" :event="event" />
    <CategoryOrganizer v-for="event in events" key="event.id" :event="event" />
  </div>
</template>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
