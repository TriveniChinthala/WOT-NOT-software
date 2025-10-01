<template>
  <div id="app">
    <router-view />
  </div>
</template>

<script>
export default {
  name: 'App',
};
</script>
<template>
  <div id="app">
    <MessageGenerator />
  </div>
</template>

<script>
import MessageGenerator from './components/MessageGenerator.vue'

export default {
  components: {
    MessageGenerator
  }
}
</script>

<style>
.Toastify__toast-container {
  z-index: 99999 !important;
}
</style>