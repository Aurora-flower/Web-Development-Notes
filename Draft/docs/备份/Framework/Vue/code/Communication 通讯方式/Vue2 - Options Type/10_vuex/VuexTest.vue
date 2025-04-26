<template>
  <div class="box">
    <Child1/>
    <br>
    <Child2/>
  </div>
</template>

<script>
import Child1 from './Child_One.vue';
import Child2 from './Child_Two.vue';

export default {
  name: 'VuexTest',
  components: {
    Child1,
    Child2,
  }
}
</script>

<style scoped>
</style>
