<template>
  <div id="app">
    <h1>Code assignment:</h1>
    <h2>Transfer component</h2>

    <TransferComponent />
  </div>
</template>

<script>
import TransferComponent from './components/TransferComponent.vue';

export default {
  name: 'App',

  components: {
    TransferComponent,
  },
};
</script>
