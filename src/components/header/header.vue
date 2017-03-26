<template>
  <div class="header">
  	<div class="content">
  		<div class="avatar">
    		<img src="./img/avatar.png" width="182" height="180">
    	</div>
	    <div class="description">
	    	<parallelogram :desc="desc[0]" class="title"></parallelogram>
	    	<p>
	    		<ul>
	    			<li v-for="item in czz.description">
	    				{{ item }}
	    			</li>
	    		</ul>
	    	</p>
	    </div>
	    <div class="contact">
	    	<parallelogram :desc="desc[1]" class="title"></parallelogram>
	    	<span class="text">
	    		<i class="iconfont icon-youxiang"></i>
	    	{{ czz.email }}
	    	</span>
	    	<span class="text">
	    		<i class="iconfont icon-shouji"></i>
	    	{{ czz.phone }}
	    	</span>
	    	<span class="text">
	    		<i class="iconfont icon-github"></i>
	    		<a :href="czz.github">{{ czz.github }}</a>
	    	</span>
	    </div>
  	</div>
  </div>
</template>

<script>
import parallelogram from 'components/parallelogram/parallelogram';

export default {
	props: {
		czz: {
			type: Object
		}
	},
	data () {
		return {
			desc: ['WHO I AM', 'CONTACT']
		};
	},
	components: {
		'parallelogram': parallelogram
	}
};
</script>

<style lang="stylus" rel='stylesheet/stylus'>
	@import "../../common/stylus/mixin.styl"

	.header
		background: #00d3ff
		.content
			display: flex
			margin: 0 auto
			padding: 50px
			box-sizing: border-box
			background: #00d3ff
			font-size: 0
			color: #3e484a
			width-change()
			.avatar
				position: relative
				display: inline-block
				flex: 0 0 350px
				// 解决垂直居中
				img
					position: absolute
					top: 50%
					left: 40%
					transform: translate(-50%, -40%)
			.description
				display: inline-block
				flex: 1
				padding: 5px 80px 5px 5px
				line-height: 35px
				margin-right: 30px
				text-align: justify
				.title
					width: 332px
					margin-bottom: 30px
					text-align: left
					font-size: 36px
					paralle-bgColor(-50deg, #3e484a, 322px)
				p
					font-size: 18px
			.contact
				display: inline-block
				flex: 1
				font-size: 20px
				padding: 5px
				line-height: 35px
				.title
					margin-bottom: 30px
					font-size: 36px
					paralle-bgColor(-60deg, #3e484a, 322px)
				.text
					display: block
					.icon-youxiang,.icon-shouji,.icon-github
						color: white
						font-size: 20px
						padding-right: 5px
					a
						color: #3e484a
			
</style>
