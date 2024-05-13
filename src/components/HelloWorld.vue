<template>
  <div class="container m-2 m-auto">
    <div class="row row-cols-5">
      <div class="col mb-2" v-for="(user, index) in users" :key="index">
        <div class="card p-3 mr-2 ">
          <img v-bind:src="user.picture" :alt="`${ user.firstName} ${ user.lastName}`" :class=" user.gender" class="m-auto" />
          <h1>{{  user.irstName }} {{  user.lastName }}</h1>
          <h3>Gender: {{  user.gender }}</h3>
          <h3>Email: {{  user.email }}</h3>
          <!-- <button :disabled="loading" :class="gender" @click="getUser()">Get Random User</button> -->
        </div>
      </div>
    </div>
  </div>

</template>

<script>
export default {
  data() {
    return {
      users: []
    }
  },
  mounted() {
    this.getUser();
  },
  methods: {
    async getUser() {
      this.loading = true;
      try {
        const response = await fetch('https://randomuser.me/api/?results=100');
        const data = await response.json();
        console.log(data);
        this.users = await data.results.map(user => ({
          firstName: user.name.first,
          lastName: user.name.last,
          email: user.email,
          gender: user.gender,
          picture: user.picture.large,
        }));

        console.log(users);
      } catch (error) {
        console.error('Error fetching users:', error);
      } finally {
       this.loading = false;
      }
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

html,
body {
  font-family: Arial, Helvetica, sans-serif;
}

#app {
  width: 400px;
  height: 100vh;
  margin: auto;
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

h1,
h3 {
  margin-bottom: 1rem;
  font-weight: normal;
}

img {
  border-radius: 50%;
  border: 5px #333 solid;
  margin-bottom: 1rem;
  width: 150px;
  height: 150px;
}

.male {
  border-color: steelblue;
  background-color: steelblue;
}

.female {
  border-color: pink;
  background-color: pink;
  color: #333;
}

button {
  cursor: pointer;
  display: inline-block;
  background: #333;
  color: white;
  font-size: 18px;
  border: 0;
  padding: 1rem 1.5rem;
}

button:focus {
  outline: none;
}

button:disabled {
  background-color: #727272 !important;
}

button:hover {
  transform: scale(0.98);
}
</style>
