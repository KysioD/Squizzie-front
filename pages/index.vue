<template>
  <div>
    <h1>Login</h1>
    <form @submit.prevent="login">
      <input type="text" v-model="username" placeholder="Username"/>
      <button type="submit">Login</button>
    </form>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'IndexPage',
  data() {
    return {
      username: '',
    }
  },
  methods: {
    login() {
      axios.get(`http://localhost:8080/api/account/${this.username}`).then(() => {
          console.log('Account exist')
          this.$router.push({name: 'dashboard'})
        }
      )
        .catch((error) => {
          if (error.response.status === 404) {
            console.log('create account')
            axios.post('http://localhost:8080/api/account/', {
              username: this.username,
            }).then(() => {
              // Open quizz dashboards
              this.$router.push({name: 'dashboard'})
            })
          } else {
            console.log(error)
          }
        })
    },
  },
}
</script>
