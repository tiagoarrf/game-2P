<template>
  <div>
    <button>START</button>
  </div>
</template>

<script>
import 'vue-router'

export default {
  computed: {
    username() {
      // We will see what `params` is shortly
      return this.$route.params.username
    },
  },
  methods: {
    goToDashboard() {
      if (isAuthenticated) {
        this.$router.push('/dashboard')
      } else {
        this.$router.push('/login')
      }
    },
  },
}
</script>

<style scoped>
button {
  background-color: hsla(160, 75%, 48%, 0.521);
  transition: color 0.5s, background-color 3.5s;
  animation: buttom 2s alternate infinite;
  height: 5rem;
  width: 10rem;
  border-bottom-style: double;
  border-color: rgba(13, 211, 145, 0.308);
  border-radius: 10px;
  font-size: 2rem;
}

button:hover {
  background-color: hsla(160, 100%, 37%, 1);
  transition: color 0.5s, background-color 3.5s;
  color: #fff;
  cursor: pointer;
}

@keyframes buttom {
  0% {
    background-color: rgb(22, 114, 83);
    transition: color 0.5s, background-color 3.5s;
  }
  50% {
    background-color: rgba(14, 230, 158, 0.726);
    transition: color 0.5s, background-color 3.5s;
  }
  100% {
  }
}
</style>
