<template>
  <div class="app">
    <router-view v-if="isLoaded">
    </router-view>
    <page-spinner v-else />
  </div>
</template>

<script>
import io from 'socket.io-client';
import PageSpinner from '@/components/PageSpinner';

export default {
  name: 'App',

  components: {
    PageSpinner,
  },

  provide() {
    return {
      socket: this.socket,
    };
  },

  data() {
    return {
      isLoaded: false,
      socket: io(process.env.VUE_APP_SOCKETIO_SERVER),
    };
  },

  async beforeCreate() {
    await this.$store.dispatch('loadUsers');
    await this.$store.dispatch('loadPuzzles');

    // Check if user is already set, then skip login screen
    const userId = JSON.parse(localStorage.getItem('userId'));

    if (userId) {
      this.$store.commit('setUserId', userId);
      if (this.$route.name !== 'Game') {
        this.$router.push({ name: 'Game' });
      }
    }

    this.isLoaded = true;
  },

  created() {
    // console.log(this.socket);
    if (this.socket) {
      this.socket.on('message', (data) => {
        console.log('got a message', data);
      })
    }
  },
}
</script>

<style>
@import "./styles/base.css";
</style>

<style scoped>
.app {
  max-width: 1024px;
  margin: 0 auto;
}
</style>
