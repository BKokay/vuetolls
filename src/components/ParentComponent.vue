<script setup lang="ts">
import { ref} from 'vue'
import type { Ref } from 'vue'
import CoordinateInputComponent from './CoordinateInputComponent.vue'
import MapComponent from './MapComponent.vue'
import TollInfoComponent from './TollInfoComponent.vue'

interface Coordinates {
  lat: number
  lng: number
}

interface RouteData {
  id: string
  // other route data fields
}

const validateCoordinates: Ref<{start: Coordinates, destination: Coordinates} | null> = ref(null)
const routeId: Ref<string | null> = ref(null)

const handleValidatedCoordinates = async ({ start, destination }: {start: Coordinates, destination: Coordinates}) => {
  validateCoordinates.value = { start, destination }

  const routeResponse = await fetch('', {})
  const routeData: RouteData = await routeResponse.json()

  routeId.value = routeData.id
}
</script>

<template>
  <div>
    <CoordinateInputComponent @coordinatesValidated="handleValidatedCoordinates" />
    <MapComponent
      v-if="validateCoordinates"
      :startCoordinate="validateCoordinates.start"
      :destinationCoordinate="validateCoordinates.destination"
    />
    <TollInfoComponent
      :routeId="routeId"
      :startCoordinate="validateCoordinates!.start"
      :destinationCoordinate="validateCoordinates!.destination"
      v-if="routeId"
    />
  </div>
</template>
