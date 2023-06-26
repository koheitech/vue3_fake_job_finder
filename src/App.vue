<template>
  <div class="app">
    <p>{{ name }} - {{ age }}</p>
    <button @click="changeName('FooBar')">Change name</button>
    <button @click="changeAge('35')">Change age</button>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, toRefs } from 'vue';

export default defineComponent({
  name: 'App',
  components: {},
  setup() {
    const state = reactive({
      name: 'Link',
      age: 25 as string | number
    })

    return { ...toRefs(state) }
  },
  methods: {
    changeName(name: string) {
      this.name = name
      return name
    },
    changeAge(age: string | number) {
      this.age = age
      return age
    }
  }
});
</script>

<style>

</style>
