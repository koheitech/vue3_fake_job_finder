<template>
  <div class="job-list">
    <p><b>Order by {{ order }}</b></p>
    <transition-group name="list" tag="ul">
      <li v-for="job in orderedJobs" :key="job.id">
        <h2>{{ job.title }} in {{ job.location }}</h2>
        <div class="salary">
          <img src="../assets/yen.svg" alt="yen icon">
          <p>{{ job.salary }} yens</p>
        </div>
        <div class="description">
          <p>
            Lorem ipsum dolor sit amet consectetur adipisicing elit. 
            Quis eligendi dolore minima. Minima pariatur sequi tenetur 
            dolor velit voluptate doloremque, nesciunt architecto, 
            voluptatem quisquam qui accusantium aliquam quis. Molestias, possimus?
          </p>
        </div>
      </li>
    </transition-group>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent, PropType } from "vue";
import Job from "@/types/Job";
import OrderTerm from "@/types/OrderTerm";
import Order from "@/types/Order";

export default defineComponent({
  props: {
    jobs: {
      required: true,
      type: Array as PropType<Job[]>,
    },
    order: {
      required: true,
      type: String as PropType<OrderTerm>,
    },
    orderDirection: {
      required: true,
      type: String as PropType<Order>,
    }
  },
  setup(props) {
    const orderedJobs = computed(() => {
      return [...props.jobs].sort((a: Job, b: Job) => {
        if(props.orderDirection === 'ASC')
          return a[props.order] > b[props.order] ? 1 : -1
        else
        return a[props.order] > b[props.order] ? -1 : 1
      })
    })

    return { orderedJobs }
  }
});
</script>

<style scoped>
  .job-list {
    max-width: 960px;
    margin: 40px auto;
  }
  .job-list ul {
    padding: 0;
  }
  .job-list li {
    list-style-type: none;
    background: white;
    padding: 16px;
    margin: 16px 0;
    border-radius: 4px;
  }
  .job-list h2 {
    margin: 0 0 10px;
    text-transform: capitalize;
  }
  .salary {
    display: flex;
  }
  .salary img {
    width: 30px;
  }
  .salary p {
    color: #008680;
    font-weight: bold;
    margin: 10px 10px;
  }
  .list-move {
    transition: all 1s
  }
</style>