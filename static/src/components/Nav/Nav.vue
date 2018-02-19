<template>

	<div class="nav">
		<!-- <div class="nav-item goods">
			点菜
		</div>

		<div class="nav-item ratings">
			评价
		</div>

		<div class="nav-item seller">
			商家
		</div> -->

		<!-- 使用router-link组件来导航 -->
		<!-- 通过传入‘to’属性指定链接 -->
		<!-- router-link默认会被渲染成为一个<a>链接 -->
		<router-link to="/goods" class="nav-item">
			点菜
			<i class="line"></i>
		</router-link>

		<router-link to="/ratings" class="nav-item">
			评价
			<i class="line"></i>
		</router-link>
		<router-link to="/seller" class="nav-item">
			商家
			<i class="line"></i>
		</router-link>
	</div>

</template>

<script>
	export default{

	}
</script>

<style>
	.nav{
		display: flex;
		width:100%;
		height: 40px;
		line-height: 40px;
		border-bottom: 1px solid #e4e4e4;
	}

	.nav .nav-item{
		flex: 1;
		text-align: center;
		font-size: 13px;
		text-decoration: none;
		color:#666666;
		position: relative;
	}

	.nav .active{
		color: #FFBB22;
	}

	.nav .active .line{
		width: 21px;
		height: 2px;
		display: inline-block;
		background-color: #FFBB22;
		position: absolute;
		left: 50%;
		bottom: 0;
		margin-left: -10px; 

	}
</style>