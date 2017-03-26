<template>
	<div class="bottom">
		<div class="content">
			<p class="text-wrapper">
				<ol>
					<li v-for="text in czz.texts" >
						{{ text }}
					</li>
				</ol>	
			</p>
			<div class="img-wrapper">
				<img src="static/imgs/pc.png">
			</div>
		</div>
	</div>
</template>

<script>
export default {
	props: {
		czz: {
			type: Object
		}
	}
};
</script>

<style lang="stylus" rel='stylesheet/stylus'>
	@import "../../common/stylus/mixin.styl"
	
	.bottom
		background: #00d3ff
		.content
			position: relative
			display: flex
			margin: 0 auto
			padding: 50px
			box-sizing: border-box
			font-size: 0
			color: #3e484a
			width-change()
			.img-wrapper
				position: absolute
				display: inline-block
				flex: 0 0 390px
				right: 0
				top: 30px
				img
					width: 80%
			.text-wrapper
				position: relative
				left: -40px
				display: inline-block
				flex: 1
				font-size: 18px
				line-height: 30px
				color: #3e484a
				ol,li
					list-style: decimal
    

</style>
