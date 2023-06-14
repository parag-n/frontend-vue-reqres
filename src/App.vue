<template>
  <div>
    <user-list :userlist="allUsers" @remove="deleteUser" />
  </div>
</template>

<script>
import axios from "axios";
import UserList from "./components/UserList"

export default {
  name: "App",
  data() {
    return{
      allUsers: []
    }
  },
  components: {
    UserList  
  },
  mounted() {
    axios.get("https://reqres.in/api/users").then(
      (response) => {
        this.allUsers = response.data.data;
        console.log(response.data.data)
      },
      (reason) => {
        console.log(reason);
      }
    );
  },
  methods: {
    deleteUser(id){
      this.allUsers = this.allUsers.filter((user)=>{ return user.id!==id})
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
