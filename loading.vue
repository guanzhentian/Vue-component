<template>
	<div class="m-loading" id="mloading" v-show="isShow">
		<div class="m-content">
			<div class="m1">
				<div class="m-box1"></div>
				<div class="m-box1"></div>
				<div class="m-box1"></div>
				<div class="m-box1"></div>
				<div class="m-box1"></div>
				<div class="m-box1"></div>
				<div class="m-box1"></div>
				<div class="m-box1"></div>
				<div class="m-box1"></div>
				<div class="m-box1"></div>
			</div>
			<div class="m2">
				<div class="m-box2"></div>
				<div class="m-box2"></div>
				<div class="m-box2"></div>
				<div class="m-box2"></div>
				<div class="m-box2"></div>
				<div class="m-box2"></div>
				<div class="m-box2"></div>
				<div class="m-box2"></div>
				<div class="m-box2"></div>
				<div class="m-box2"></div>
			</div>
		</div>
	</div>
</template>
<script type="text/javascript">
	export default{
		props:{
			isShow:{
				type:Boolean,
				default:false
			}
		}
	}
</script>
<style type="text/css" scoped lang="less">
	.m-loading{
		width:100%;
		height:100%;
		background-color: rgba(0,0,0,0.5);
		position: fixed;
		left:0;
		top:0;
		z-index:200;
		display: flex;
		align-items: center;
		justify-content: center;
		.m-content{
			width:200px;
			height:100px;
			.m1{
				width:200px;
				display: flex;
				.m-box1{
					flex: 0 0 10px;
					height:10px;
					position: relative;
					background-color: transparent;
					border-radius: 50%;
					margin-right: 10px;
					animation:box1 0.9s;
					animation-timing-function: ease-in-out;
					animation-direction: alternate;
					animation-iteration-count: infinite;
				}
				.m-box1:nth-child(2){
					animation-delay:0.15s;
				}
				.m-box1:nth-child(3){
					animation-delay:0.3s;
				}
				.m-box1:nth-child(4){
					animation-delay:0.45s;
				}
				.m-box1:nth-child(5){
					animation-delay:0.6s;
				}
				.m-box1:nth-child(6){
					animation-delay:0.75s;
				}
				.m-box1:nth-child(7){
					animation-delay:0.9s;
				}
				.m-box1:nth-child(8){
					animation-delay:1.05s;
				}
				.m-box1:nth-child(9){
					animation-delay:1.2s;
				}
				.m-box1:nth-child(10){
					animation-delay:1.45s;
				}
			}
			.m2{
				width:200px;
				margin-top: 90px;
				display: flex;
				.m-box2{
					flex: 0 0 10px;
					height:10px;
					position: relative;
					background-color: transparent;
					border-radius: 50%;
					margin-right: 10px;
					animation:box2 0.9s;
					animation-timing-function: ease-in-out;
					animation-direction: alternate;
					animation-iteration-count: infinite;
				}
				.m-box2:nth-child(2){
					animation-delay:0.15s;
				}
				.m-box2:nth-child(3){
					animation-delay:0.3s;
				}
				.m-box2:nth-child(4){
					animation-delay:0.45s;
				}
				.m-box2:nth-child(5){
					animation-delay:0.6s;
				}
				.m-box2:nth-child(6){
					animation-delay:0.75s;
				}
				.m-box2:nth-child(7){
					animation-delay:0.9s;
				}
				.m-box2:nth-child(8){
					animation-delay:1.05s;
				}
				.m-box2:nth-child(9){
					animation-delay:1.2s;
				}
				.m-box2:nth-child(10){
					animation-delay:1.45s;
				}
			}
		}
	}

	@keyframes box1{
		from {top:0; background-color: rgb(227,140,173);}
		to{top:100px;background-color: rgb(144,33,74);}
	}
	@keyframes box2{
		from {top:0;background-color: rgb(155,234,247) }
		to{top:-100px;background-color: rgb(30,75,156)}
	}
</style>