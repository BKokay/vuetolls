<script setup lang="ts">
import { ref, watch } from 'vue'

const props = defineProps({
  routeId: String
})

const tollInfo = ref(null)

watch(
  () => props.routeId,
  async (routeId) => {
    if (routeId) {
      const url = ''
      const routeMatchResponse = await fetch(url, {
        headers: {
          'Content-Type': 'application/json',
          Authorization: 'hereDataToken'
        }
      })
      const routeMatch = await routeMatchResponse.json()
      const trace = routeMatch.map()
      const hereTollResponse = await fetch(url, {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
          Authorization: 'hereDataToken'
        },
        body: trace
      })
      tollInfo.value = await hereTollResponse.json()
    }
  }
)
</script>

<template>
  <div v-if="tollInfo">
    <!-- display toll info -->
  </div>
</template>
