<script setup>

const dialog = ref(false)
const currentModel = useCurrentModel()
const availableModels = [
    'gpt-3.5-turbo',
    'gpt-4',
    'gpt-3.5-turbo(API)'
]
const currentModelDefault = ref(MODELS[currentModel.value.name])

onNuxtReady(() => {
  currentModel.value = getCurrentModel()
  watch(currentModel, (newVal, oldVal) => {
    currentModelDefault.value = MODELS[newVal.name]
    saveCurrentModel(newVal)
  }, { deep: true })
})

</script>

<template>
  <v-dialog
      v-model="dialog"
      persistent
  >
    <template v-slot:activator="{ props }">
      <v-list-item
          v-bind="props"
          rounded="xl"
          prepend-icon="tune"
          :title="$t('modelParameters')"
      ></v-list-item>
    </template>
    <v-card>
      <v-toolbar
          density="compact"
      >
        <v-toolbar-title>{{ $t('modelParameters') }}</v-toolbar-title>

        <v-spacer></v-spacer>

        <v-btn icon="close" @click="dialog = false"></v-btn>
      </v-toolbar>
      <v-card-text>
        <v-select
            v-model="currentModel.name"
            :label="$t('model')"
            :items="availableModels"
            variant="underlined"
        ></v-select>

      </v-card-text>
    </v-card>
  </v-dialog>
</template>

<style scoped>

</style>