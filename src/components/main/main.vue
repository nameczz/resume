<template>
  <div class="main">
  	<div class="content ">
		<triangle></triangle>
  		<div class="h2-wrapper clearfix">
  			<h2 class="h2-left">
  				<i class="iconfont icon-zuopin"></i>
  				WORKINGS
  			</h2>
  			<span class="tips">项目Tips可点击</span>
  			<h2 class="h2-right">
  				<i class="iconfont icon-jingyan"></i>
  				EXPERIENCE
  			</h2>
  		</div>
  		<div class="circle-wrapper">
  			<ul>
  				<li v-for="circle in circles" class="circle">
  					{{ circle }}
  				</li>
  			</ul>
  		</div>
  		<panting :area="area" :moves="moves" @drawFinish="show"></panting>
  		<div class="desc-right">
  			<ul>
	  			<li v-for="(item, index) in czz.titles" class="item clearfix" >
	  				<transition-group name="fade">
  						<div class="title" :class="{'title-left': item.type === 1}" :key="1" @click="showDetail(index)">
  							<parallelogram :desc="item.desc" v-show="showTitle"></parallelogram>
  						</div>
	  					<p :key="2" v-show="showTitle" :class="{'title-left': item.type === 1}">
		  					Github：<a :href="item.github">{{ item.github }}</a>
	  					</p>
	  				</transition-group>
	  			</li>
  			</ul>
  		</div>
  		<div class="desc-left">
  			<transition-group name="fade">
				<div  @click="showDetail(3)" :key="1">
					<parallelogram 
						:desc="'Jquery-2048'" 
						v-show="showTitle" 
						class="title">
					</parallelogram>
				</div>
				<p :key="2" v-show="showTitle">
					Github：<a href="https://github.com/nameczz/game-2048">https://github.com/nameczz/game-2048</a>
				</p>
			</transition-group>
  		</div>
  		<h2 class="software">
  			<i class="iconfont icon-ruanjianxiazai"></i>
  			SOFTWARE SKILLS
  		</h2>
  		<div class="skill-wrapper">
  			<ul>
  				<li v-for='skill in czz.skills' class="skill">
  					<skills 
  						:circleArea="circleArea" 
  						:skillName="skill.name" 
  						:skillPercent="skill.value">
  					</skills>
  				</li>
  			</ul>
  		</div>
  	</div>
  </div>
</template>

<script>
import panting from 'components/panting/pating';
import parallelogram from 'components/parallelogram/parallelogram';
import skills from 'components/skills/skills';
import triangle from 'components/triangle/triangle';

export default {
	props: {
		czz: {
			type: Object
		}
	},
	data () {
		return {
			circles: [2016, 2017.2, 2017.3],
			area: [1100, 972],
			moves: [
				{startX: 400, startY: 170, endX: 400, endY: 490},
				{startX: 398, startY: 170, endX: 798, endY: 170},
				{startX: 398, startY: 320, endX: 878, endY: 320},
				{startX: 398, startY: 490, endX: 798, endY: 490},
				{startX: 398, startY: 170, endX: 300, endY: 170},
				{startX: 300, startY: 170, endX: 300, endY: 240}
			],
			desc: ['WHO I AM', 'CONTACT'],
			showTitle: false,
			circleArea: [150, 150]
		};
	},
	methods: {
		show () {
			this.showTitle = true;
		},
		showDetail (num) {
			console.log(num);
			this.$emit('showDetail', num);
		}
	},
	components: {
		'panting': panting,
		'parallelogram': parallelogram,
		'skills': skills,
		'triangle': triangle
	}
};
</script>

<style lang="stylus" rel='stylesheet/stylus'>
	@import "../../common/stylus/mixin.styl"
	
	.main
		background: #3e484a
		.content
			position: relative
			margin: 0 auto
			padding: 50px 50px 0 50px
			width: 1200px
			height: 1000px
			.h2-wrapper
				position: relative
				margin-left: 50px
				z-index: 10
				width: 100%
				font-size: 36px
				color: #6e7c85
				.tips
					margin-left: 264px
					font-size: 26px
					font-style: italic
				.h2-left
					float: left
					.icon-zuopin
						font-size: 36px
						color: #00d3ff
				.h2-right
					float: right
					.icon-jingyan
						font-size: 36px
						color: #00d3ff
			.circle-wrapper
				position: relative
				margin: 50px auto 70px auto
				padding: 20px 0
				width: 100px
				border-right: 6px solid #6e7c85
				z-index: 8
				.circle
					position: relative
					right: -40%
					padding-top: 12px
					box-sizing: border-box
					margin-bottom: 30px
					width: 122px 
					height: 122px
					border-radius: 50%
					background: #00d3ff
					color: #fff
					font-size: 30px
					text-align: center
					line-height: 100px
					&:last-child
						margin-bottom: 0
			.desc-right
				position: absolute
				width: 320px
				top: 212px
				right: 120px
				z-index: 100
				.fade-enter-active, .fade-leave-active
					transition: all .5s
				.fade-enter, .fade-leave-active 
					transform: translateX(100px)
					opacity: 0
				.item
					width: 260px
					.title
						margin-bottom: 25px
						text-align: right
						cursor: pointer
						paralle-bgColor(60deg, #6e7c85, 330px)
						&:hover
							paralle-bgColor(60deg, #00d3ff, 330px)
					.title-left
						position: relative
						right: -38%
					p
						margin-bottom:56px
						color: #fff
						a
							color: #fff 
			.desc-left
				position: absolute
				top: 272px
				left: 90px
				z-index: 100
				.fade-enter-active, .fade-leave-active
					transition: all .5s
				.fade-enter, .fade-leave-active 
					transform: translateX(-100px)
					opacity: 0
				.title
					margin-bottom: 25px
					text-align: left
					cursor: pointer
					paralle-bgColor(-60deg, #6e7c85, 330px)
					&:hover
						paralle-bgColor(-60deg, #00d3ff, 330px)
				p
					color: #fff
					margin-bottom:36px
					a
						color: #fff
					
			.software
				margin-left: 50px
				font-size: 36px
				color: #6e7c85
				margin-bottom: 50px
				.icon-ruanjianxiazai
					font-size: 36px
					color: #00d3ff
			.skill-wrapper
				width: 1050px
				margin: 0 auto
				.skill
					display: inline-block
</style>
