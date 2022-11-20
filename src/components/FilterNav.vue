<template>
	<nav class="filter-nav">
		<button @click="updateFilter('all')" :class="{active : current === 'all'}">All</button>
		<button @click="updateFilter('completed')" :class="{active : current === 'completed'}">Completed</button>
		<button @click="updateFilter('ongoing')" :class="{active : current === 'ongoing'}">Ongoing</button>
	</nav>
</template>
<script>
export default {
	emits: ["filter-change"],
	props: ["current"], 
	methods: {
		updateFilter(by) {
			this.$emit('filter-change', by)
		}
	},
}
</script>
<style>
.filter-nav button{
	background-color: none;
	border: none;
	color: rgb(182, 179, 179);
	outline: none;
	font-size: 12px;
	text-transform: uppercase;
	margin-right: 10px;
	letter-spacing: 1px;
	font-weight: bold;
	cursor: pointer;
}
.filter-nav button.active{
	color: #555;
}
</style>