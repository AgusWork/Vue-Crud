<template>
	<InsertComponent />
</template>

<script>
import InsertComponent from "./components/ListComponent.vue";

export default {
	name: "App",
	components: {
		InsertComponent,
	},
};
</script>

<style>
body{
	background: linear-gradient(135deg, #f5f7fa, #c3cfe2);
	margin: 0;
	padding: 0;
}
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;    
	color: #2c3e50;
	
}
</style>
