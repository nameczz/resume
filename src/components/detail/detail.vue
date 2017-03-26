<template>
  <div class="detail">
  	<div class="content">
  		<triangle ></triangle>
  		<div class="pic-wrapper">
  			<carousel v-if="img === ''"></carousel>
  			<img :src="img" v-else>
  		</div>
    	<div class="skill-wrapper">
    		<ul>
    			<li v-for="skill in skills">
    				<skills 
	    				:circleArea="circleArea" 
	    				:skillPercent="skill.value" 
	    				:skillName="skill.name">
    				</skills>
    			</li>
    		</ul>
    	</div>
    	<div class="text-wrapper">
    		<p class="description">
    			<ol>
    				<li v-for="text in desc">
    					{{ text }}
    				</li>
    			</ol>	
    		</p>
    	</div>
    	<div class="btn" @click="backToMain(4)">
    		<parallelogram desc="返回项目列表"></parallelogram>
    	</div>
  	</div>
  </div>
</template>

<script>
import triangle from 'components/triangle/triangle';
import carousel from 'components/carousel/carousel';
import skills from 'components/skills/skills';
import parallelogram from 'components/parallelogram/parallelogram';

export default {
	props: {
		img: {
			type: String,
			default: ''
		},
		skills: {
			type: Array
		},
		desc: {
			type: Array
		}
	},
	data () {
		return {
			circleArea: [150, 150]
		};
	},
	components: {
		'triangle': triangle,
		'carousel': carousel,
		'skills': skills,
		'parallelogram': parallelogram
	},
	methods: {
		backToMain (destination) {
			this.$emit('showMain', destination);
		}
	}
};
</script>

<style lang="stylus" rel='stylesheet/stylus'>
@import "../../common/stylus/mixin.styl"

  .detail
    background: #3e484a
    .content
    	position: relative
    	margin: 0 auto
    	padding: 50px 50px 0 50px
    	width: 1200px
    	height: 1000px
    	.pic-wrapper
    		position: relative
    		z-index: 100
    		margin-bottom:50px
    	.skill-wrapper
    		position: absolute
    		top:138px
    		right:50px
    		li
    			margin-bottom: 100px
    	.description
    		width:700px
    		padding:10px
    		line-height:30px
    		color: #FFFAFA
    		ol
    			list-style-type: decimal
    			li
    				list-style: inherit
    	.btn
    		position: absolute
    		bottom: 50px
    		right: 150px
    		text-align: right
    		cursor: pointer
    		paralle-bgColor(60deg, #6e7c85, 330px)
    		&:hover
    			paralle-bgColor(60deg, #00d3ff, 330px)
</style>
