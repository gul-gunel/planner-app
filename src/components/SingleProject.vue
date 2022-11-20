<template>
	<div class="project" :class="{ complete : project.completed}">
		<div class="actions">
			<h3 @click="showDetails = !showDetails"> {{ project.title }} </h3>
			<div class="icons">
				<router-link :to="{ name : 'EditProject', params: { id: project.id }}">
					<span class="material-icons">edit</span>
				</router-link>
				<span @click="deleteProject" class="material-icons">delete</span>
				<span @click="toggleComplete" class="material-icons">done</span>
			</div>
		</div>
		<div v-if="showDetails" class="details">
			<p> {{ project.details }} </p>
		</div>
	</div>
</template>
<script>
export default {
	props: ["project"],
	emits: ["delete", "complete"],
	data() {
		return {
			showDetails: false,
			url: "http://localhost:3000/projects/" + this.project.id,
		}
	},
	methods: {
		deleteProject() {
			fetch(this.url, { method: "DELETE" })
				.then(() => this.$emit("delete", this.project.id))
				.catch(e => console.error(e))
		},
		toggleComplete() {
			fetch(this.url, {
				method: "PATCH",
				headers: {'Content-Type': 'application/json'},
				body: JSON.stringify({ completed: !this.project.completed})
			} )
				.then(() => this.$emit('complete', this.project.id))
				.catch(e => console.error(e))
		}
	},
}
</script>
<style>
.project {
	margin: 20px auto;
	background-color: #fff;
	padding: 10px 20px;
	border-radius: 5px;
	box-shadow: 1px 2px 3px rgba(0, 0, 0, .5);
	border-left: 8px solid #dd8f11ce;
}
.project.complete {
	border-left: 8px solid #76dd78;
}
.project.complete .icons > .material-icons:last-child {
	color: #76dd78;
	font-weight: 600;
}
h3 {
	cursor: pointer;
}
.actions {
	display: flex;
	justify-content: space-between;
	align-items: center;
}
.material-icons {
	font-size: 24px;
	margin-left: 10px;
	color: #bbb;
	cursor: pointer;
}
.material-icons:hover {
	color: #777;
}
</style>

