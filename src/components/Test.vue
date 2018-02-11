<template>
	<div class="test">
		I am in Test.vue
		{{msg}}
	</div>
</template>

<script>
export default{
	data(){
		return{
			msg: "I am in data Test.vue"
		}
	}
}
</script>

<style>
.test{
	color: red;
}
	
</style>