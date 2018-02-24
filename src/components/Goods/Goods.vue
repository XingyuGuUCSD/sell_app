<template>
	<div class="goods">
		<!-- 分类 -->
		<div class="menu-wrapper" ref="menuScroll">
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

		<!-- 商品列表 -->
		<div class="foods-wrapper" ref="foodScroll">
			<ul>
				<!-- 专场 -->
				<li class="container-list food-list-hook">
					<div v-for="item in container.operation_source_list">
						<img :src="item.pic_url"/>
					</div>
				</li>
				<!-- 具体分类 -->
				<li v-for="item in goods" class="food-list food-list-hook">
					<!-- 具体商品 -->
					<h3 class="title">{{item.name}}</h3>
					<ul>
						<li v-for="food in item.spus" class="food-item">
							<div class="icon" :style="head_bg(food.picture)"></div>
							<div class="content">
								<h3 class="name">{{food.name}}</h3>
								<p class="desc" v-if="food.description">{{food.description}}</p>
								<div class="extra">
									<span class="saled">{{food.month_saled_content}}</span>
									<span class="praise">{{food.praise_content}}</span>
								</div>
								<img class="product" :src="food.product_label_picture"/>
								<p class="price">
									<span class="text">￥{{food.min_price}}</span>
									<span class="unit">/{{food.unit}}</span>
								</p>
							</div>
						</li>
					</ul>
				</li>
			</ul>
		</div>
	</div>
</template>

<script>

	import BSroll from 'better-scroll'


	export default{
		data(){
			return {
				container: {},
				goods: [],
				listHeight:[]
			}
		},
		//vue生命周期
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
                	//调用scroll
                	//that.initScroll();
                	//开始时dom元素没有渲染。即高度上有问题
                	//在获取到数据后，并DOM已经被渲染，表示列表高度是没有问题
                	//nextTick
                	that.$nextTick( ()=>{
                		//DOM已经更新
                			that.initScroll();
                			that.calculateHeight();
                		}
                	);
              	}
            })
            .catch(function (error) {//出错数据
              console.log(error);
            });
    	},
    	methods: {
    		head_bg(imgName){
    			return "background-image: url(" + imgName + ");"
    		},

    		//滚动的初始化
    		initScroll(){
    			//ref属性就是用来绑定某个dom元素或者某个组件的，然后在this.$ref中
    			new BSroll(this.$refs.menuScroll);
    			new BSroll(this.$refs.foodScroll);
    		},

    		calculateHeight(){
    			// 通过$refs获取到相应的数据
    			let foodlist = this.$refs.getElementsByClassName("food-list-hook");

    			//添加到数组区间
    			//0-216第一个区间（专场）
    			//217-1342第二个区间（热销）
    			let height = 0;
    			this.listHeight.push(height);
    			

    		}
    	}
    	// computed: {//计算属性不能传递参数

    	// }
	}
</script>

<style>
	@import url("Goods.css");
</style>