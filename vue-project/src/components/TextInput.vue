<script lang="ts" setup>
defineProps<{
  modelValue?: string | null
}>()

const model = defineModel<string | null>()
</script>

<template>
  <input
    v-model="model"
  />
</template>
