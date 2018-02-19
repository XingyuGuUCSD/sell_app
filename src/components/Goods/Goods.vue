<template>
	<div class="goods">
		<!-- 分类 -->
		<div class="menu-wrapper">
			<ul>
				<!-- 专场 -->
				<li class="menu-item">
					<p class="text">
						<img :src="container.tag_icon" v-if="container.tag_icon" class="icon"/>
						{{container.tag_name}}
					</p>
				</li>
				<li class="menu-item" v-for="item in goods">
					<p class="text">
						<img :src="item.icon" v-if="item.icon" class="icon"/>
						{{item.name}}
					</p>
				</li>
			</ul>
		</div>
		<div class="foods-wrapper"></div>
	</div>
</template>

<script>


	export default{
		data(){
			return {
				container: {},
				goods: []
			}
		},
		created(){//发起异步请求，获取数据

    		var that = this;
    		//通过axios发起get请求
      		this.$axios.get('/api/goods')
            	.then(function (response) {//获取到数据
             	 //console.log(response);
              	var dataSource = response.data;
              	console.log(dataSource);
              	if(dataSource.code == 0){
                	that.container = dataSource.data.container_operation_source;
                	that.goods = dataSource.data.food_spu_tags;
                console.log(that.container);
              	}
            })
            .catch(function (error) {//出错数据
              console.log(error);
            });
    	}
	}
</script>

<style>
	@import url("Goods.css");
</style>