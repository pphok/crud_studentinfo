<template>
  <div id="app" class="app">
    <student-crud></student-crud>
  </div>
</template>

<script>
import StudentCrud from './components/StudentCrud.vue';

export default {
  name: 'App',
  components: {
    StudentCrud,
  },
};
</script>

<style>
.app {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  background-color: #f4f4f9;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}
</style>
