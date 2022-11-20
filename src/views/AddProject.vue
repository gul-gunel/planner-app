<template>
  <form @submit.prevent="handleSubmit">
    <label for="title">Title : </label>
    <input type="text" v-model="title" required id="title">
    <label for="details">Details : </label>
    <textarea v-model="details" required id="details" rows="5"></textarea>
    <button class="btn">Add Project</button>
  </form>
</template>
<script>
export default {
  data() {
    return {
      title: '',
      details: ''
    }
  },
  methods: {
    handleSubmit() {
      let project = {
        title: this.title,
        details: this.details,
        completed: false
      }
      fetch("http://localhost:3000/projects", {
        method: "POST",
        headers: {'Content-Type': 'application/json'},
        body: JSON.stringify(project)
      })
        // .then(() => this.$router.push('/'))
        .then(() => this.$router.push({ name: 'Home' }))
        .catch(err => console.error(err))
    }
  },
}
</script>
<style>
*{
  box-sizing: border-box;
}
form{
  background-color: #fff;
  padding: 20px;
  border-radius: 10px;
}
label{
  display: block;
  color: #bbb;
  text-transform: uppercase;
  font-size: 14px;
  font-weight: bold;
  letter-spacing: 1px;
  margin: 20px 0 10px 0;
}
input, textarea{
  padding: 10px;
  border: none;
  border-bottom: 1px solid #bbb;
  width: 100%;
  outline: none;
}
textarea{
  border: 1px solid #bbb;
}
.btn{
  display: block;
  margin: 20px auto 0;
  background-color: #76dd78;
  color: #fff;
  padding: 10px;
  border: none;
  border-radius: 7px;
  font-size: 16px;
}
</style>