<template>
  <div class="tralala">
    Hello students {{ count }}
    Hello computed {{ ageAndCountSum }}
    <button class="my-button"
            @click="incrementCount"></button>

    <student v-for="(student, index) in names"
         :key="index"
         :name="student.name"
         :age="student.age"
    />
  </div>
</template>

<script setup lang="ts">
import {computed, ref, watch, onMounted, onBeforeUnmount } from "vue";
import Student from "./components/Student.vue";

const count = ref(0)

type Student = {
  name: string
  age: number
}

const names = ref<Student[]>([
    {
      name: "Ivan",
      age: 25,
    },
    {
      name: "Peter",
      age: 26,
    },
    {
      name: "Gergana",
      age: 23,
    }
])

const ageAndCountSum = computed(() => {
  const ageSum = names.value.reduce((acc, { age }) => {
    return acc + age
  }, 0)
  return ageSum + count.value
})

watch(ageAndCountSum,
    (newValue, oldValue)=> {
      if(newValue > 55) {
        console.log('tralala', oldValue)
      }
    },
    {
      immediate: true,
      deep: true,
    }
)

onMounted(()=> {
  console.log('dispatch request to fetch data')
})

onBeforeUnmount(() => {
  console.log('component will unmount')
})

function incrementCount() {
  count.value = count.value + 1
  names.value = names.value.filter(({ name }) => name !== "Ivan")
}


</script>


<style scoped>
  .tralala {
    background: #a5a5f6;
    padding: 12px;
    color: white;
  }
</style>
