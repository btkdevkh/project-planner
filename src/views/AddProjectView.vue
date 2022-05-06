<template>
  <form @submit.prevent="handleSubmit">
    <input type="text" v-model="title" required placeholder="Title">
    <textarea v-model="details" required placeholder="Details"></textarea>
    <button>Add Project</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      title: '',
      details: '',
      url: 'http://localhost:3000/projects'
    }
  },
  methods: {
    handleSubmit() {
      const project = {
        title: this.title,
        details: this.details,
        complete: false
      }

      fetch(this.url, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(project)
      })
        .then(() => this.$router.push('/'))
        .catch(err => console.log(err))
    }
  }
}
</script>

<style>
form {
  border-radius: 5px;
  text-align: center;
  max-width: 320px;
  margin: 0 auto;
  background-color: aliceblue;
  padding: 25px;
}

input, textarea {
  border-radius: 5px;
  width: 100%;
  padding: 10px;
  margin-bottom: 15px;
}

form button {
  padding: 10px;
  border: none;
  color: white;
  background-color: blueviolet;
  cursor: pointer;
  border-radius: 5px;
}
</style>