<template>
  <div>
    <table class="table table-bordered table-hover table-responsive-xl">
      <th>
        <th>Title</th>
        <th>Description</th>
        <th>Author</th>
        <th>Score</th>
      </th>
      <tr v-for="quizz in quizzs" :key="quizz.id">
        <td>{{ quizz.title }}</td>
        <td>{{ quizz.description }}</td>
        <td>{{ quizz.author }}</td>
        <td>{{ quizz.score }}</td>
      </tr>
    </table>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'dashboard',
  data() {
    return {
      quizzs: [],
    }
  },
  mounted() {
    axios.get('http://localhost:8080/api/quizz/').then((response) => {
      this.quizzs = response.data
    })
  },
}
</script>
