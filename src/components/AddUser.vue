<template>
  <form id="userForm" class="table table-dark">
    <table>
      <tbody>
        <tr>
          <td>ADD NEW USER</td>
          <td>
            <input
              @blur="saveAttribute"
              type="text"
              id="first_name"
              name="first_name"
              placeholder="First Name"
              required
            />
          </td>
          <td>
            <input
              @blur="saveAttribute"
              type="text"
              id="last_name"
              name="last_name"
              placeholder="Last Name"
              required
            />
          </td>
          <td>
            <input
              @blur="saveAttribute"
              type="text"
              id="trigram"
              name="trigram"
              placeholder="Trigram"
              required
            />
          </td>
          <td>
            <input
              @blur="saveAttribute"
              type="text"
              id="email"
              name="email"
              placeholder="Email"
              required
            />
          </td>
          <td>
            <select @blur="saveAttribute" id="role" name="role" required>
              <option value="default" selected disabled>
                -- Select Your Role --
              </option>
              <option v-for="role in roles" :value="role" :key="role">
                {{ role }}
              </option>
            </select>
          </td>
          <td>
            <button
              @click.prevent="$emit('add', user)"
              @click="resetForm"
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
export default {
  name: "AddUser",

  // props to be received from the parent element
  props: ["roles", "imageUrl"],

  data() {
    return {
      user: {},
    };
  },

  methods: {
    // updating the user object with respective inputs
    saveAttribute(event) {
      this.user = { ...this.user, [event.target.name]: event.target.value };

      // while updating the trigram, we also update the url of avatar
      if (event.target.name == "trigram") {
        this.user = {
          ...this.user,
          avatar:
            this.imageUrl.prefix + event.target.value + this.imageUrl.suffix,
        };
      }
    },

    // resetting the user form once submit is clicked
    resetForm() {
      document.getElementById("userForm").reset();
    },
  },
};
</script>
