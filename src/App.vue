<template>
  <div id="app">
    <ListRepos :defaultUser="defaultUser" />
  </div>
</template>

<script>
import ListRepos from './components/ListRepos.vue'

export default {
  name: 'App',
  components: {
    ListRepos
  },
  data() {
    return {
      defaultUser: 'naveteam'
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  border: none;
  outline: none;
}

#app {
  font-family: Poppins, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #eee;
  background: #faeee7;
  width: 100%;
  min-height: 100vh;
  padding-top: 24px;
}

h1, h2, h3, h4, h5, h6 {
  color: #33272a;
}

a, p {
  color: #594a4e;
}

a:hover {
  color: #ff8ba7;
}

button {
  color: #33272a;
  font-size: 14px;
  font-weight: 600;
  background: #ff8ba7;
  height: 48px;
  min-width: 200px;
  padding: 0 24px;
  max-width: 400px;
  border-radius: 8px;
  margin: 12px auto;
  display: flex;
  justify-content: center;
  align-items: center;
}

button:hover {
  background: #FFB1C4;
  cursor: pointer;
}
</style>
