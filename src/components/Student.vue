<template>
  <div class="student-name"
       :class="{
        'young-student': props.age < 25
      }">
    {{ props.name }}
  </div>
  <div v-if="props.age < 26"
       class="student-age">
    {{ props.age }}
  </div>
</template>

<script setup lang="ts">
type Props = {
  name: string
  age: number
}
const props = defineProps<Props>()

</script>

<style scoped>
  .young-student {
    border: 1px solid green;
  }
</style>