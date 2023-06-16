<template>
  <div>
    <add-user :roles="roles" :imageUrl="imageUrl" @add="addUser" />
    <user-list :userlist="allUsers" @remove="removeUser" />
    <v-grid :source="dummyusers" :columns="columns"></v-grid>
  </div>
</template>

<script>
import UserList from "./components/UserList";
import AddUser from "./components/AddUser";
import VGrid from "@revolist/vue3-datagrid";
import MyAxios from "./custom-config/MyAxios";

export default {
  name: "App",

  data() {
    return {
      allUsers: [],
      roles: [],
      imageUrl: {},
      // specification for datagrid trial
      columns: [
        { prop: "id", name: "ID" },
        { prop: "avatar", name: "Profile Picture" },
        { prop: "first_name", name: "First Name" },
        { prop: "last_name", name: "Last Name" },
        { prop: "trigram", name: "Trigram" },
        { prop: "email", name: "Email" },
        { prop: "role", name: "Role" },
      ],
      // source for datagrid trial
      dummyusers: [
        {
          id: "1",
          avatar: "Hello",
          first_name: "Parag",
          last_name: "Nukalwar",
          trigram: "PNR11",
          email: "parag.nukalwar@3ds.com",
          role: "Software Engineer",
        },
      ],
    };
  },

  // list of all the child components
  components: {
    AddUser,
    UserList,
    VGrid,
  },

  // this method will be called as soon as the app is mounted. We will retrieve all the data that is required in the beginning.
  mounted() {
    // retrieving all the users from database and storing them locally
    MyAxios.get("/users")
      .then((response) => {
        this.allUsers = response.data;
      })
      .catch(() => {
        console.log("start the server first\n");
      });

    // retrieving the roles from database and storing them locally
    MyAxios.get("/roles").then((response) => {
      this.roles = response.data;
    });

    // getting the image url for the profile pictures
    MyAxios.get("/imageurl").then((response) => {
      this.imageUrl = response.data;
    });
  },

  methods: {
    // Deleting a specified user from the database and updating the local cache of users.
    removeUser(id) {
      MyAxios.delete(`/users/${id}`).then(() => {
        MyAxios.get("/users").then((response) => {
          this.allUsers = response.data;
        });
      });
    },

    // Posting a user to the database and updating the local cache of users.
    addUser(user) {
      MyAxios.post("/users", user).then(() => {
        MyAxios.get("/users").then((response) => {
          this.allUsers = response.data;
        });
      });
    }
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
