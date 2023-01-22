<script>
export default {
  data() {
    return {
      num: 1,
      users: []
    }
  },
  methods: {
    async getData() {
      let resp = await fetch(`http://localhost:5034/users/${this.num}`);
      const json = await resp.json();
      console.log(json)
      this.users = json.results ?? [];
    }
  }
}
</script>

<template>
  <form @submit.prevent>
    <input type="number" v-model="num">
    <button @click="getData">Pobierz</button>
  </form>

  <div v-if="users.length > 0">
    <table>
      <thead>
        <tr>
          <th>Imię</th>
          <th>Nazwisko</th>
          <th>Email</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in users" v-bind:key="user.email">
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
