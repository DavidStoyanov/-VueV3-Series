<template>
  <div class="home">
    <br>
    <input v-model="search" type="text">
    <p>Searching for: {{ search }}</p>
    <b></b>
    <span v-for="name in matchingNames" :key="name">
      {{ name }}
    </span>
    <br>
  </div>
</template>

<script>
import { ref } from '@vue/reactivity'
import { computed, watch, watchEffect } from '@vue/runtime-core'

export default {
  name: 'HomeView',
  setup() {
    let search = ref('')
    let names = ref(['mario', 'ted', 'ped', 'led', 'smet'])

    watch(search, () => {
      console.log('watch function ran')
    }) 

    watchEffect(() => {
      console.log('watchEffect function ran', search.value)
    })

    const matchingNames = computed(() => {
      return names.value.filter(x => x.includes(search.value))
    })

    return { names, search, matchingNames }
  }
}
</script>

<style>
  span {
    display: inline-block;
    border: 1px solid #000;
    padding: 0.5rem 1rem;
    margin: 1rem 0.3rem;
  }
</style>