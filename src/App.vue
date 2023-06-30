<template>
  <div class="app">
    <header>
      <dv class="title">
        <img src="./assets/job.svg" alt="site logo">
        <h1>Job Finder</h1>
      </dv>
      <div class="order">
        <button @click="handleClick('title')">Order by Title</button>
        <button @click="handleClick('salary')">Order by Salary</button>
        <button @click="handleClick('location')">Order by Location</button>
        <button class="toggleButton" @click="toggleOrder">Reverse Order</button>
      </div>
    </header>
    <JobList :jobs="jobs" :order="order" :order-direction="orderDirection"/>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import JobList from './components/JobsList.vue'
import Job from  './types/Job'
import OrderTerm from  './types/OrderTerm'
import Order from './types/Order';

export default defineComponent({
  name: 'App',
  components: { JobList },
  setup() {
    const jobs = ref<Job[]>([
      { title: 'farm worker', location: 'lon lon ranch', salary: 30000, id: '1' },
      { title: 'quarryman', location: 'death mountain', salary: 40000, id: '2' },
      { title: 'flute player', location: 'the lost woods', salary: 35000, id: '3' },
      { title: 'fisherman', location: 'lake hylia', salary: 21000, id: '4' },
      { title: 'prison guard', location: 'gerudo valley', salary: 32000, id: '5' }
    ])

    const order = ref<OrderTerm>('title')
    const orderDirection = ref<Order>('ASC')

    const handleClick = (term: OrderTerm) => {
      order.value = term
    }

    const toggleOrder = () => {
      orderDirection.value = (orderDirection.value === 'ASC') ? 'DECS' : 'ASC'
    }

    return { jobs, handleClick, toggleOrder, order, orderDirection }
  },
  methods: {
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
    color: #008680;
    border: 3px solid #008680;
    background: white;
    padding: 8px 16px;
    border-radius: 4px;
    cursor: pointer;
    font-weight: bold;
  }
  .toggleButton {
    color: black;
    border: 3px solid black;
  }
  header .title{
    color: #008680;
    display: flex;
    justify-content: center;
  }
  header img {
    width: 60px;
    margin-right: 20px;
  }
  header h1 {
    font-size: 3em;
  }
</style>