<template>
  <q-page class="row items-center justify-evenly">
    <my-component title="My component"></my-component>
  </q-page>
</template>

<script lang="ts">
import MyComponent from '../components/MyComponent.vue';
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'IndexPage',
  components: { MyComponent },
});
</script>
