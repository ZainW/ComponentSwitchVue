<script setup lang="ts">
interface Props {
  value: number
}
defineProps<Props>()
const emit = defineEmits<{
  submit: [id: number]
}>()
</script>
<template>
  <div>
    <h1>Comp1</h1>
    <button @click="emit('submit', value)">{{ value }}</button>
  </div>
</template>
