<template>
	<div class="star">
		<span v-for="itemClass in itemClasses" :class="itemClass" class="star-item"></span>


	</div>
</template>

<script>

	//星星的长度
	const LENGTH = 5;
	const CLS_ON = 'on';
	const CLS_HALF = 'half';
	const CLS_OFF = 'off';


	export default{
		//对外接口
		props:{
			score:{
				type: Number
			}
		},

		computed:{
			itemClasses(){
				let result = [];
				let score = Math.floor(this.score*2)/2;
				let hasDemical = score %1 !==0;
				let integer = Math.floor(score);
				for(let i = 0; i < integer; i++){
					result.push(CLS_ON);
				}

				if(hasDemical){
					result.push(CLS_HALF);
				}
				while(result.length < LENGTH){
					result.push(CLS_OFF);
				}

				return result;
			}
		},
	}
</script>

<style>
	.star{
		font-size: 0;
	}
	.star .star-item{
		display: inline-block;
		width: 10px;
		height: 10px;
		margin-right: 3px;
		background-repeat: no-repeat;
		background-size: 10px 10px;
	}
	.star .star-item:last-child{
		margin-right: 0px;
	}

	/*三种图片类型*/
	.star .on{
		background-image: url(star24_on@2x.png);
	}

	.star .half{
		background-image: url(star24_half@2x.png);
	}

	.star .off{
		background-image: url(star24_off@2x.png);
	}
</style>