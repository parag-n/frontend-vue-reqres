<template>
  <form id="userForm">
    <table class="table table-dark">
      <tbody>
        <tr>
          <td>ADD NEW USER</td>
          <td>
            <input
              @blur="inputField"
              type="text"
              id="avatar"
              name="avatar"
              placeholder="Image URL"
              required
            />
          </td>
          <td>
            <input
              @blur="inputField"
              type="text"
              id="first_name"
              name="first_name"
              placeholder="First Name"
              required
            />
          </td>
          <td>
            <input
              @blur="inputField"
              type="text"
              id="last_name"
              name="last_name"
              placeholder="Last Name"
              required
            />
          </td>
          <td>
            <input
              @blur="inputField"
              type="text"
              id="trigram"
              name="trigram"
              placeholder="Trigram"
              required
            />
          </td>
          <td>
            <input
              @blur="inputField"
              type="text"
              id="email"
              name="email"
              placeholder="Email"
              required
            />
          </td>
          <td>
            <select @blur="inputField" id="role" name="role" required>
              <option value="default" selected disabled>
                -- Select Your Role --
              </option>
              <option value="Services Software Consultant">
                Services Software Consultant
              </option>
              <option value="Software Engineer">Software Engineer</option>
              <option value="DevOps Engineer">DevOps Engineer</option>
            </select>
          </td>
          <td>
            <button
              @click.prevent="addUser"
              type="submit"
              class="btn btn-success"
            >
              Add User
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </form>
</template>

<script>
import MyAxios from "@/custom-config/MyAxios";

export default {
  name: "AddUser",
  props: ["userlist"],
  data() {
    return {
      user: {},
    };
  },
  methods: {
    inputField(value) {
      this.user = { ...this.user, [value.target.name]: value.target.value };
    },
    addUser() {
      console.log(this.user);

      MyAxios.post("/users", this.user)
        .then((response) => {
          console.log(response.data);
          this.$emit('addNewUser', response.data);
          document.getElementById("userForm").reset();
        });
    },
  },
};
</script>
