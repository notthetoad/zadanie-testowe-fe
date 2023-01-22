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
      let resp = await fetch(`http://localhost:5034/users/${this.num}`); // TODO change endpoint to correct one
      // console.log(await resp.json());
      const json = await resp.json();
      console.log(json)
      this.users = json.results;
    }
  }
}
</script>

<template>
  <form @submit.prevent>
    <input type="number" v-model="num">
    <button @click="getData">Click to fetch data.</button>
  </form>

  <div v-if="users.length > 0">
    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>Last Name</th>
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
