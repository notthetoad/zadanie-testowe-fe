<script>
export default {
  data() {
    return {
      numberOfUsers: 1,
      randomUsers: []
    }
  },
  methods: {
    async getRandomUsersData() {
      let resp = await fetch(`http://localhost:5034/users/${this.numberOfUsers}`);
      const jsonResponse = await resp.json();
      this.randomUsers = jsonResponse.results ?? [];
    }
  }
}
</script>

<template>
  <form @submit.prevent>
    <input type="number" v-model="numberOfUsers" min="1">
    <button @click="getRandomUsersData">Pobierz</button>
  </form>

  <div v-if="randomUsers.length > 0">
    <table>
      <thead>
        <tr>
          <th>Imię</th>
          <th>Nazwisko</th>
          <th>Email</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in randomUsers" v-bind:key="user.email">
          <td>{{ user.name.first }}</td>
          <td>{{ user.name.last }}</td>
          <td>{{ user.email }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style scoped>
  form {
    display: flex;
    flex-direction: column;
    margin-bottom: 8px;
  }

  form > * {
    width: 100%;
    margin: 4px;
    padding: 6px 0px;
  }
</style>
