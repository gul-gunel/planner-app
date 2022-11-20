<template>
	<nav class="main-nav">
		<router-link :to="{name: 'Home'}">Home</router-link> |
		<router-link :to="{name: 'AddProject'}">Add New Project</router-link>
	</nav>
</template>
<script>
export default {
	
}
</script>
<style>
.main-nav{
	text-align: center;
	margin: 30px auto;
}
/* vue'de router-link html'e a etiketi olarak geçer */
.main-nav a{
	display: inline-block;
	text-decoration: none;
	margin: 0 10px;
	color: #999;
	font-size: 18px;
} 
/* vue'da active classıdır. a:active gibi */
a.router-link-active{
	border-bottom: 2px solid #76dd78;
	padding-bottom: 4px;
	color: #76dd78;
}
</style>