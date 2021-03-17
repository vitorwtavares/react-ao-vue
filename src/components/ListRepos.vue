<template>
  <div class="flex column">
    <h1 class="title">💻 {{ user || '_' }}'s repositories 📚</h1>
      <div class="flex search-container">
        <p>🔍 search by github username</p>
        <input class="search" v-model="user"/>
        <!-- ... -->
        <button @click="getRepos">
          fetch {{ user || '_' }}'s repositories
        </button>
      </div>
      <p v-if="lastUserFetched !== user" class="instructions">
        type in an username and click the button to fetch that user's repositories
      </p>
      <p v-else-if="loading ">
        loading...
      </p>
      <a 
        v-else 
        v-for="(repo, index) in repos" 
        :key="index" 
        :href="repo.html_url" 
        target="_blank"
      >
          {{ repo.name }}
      </a>
  </div>
</template>

<script>
  export default {
    name: 'ListRepos',
    props: {
      defaultUser: {
        type: String,
        required: true,
        default: 'naveteam'
      }
    },
    data() {
      return {
        user: '',
        api_url: 'https://api.github.com',
        repos: [],
        loading: false,
        lastUserFetched: ''
      }
    },
    methods: {
      async getRepos() {
        try{
          this.loading = true
          this.lastUserFetched = this.user
          const response = await fetch(`${this.api_url}/users/${this.user}/repos`)
          const data = await response.json()
          this.repos = data
        } catch(err) {
          console.log(err)
        } finally {
          this.lastUserFetched = this.user
          this.loading = false
        }
      }
    },
    created() {
      this.user = this.defaultUser
      this.lastUserFetched = this.defaultUser
      this.getRepos()
    }
  }
</script>

<style scoped>
  .title {
    margin: 0 auto 24px;
  }
  
  .flex {
    display: flex;    
  }

  .column {
    flex-direction: column;
  }

  a {
    max-width: 200px;
    margin: 0 auto;
    font-size: 14px;
  }

  .search-container {
    margin: 0 auto;
    align-items: center;
  }

  .search {
    margin: 0 12px;
    padding: 12px;
    font-size: 14px;
    border-radius: 8px;
    height: 48px;
    min-width: 300px;
  }

  .instructions {
    margin-top: 48px;
  }
</style>
