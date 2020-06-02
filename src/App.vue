<template>
  <div id="app">
    <table>
      <thead>
        <tr>
          <th>#</th>
          <th>Name</th>
          <th>Email</th>
          <th>Avatar</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in users" :key="user.id">
          <td>{{ user.id }}</td>
          <td>{{ user.first_name + " " + user.last_name }}</td>
          <td>{{ user.email }}</td>
          <td>
            <img :src="user.avatar" height="250" width="250" />
          </td>
        </tr>
      </tbody>
    </table>
    <Obsorver @intersecting="intersecting" />
  </div>
</template>

<script>
import Obsorver from "./components/Obsorver.vue";

export default {
  name: "App",
  data: () => {
    return {
      page: 0,
      users: []
    };
  },
  components: {
    Obsorver
  },
  methods: {
    async intersecting() {
      const res = await fetch(
        `https://reqres.in/api/users?page=${this.page++}`
      );
      const { data } = await res.json();
      this.users = [...this.users, ...data];
    }
  }
};
</script>

<style scoped>
img {
  border-radius: 25px;
}
</style>