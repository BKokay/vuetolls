<script setup lang="ts">
import { mapTripToken } from '@/uitls/constants'
import { ref, watch } from 'vue'

const props = defineProps({
  startCoordinate: Object,
  destinationCoordinate: Object
})

const route = ref(null)

watch(
  () => [props.startCoordinate, props.destinationCoordinate],
  async ([start, destination]) => {
    if (start && destination) {
        const headers = { headers: {
        'Content-Type': 'application/json',
        'Authorization': mapTripToken
    }}
    //obviously this would need to be hashed out to get the data I want 
      const routeResponse = await fetch('', headers)    
      route.value = await routeResponse.json()
    }
  }
)
</script>

<template> 
    <!-- would need to put map component here, then render the route -->
    <div v-if="route">
        <!-- render route here -->
    </div>
</template>
