<template>
  <div class="min-h-screen bg-gray-100 py-8">
    <NuxtRouteAnnouncer />
    <div class="max-w-2xl mx-auto px-4">
      <div class="bg-white rounded-lg shadow-lg p-8">
        <h1 class="text-3xl font-bold text-center text-gray-800 mb-8">
          F-Zero: Maximum Velocity<br>
          Vermilion Code Generator
        </h1>
        
        <div class="space-y-6">
          <div>
            <UFormGroup label="Player Name" description="Enter alphabetic characters only">
              <UInput
                v-model="playerName"
                placeholder="Enter player name..."
                :maxlength="20"
                @input="handleInput"
                size="lg"
              />
            </UFormGroup>
          </div>
          
          <div v-if="vermilionCode" class="bg-blue-50 border border-blue-200 rounded-lg p-6">
            <h3 class="text-lg font-semibold text-blue-800 mb-2">Generated Vermilion Code:</h3>
            <div class="font-mono text-2xl text-blue-900 bg-white rounded p-4 border">
              {{ vermilionCode }}
            </div>
          </div>
          
          <div v-if="playerName && !vermilionCode" class="text-gray-500 text-center">
            Enter a valid player name to generate Vermilion Code
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { generate } from 'jet-vermillion-generator'

const playerName = ref('')

const handleInput = (event) => {
  // Only allow alphabetic characters
  const value = event.target.value.replace(/[^A-Za-z]/g, '')
  playerName.value = value
}

// Compute Vermilion Code reactively
const vermilionCode = computed(() => {
  if (playerName.value && playerName.value.length > 0) {
    return generate(playerName.value.toUpperCase())
  }
  return ''
})
</script>
