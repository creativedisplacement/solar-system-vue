<template>
    <div class="planet-list">
        <p>Ordered by: {{ order }} </p>
        <transition-group name="list" tag="ul">
            <li v-for="planet in orderedPlanets" :key="planet.id">
                <h2>{{ planet.name }} </h2>
                <div class="introduction">
                    <img :src="planet.imageUrl" :alt="planet.name" /> 
                    <p>{{ planet.introduction }}</p>
                </div>
            </li>
        </transition-group>
    </div>
</template>

<script lang="ts">
import { computed, defineComponent, PropType } from 'vue'
import Planet from '@/models/Planet'
import OrderTerm from '@/models/OrderTerm'

export default defineComponent({
    props: {
        planets:{
            required: true,
            type: Array as PropType<Planet[]>
        },
        order: {
            required: true,
            type: String as PropType<OrderTerm>
        }
    },
    setup(props) {
        const orderedPlanets  = computed(() => {
            return [...props.planets].sort((a: Planet, b: Planet) => {
                return a[props.order] > b[props.order] ? 1 : -1
            })
        })

        return { orderedPlanets }
    }
})
</script>

<style scoped>
.planet-list {
    max-width: 960px;
    margin: 40px auto;
  }
  .planet-list ul {
    padding: 0
  }
  .planet-list li {
    list-style-type: none;
    padding: 16px;
    margin: 16px 0;
    border-radius: 4px;
    border:solid 1px #ffffff;
  }
  .planet-list h2 {
    margin: 0 0 10px;
    text-transform: capitalize;
  }
  .introduction {
    display: flex;
  }
  .introduction img {
    width: 30px;
    height: 35px;
    margin-right:10px;
  }
  .introduction p {
    color: #17bf66;
    font-weight: bold;
    margin: 10px 4px;
  }
  .list-move {
    transition: all 1s;
  }
</style>