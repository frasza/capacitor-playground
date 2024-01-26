<script setup lang="ts">
import { Geolocation } from '@capacitor/geolocation'
import { ActionSheet, ActionSheetButtonStyle } from '@capacitor/action-sheet'
import { FilePicker } from '@capawesome/capacitor-file-picker'

const loc = ref<{
  lat: null | number
  long: null | number
}>({
  lat: null,
  long: null,
})

const getCurrentPosition = async () => {
  const pos = await Geolocation.getCurrentPosition()
  loc.value = {
    lat: pos.coords.latitude,
    long: pos.coords.longitude,
  }
}

const showActions = async () => {
  await ActionSheet.showActions({
    title: 'Photo Options',
    message: 'Select an option to perform',
    options: [
      {
        title: 'Upload',
      },
      {
        title: 'Share',
      },
      {
        title: 'Remove',
        style: ActionSheetButtonStyle.Destructive,
      },
    ],
  })
}

const pickFiles = async () => {
  await FilePicker.pickFiles({
    types: ['image/png'],
    multiple: true,
  })
}
</script>

<template>
  <div>
    <h1>Geolocation</h1>
    <p>Your location is:</p>
    <p>Latitude: {{ loc.lat }}</p>
    <p>Longitude: {{ loc.long }}</p>

    <div class="flex gap-4 mt-6">
      <UButton @click="getCurrentPosition">Get Current Location</UButton>
      <UButton @click="showActions">Show actions</UButton>
      <UButton @click="pickFiles">Pick file</UButton>
    </div>
  </div>
</template>
