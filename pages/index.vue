<template>
  <div class="min-h-screen bg-gray-100 py-8">
    <div class="max-w-2xl mx-auto px-4">
      <div class="bg-white rounded-lg shadow-lg p-8">
        <h1 class="text-3xl font-bold text-center text-gray-800 mb-8">
          F-ZERO: Maximum Velocity<br>
          Vermilion Code Generator
        </h1>

        <div class="space-y-6">
          <ClientOnly>
            <div>
              <UFormField label="Player Name" help="Enter alphanumeric characters and some symbols only" size="xl">
                <UInput
                    :value="playerName"
                    placeholder="Enter player name..."
                    :maxlength="8"
                    @input="handleInput"
                />
              </UFormField>
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

            <template #fallback>
              <div class="text-center text-gray-500">
                Loading form...
              </div>
            </template>
          </ClientOnly>
        </div>
      </div>
    </div>
    <footer class="text-center text-gray-400 mt-8">
      &copy; 2025 <a href="https://github.com/cyrus07424" target="_blank">cyrus</a>
    </footer>
  </div>
</template>

<script setup>
import {generate} from 'jet-vermillion-generator'
import {computed, ref} from 'vue'

const playerName = ref('')

const handleInput = (event) => {
  playerName.value = event.target.value.toUpperCase().replace(/[^ !&',-.\/0-9?A-Z_]/g, '');
}

const vermilionCode = computed(() => {
  if (0 < playerName.value.length) {
    try {
      return generate(playerName.value)
    } catch (e) {
      return ''
    }
  }
  return ''
})

// Setup page meta
useHead({
  title: 'F-ZERO: Maximum Velocity Vermilion Code Generator'
})
</script>