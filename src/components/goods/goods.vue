<template>
	<div class="goods">
		<div class="menu-wrapper" ref="menuWrapper">
			<ul>
				<li v-for="(item, index) in goods" class="menu-item" :class="{'current':currentIndex===index}" @click="selectMenu(index,$event)">
					<span class="text">
						<span v-show="item.type>0" class="icon" :class="classMap[item.type]"></span>{{ item.name }}
					</span>
				</li>
			</ul>
		</div>
		<div class="foods-wrapper" ref="foodsWrapper">
			<ul>
				<li v-for="item in goods" class="food-list" ref="foodList">
					<h1 class="title">{{ item.name }}</h1>
					<ul>
						<li v-for="food in item.foods" class="food-item">
							<div class="icon">
								<img :src="food.icon" width="57" height="57">
							</div>
							<div class="content">
								<h2 class="name">{{ food.name }}</h2>
								<p class="desc">{{ food.description }}</p>
								<div class="extra">
									<span class="count">月售{{ food.sellCount }}份</span><span>好评率{{ food.rating }}%</span>
								</div>
								<div class="price">
									<span class="now">￥{{ food.price }}</span><span class="old" v-show="food.oldPrice">￥{{ food.oldPrice }}</span>
								</div>
							</div>
						</li>
					</ul>
				</li>
			</ul>
		</div>
	</div>
</template>

<script>
	import BScroll from 'better-scroll';
	const ERR_OK = 0;

	export default {
	props: {
	seller: {
	type: Object
	}
	},
	data() {
	return {
	goods: [],
	listHeight: [],
	scrollY: 0
	};
	},
	computed: {
	currentIndex() {
	for (let i = 0; i < this.listHeight.length; i++) {
	let height1 = this.listHeight[i];
	let height2 = this.listHeight[i + 1];
	if ((this.scrollY >= height1 && this.scrollY < height2) || !height2) {
	return i;
	}
	}
	return 0;
	}
	},
	created() {
	this.classMap = ['decrease', 'discount', 'special', 'invoice', 'gurantee'];
	this.$http.get('/api/goods').then((response) => {
	response = response.body;
	if (response.errno === ERR_OK) {
	this.goods = response.data;
	this.$nextTick(() => { // 计算DOM相关的时候记得调用这个函数
	this._initScroll();
	this._calculateHeight();
	});
	}
	});
	},
	methods: {
	selectMenu(index, event) {
	if (!event._constructed) { // 避免网页点击触发两遍  给它传一个事件
	return;
	}
	let foodList = this.$refs.foodList;
	let el = foodList[index]; // 拿到对应的右边的位置
	this.foodsScroll.scrollToElement(el, 300); // 设置滚动
	},
	_initScroll() {
	this.menuScroll = new BScroll(this.$refs.menuWrapper, {
	click: true
	});
	this.foodsScroll = new BScroll(this.$refs.foodsWrapper, {
	probeType: 3
	});

	this.foodsScroll.on('scroll', (pos) => {
	this.scrollY = Math.abs(Math.round(pos.y));
	});
	},
	_calculateHeight() {
	let foodList = this.$refs.foodList;
	let height = 0;
	this.listHeight.push(height);
	for (let i = 0; i < foodList.length; i++) {
	let item = foodList[i];
	height += item.clientHeight;
	this.listHeight.push(height);
	}
	}
	}
	};
</script>

<style type="text/css">
	.goods{
		display: flex;position: absolute;top: 174px;bottom: 46px;width: 100%;overflow: hidden;
	}
	.goods .menu-wrapper{
		flex:0 0 80px;width: 80px;background:#f3f5f7;
	}
	.goods .menu-wrapper .menu-item{
		display: table;height: 54px;width: 56px;line-height: 14px;padding: 0 12px;
	}
	.goods .menu-wrapper .menu-item.current{
		position: relative;z-index: 10;margin-top: -1px;background: #fff;font-weight: 700;
	}
	.goods .menu-wrapper .menu-item .text{
		display: table-cell;width: 56px;vertical-align: middle;font-size: 12px;position: relative;
	}
	.goods .menu-wrapper .menu-item .text:after{
    	position: absolute;display: block;left: 0;bottom: 0;width: 100%;border-top: 1px solid rgba(7,17,27,0.1);content: ' ';
	}
	.goods .menu-wrapper .menu-item .text .icon{
		display: inline-block;width: 12px;height: 12px;margin-right: 2px;
	}
	.goods .menu-wrapper .menu-item .text .decrease{
		background: url(decrease_3@2x.png) no-repeat; background-size: 12px 12px;
	}
	.goods .menu-wrapper .menu-item .text .discount{
		background: url(discount_3@2x.png) no-repeat; background-size: 12px 12px;
	}
	.goods .menu-wrapper .menu-item .text .gurantee{
		background: url(guarantee_3@2x.png) no-repeat; background-size: 12px 12px;
	}
	.goods .menu-wrapper .menu-item .text .invoice{
		background: url(invoice_3@2x.png) no-repeat; background-size: 12px 12px;
	}
	.goods .menu-wrapper .menu-item .text .special{
		background: url(special_3@2x.png) no-repeat; background-size: 12px 12px;
	}
	.goods .foods-wrapper{
		flex: 1;
	}
	.foods-wrapper .title{
		padding-left: 14px;height: 26px;line-height: 26px;border-left: 2px solid #d9dde1;font-size: 12px;color: rgb(147,153,159);background: #f3f5f7;
	}
	.foods-wrapper .food-item{
		display: flex;margin:18px;position: relative;padding-bottom: 18px;
	}
	.foods-wrapper .food-item:after{
		position: absolute;display: block;left: 0;bottom: 0;width: 100%;border-top: 1px solid rgba(7,17,27,0.1);content: ' ';
	}
	.foods-wrapper .food-item:last-child{
		margin-bottom: 0;
	}
	.foods-wrapper .food-item:last-child:after{
		display: none;
	}
	.foods-wrapper .food-item .icon{
		flex: 0 0 57px;margin-right: 10px;
	}
	.foods-wrapper .food-item .content{
		flex: 1;
	}
	.foods-wrapper .food-item .content .name{
		margin:2px 0 8px 0;height: 14px;line-height: 14px;font-size: 12px;color: rgb(7,17,27); 
	}
	.foods-wrapper .food-item .content .desc,.foods-wrapper .food-item .content .extra{
		font-size: 10px;color: rgb(147,153,159);
	}
	.foods-wrapper .food-item .content .desc{
		margin-bottom: 8px;line-height: 12px
	}
	.foods-wrapper .food-item .content .extra .count{
		margin-right:12px;
	}
	.foods-wrapper .food-item .content .price{
		line-height: 24px;
	}
	.foods-wrapper .food-item .content .price .now{
		margin-right: 8px;color: rgb(240,20,20);font-weight: 700;
	}
	.foods-wrapper .food-item .content .price .old{
		text-decoration: line-through;font-size: 10px;color: rgb(147,153,159);
	}
</style>