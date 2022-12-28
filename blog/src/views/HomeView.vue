<template>
  <div class="home">
    <p ref="p">My name is {{ name }} and my age is {{ age }}</p>
    <button @click="handleClick">click me!</button>
    <button @click="name = 'Another One'">change name</button>
    <button @click="age = 123">try change age</button>
    <br>
    <button @click="addAge(22)">Age Up</button>
    <br>
      <label>
        <span>Name:</span>
        <input v-model="name" type="text" />
      </label>
    <br>
  </div>
</template>

<script>
import { ref } from '@vue/reactivity'

export default {
  name: 'HomeView',
  setup() {
    let name = ref('mario')
    let age = ref(30)
    //let age = 30

    const p = ref()

    const handleClick = () => {
      console.log(p, p.value)
    }

    const changeName = () => {
      name.value = 'Another One'
    }

    const addAge = (value) => {
      age.value + value;
    }

    return { name, age, handleClick, addAge, p }
  }
}
</script>
