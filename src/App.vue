<template>
  <div>
    <add-user :userlist="allUsers" @addNewUser="addUser"/>
    <user-list :userlist="allUsers" @remove="deleteUser"/>
  </div>
</template>

<script>
import axios from "./custom-config/MyAxios";
import UserList from "./components/UserList"
import AddUser from "./components/AddUser"

export default {
  name: "App",
  data() {
    return{
      allUsers: []
    }
  },
  components: {
    AddUser,
    UserList  
  },
  mounted() {
    axios.get("/users").then(
      (response) => {
        this.allUsers = response.data;
      },
      (reason) => {
        console.log(reason);
      }
    );
  },
  methods: {
    deleteUser(id){
      this.allUsers = this.allUsers.filter((user)=>{ return user.id!==id})
    },
    addUser(user){
      this.allUsers = [...this.allUsers, user];
    }
  }
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
