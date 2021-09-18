<template>
  <div class="home">
    <h2>Home</h2>
    <Events />
  </div>
</template>

<script>
import Events from '@/components/Events.vue';

export default {
  name: 'Home',
  components: {
    Events
  }
}
</script>
