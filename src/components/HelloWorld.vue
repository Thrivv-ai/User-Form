<template>
  <v-app>
    <v-main class="main">
      <div class="container">
        <div>
          <v-text-field v-model="name" clearable label="Name" variant="outlined"></v-text-field>
        </div>
        <div>
          <v-text-field v-model="phone" clearable label="Phone Number" variant="outlined"></v-text-field>
        </div>
        <div>
          <v-text-field v-model="email" clearable label="Email" variant="outlined"></v-text-field>
        </div>
        <div>
          <button @click="submitForm">Submit</button>
        </div>
      </div>
    </v-main>
  </v-app>
</template>

<script setup>
</script>

<script>
import axios from "axios";
export default {
  data() {
    return {
      name: '',
      phone: '',
      email: ''
    };
  },

  methods: {
    async submitForm() {
      try {
        let user_data = {
          name: this.name,
          phone: this.phone,
          email: this.email
        }
        let URL = process.env.VUE_APP_BACKEND_URL + '/submit';
        console.log("The URL is: ", URL)
        axios
          .post(URL, user_data)
          .then((data) => {
            console.log(data)
          })
          .catch((error) => {
            console.log('error', error)
          })
      } catch (error) {
        alert('Error submitting form');
        console.error(error);
      }
    }
  },
};
</script>

<style scoped>
.container {
  background: white;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
  justify-content: center;
}

input {
  display: block;
  width: 100%;
  margin: 10px 0;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

button {
  background-color: #007bff;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}
</style>