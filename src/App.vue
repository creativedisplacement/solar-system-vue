<template>
  <div class="app">
    <header>
      <div class="title">
        <img src="./assets/nasa-logo.png" alt="Nasa logo">
          <h1>Solar System</h1>
      </div>
      <div class="order">
        <button @click="handleClick('name')">order by name</button>
        <button @click="handleClick('ordinal')">order by distance from the sun</button>
        <button @click="handleClick('moons')">order by number of moons</button>
      </div>
    </header>
    
    
    <Planets :planets="planets" :order="order" />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, toRefs } from 'vue';
import Planet from './models/Planet'
import OrderTerm from './models/OrderTerm'
import Planets from './components/Planets.vue'
import PlanetData from './data/planets.json'

export default defineComponent({
  name: 'App',
  components: { Planets },
  setup() {

    const planets = PlanetData

    const order = ref<OrderTerm>('ordinal')

    const handleClick = (term: OrderTerm) => {
        order.value = term
    }

    return { planets, handleClick, order }
  }
});
</script>

<style>
header {
    text-align: center;
  }
  header .order {
    margin-top: 20px;
  }
  button {
    margin: 0 10px;
    color: #1195c9;
    border: 3px solid #1195c9;
    background: #d5f0ff;
    padding: 8px 16px;
    border-radius: 4px;
    cursor: pointer;
    font-weight: bold;
  }
  header .title{
    display: flex;
    justify-content: center;
  }
  header img {
    width: 250px;
  }

  header h1 {
    font-size: 3em;
  }
</style>
