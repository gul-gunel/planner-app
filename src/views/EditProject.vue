<template>
	<form @submit.prevent="handleEditSubmit">
		<label for="t">Title : </label>
		<input type="text" v-model="title" required>
		<label for="d">Details : </label>
		<textarea id="d" rows="5" v-model="details" required></textarea>
		<button class="btn">Update Project</button>
	</form>
</template>
<script>
export default {
	props: ["id"],
	data() {
		return {
			title: '',
			details: '',
			url: "http://localhost:3000/projects/" + this.id
		}
	},
	mounted() {
		fetch(this.url)
			.then(project_response => project_response.json())
			.then((data) => {
				this.title = data.title
				this.details = data.details
			})
	},
	methods: {
		handleEditSubmit() {
			fetch(this.url, {
				method: 'PATCH',
				headers: { "Content-Type": "application/json" },
				body: JSON.stringify({title: this.title, details: this.details})
			})
				.then(() => this.$router.push({name: 'Home'}))
				.catch((e) => console.error(e))
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
