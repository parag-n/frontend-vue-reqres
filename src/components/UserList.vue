<template>
  <table class="table table-dark table-striped">
    <thead>
      <tr>
        <th colSpan="12" class="table-warning">List Of All Users</th>
      </tr>
      <tr>
        <th>ID</th>
        <th>Image</th>
        <th>First Name</th>
        <th>Last Name</th>
        <th>Email</th>
        <th>Action</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="user in userlist" :key="user.id">
        <td>{{ user.id }}</td>
        <td><img :src="user.avatar" /></td>
        <td>{{ user.first_name }}</td>
        <td>{{ user.last_name }}</td>
        <td>{{ user.email }}</td>
        <td><button @click="$emit('remove', user.id)" class="btn btn-danger">Delete</button></td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: "UserList",
  props: ["userlist"],
};
</script>

<style></style>
