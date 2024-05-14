<script setup lang="ts">
import {ref} from 'vue'
import {mapTripToken} from '../uitls/constants.js'

const startCoordinate = ref('')
const destinationCoordinate = ref('')

const validateCoordinates = async() => {
    const url = ''
    const headers = { headers: {
        'Content-Type': 'application/json',
        'Authorization': mapTripToken
    }}
    const validatedStart = await fetch(url, headers)
    const startData = await validatedStart.json()
    //whatever you normally do with fetch here. 
    const validStart = startData.coordinates
    //repeat with destination
    const validatedDestination = await fetch(url, headers)
    const destinationData = await validatedDestination.json()
    //whatever you normally do with fetch here. 
    const validDestination = destinationData.coordinates


    const emit = defineEmits()
    emit('coordinatesValidated', {start: validStart, destination: validDestination})
}
</script>

<template>
    <div>
        <input type="text" v-model="startCoordinate" placeholder="start">
        <input type="text" v-model="destinationCoordinate" placeholder="destination">
        <button @click="validateCoordinates">click me!</button>
    </div>
</template>