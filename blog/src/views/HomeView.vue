<template>
  <div class="home">

    <h1>Home</h1>

    <div>
      <h2>Refs</h2>
      <p>My name is {{ nameRef.name }}</p>
      <button @click="changeNameRef">Update name ref</button>
    </div>

    <div>
      <h2>Reactive</h2>
      <p>My name is {{ nameReactive.name }}</p>
      <button @click="changeNameReactive">Update name reactive</button>
    </div>

    <br>
  </div>
</template>

<script>
import { ref, reactive } from '@vue/reactivity'

export default {
  name: 'HomeView',
  setup() {
    let nameRef = ref({name: 'mario'})
    let nameReactive = reactive({name: 'mario'})

    const changeNameRef = () => {
      nameRef.value.name = 'Another One'
    }

    const changeNameReactive = () => {
      // Doesn't work with primitive values/ only referent
      nameReactive.name = 'Another One'
    }

    return { nameRef, nameReactive, changeNameRef, changeNameReactive }
  }
}
</script>
