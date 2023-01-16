<template>
    <div class="divers">
      <h1>This is an divers page</h1>
      <ToDo/>
    </div>
  </template>
  
<script>
  import ToDo from "../components/ToDo.vue";
  export default {
    name: 'DiversView',
    components: {
        ToDo
    }
  }
</script>