<template>
	<div class="header">
		<div class="content-wrapper">
			<div class="avatar">
				<img :src="seller.avatar" width="64" height="64">
			</div>
			<div class="content">
				<div class="title">
					<span class="brand"></span>
					<span class="name">{{ seller.name }}</span>
				</div>
				<div class="description">
					{{ seller.description }}/{{ seller.deliveryTime }}分钟送达
				</div>
				<div v-if="seller.supports" class="supports" @click="showDetail">
					<span class="icon" :class="classMap[seller.supports[0].type]"></span>
					<span class="text">{{ seller.supports[0].description }}</span>
				</div>
			</div>
			<div v-if="seller.supports" class="support-count">
				<span class="count">{{ seller.supports.length }}个</span>
				<i class="icon-keyboard_arrow_right"> &gt; </i>
			</div>
		</div>
		<div class="bulletin-wrapper">
			<span class="bulletin-title"></span><span class="bulletin-text"> {{ seller.bulletin }} </span>
			<i class="icon-keyboard_arrow_right"> &gt; </i>
		</div>
		<div class="background">
			<img :src="seller.avatar" width="100%" height="100%">
		</div>
		<div v-show="detailShow" class="detail"  name="fade">
			<div class="detail-wrapper clearfix">
				<div class="detail-main">
					<h1 class="name">{{ seller.name }}</h1>
					<div class="star-wrapper">
						<star :size="48" :score="seller.score"></star>
					</div>
					<div class="title">
						<div class="line"></div>
						<div class="text">优惠信息</div>
						<div class="line"></div>
					</div>
					<ul v-if="seller.supports" class="supports">
						<li class="support-item" v-for="(item,index) in seller.supports">
							<span class="icon" :class="classMap[index]"></span>
							<span class="text">{{ seller.supports[index].description }}</span>
						</li>
					</ul>
					<div class="title">
						<div class="line"></div>
						<div class="text">商家公告</div>
						<div class="line"></div>
					</div>
					<div class="bulletin">
						<p class="content">{{ seller.bulletin }}</p>
					</div>
				</div>
			</div>
			<div class="detail-close" @click="hideDetail">x</div>
		</div>
	</div>
</template>

<script>
	import star from 'components/star/star';
	export default {
	props: {
	seller: {
	type: Object
	}
	},
	data() {
	return {
	detailShow: false
	};
	},
	methods: {
	showDetail() {
	this.detailShow = true;
	},
	hideDetail() {
	this.detailShow = false;
	}
	},
	created() {
	this.classMap = ['decrease', 'discount', 'special', 'invoice', 'gurantee'];
	},
	components: {
	star
	}
	};
	
</script>
<style type="text/css">
	body,html{

	}
	.header{
		color: #fff;position: relative;background: rgba(7,17,27,0.5);overflow: hidden;
	}
	.header .content-wrapper{
		padding: 24px 12px 18px 24px;font-size: 0; /* 消除图片和文字之间的空白空隙 */
		position: relative;
	}
	.header .content-wrapper .avatar{
		display: inline-block;
	}
	.header .content-wrapper .avatar img{
		border-radius: 2px;
	}
	.header .content-wrapper .content{
		display: inline-block;font-size: 14px;margin-left: 16px;
	}
	.header .content-wrapper .content .title{
		margin:2px 0 8px 0; 
	}
	.header .content-wrapper .content .title .brand{
		display: inline-block;width: 30px;height: 18px;vertical-align: top;
	}
	@media (-webkit-min-device-pixel-ratio: 3),(min-device-pixel-ratio: 3){
		.header .content-wrapper .content .title .brand{
			background: url(brand@3x.png) no-repeat;background-size:30px 18px; 
		}
	}
	@media (-webkit-min-device-pixel-ratio: 2),(min-device-pixel-ratio: 2){
		.header .content-wrapper .content .title .brand{
			background: url(brand@2x.png) no-repeat;background-size:30px 18px; 
		}
	}
	.header .content-wrapper .content .title .name{
		margin-left: 6px;font-size: 16px;line-height: 18px;font-weight: bold;
	}

	.header .content-wrapper .content .description{
		margin-bottom:10px;line-height: 12px;font-size: 12px; 
	}
	.header .content-wrapper .content .support .icon{
		display: inline-block;width: 12px;height: 12px;margin-right: 4px;
	}
/*	.header .content-wrapper .content .support .decrease{
		background: url(decrease_1@2x.png) no-repeat; background-size: 12px;
	}
	.header .content-wrapper .content .support .discount{
		background: url(discount_1@2x.png) no-repeat; background-size: 12px;
	}
	.header .content-wrapper .content .support .gurantee{
		background: url(gurantee_1@2x.png) no-repeat; background-size: 12px;
	}
	.header .content-wrapper .content .support .invoice{
		background: url(invoice_1@2x.png) no-repeat; background-size: 12px;
	}
	.header .content-wrapper .content .support .special{
		background: url(special_1@2x.png) no-repeat; background-size: 12px;
	}*/
	.header .content-wrapper .content .supports .text{
		line-height: 12px;font-size: 10px;
	}
	.support-count{
		position: absolute;right: 12px;bottom: 18px;padding: 0 8px;line-height: 24px;border-radius: 14px;
		background: rgba(0,0,0,0.2);text-align: center;
	}
	.support-count .count{
		vertical-align: top;
		font-size: 10px;
	}
	.support-count .icon-keyboard_arrow_right{
		font-size: 10px;margin-left:2px; line-height: 24px;
	}

	.bulletin-wrapper{
		height: 28px;line-height: 28px;padding: 0 22px 0 12px; white-space: nowrap;overflow: hidden;text-overflow: ellipsis;
		background: rgba(7,17,27,0.2)
	}
	.bulletin-title{
		display: inline-block;width: 22px;height: 12px;background: url(bulletin@2x.png) no-repeat;background-size:22px 12px;vertical-align: top;margin-top: 8px;
	}
	@media (-webkit-min-device-pixel-ratio: 3),(min-device-pixel-ratio: 3){
		.bulletin-title{
			display: inline-block;width: 22px;height: 12px;background: url(bulletin@3x.png) no-repeat;background-size:22px 12px;vertical-align: top;margin-top: 8px;
		}
	}
	.bulletin-text{
		font-size: 10px;,margin:0 4px;vertical-align: top;
	}
	.header .background{
		position: absolute;top: 0;left: 0;width: 100%;height: 100%; z-index: -1;filter: blur(10px);
	}
	.header .detail{
		position: fixed;top:0;left:0;z-index: 100;width: 100%;height: 100%;overflow: auto;background:rgba(7,17,27,0.8);backdrop-filter:blur(10px);
	}
	.header .detail.fade-enter-active,.header .detail.fade-leave-active {
		transition: opacity .5s;
	}
	.header .detail.fade-enter,.header .detail.fade-leave-active {
		opacity: 0;
	}
	.clearfix{
		display: inline-block;
	}
	.clearfix:after{
		display: block;content: '';height: 0;line-height: 0;clear: both;visibility: hidden;
	}

	.detail .detail-wrapper{
		min-height: 100%;width: 100%;
	}
	.detail .detail-wrapper .detail-main{
		margin-top:64px;padding-bottom: 64px;
	}
	.detail .detail-wrapper .detail-main .name{
		line-height: 16px;text-align: center;font-size: 16px;font-weight: 700;
	}
	.detail .detail-wrapper .detail-main .star-wrapper{
		margin-top: 18px;padding: 2px 0;text-align: center;
	}
	.detail .detail-wrapper .detail-main .title{
		width: 80%;margin:30px auto;display: flex; 
	}
	.detail .detail-wrapper .detail-main .title .line{
		flex: 1;position: relative;top: -6px;border-bottom: 1px solid rgba(255,255,255,0.2);
	}
	.detail .detail-wrapper .detail-main .title .text{
		padding: 0 5px;font-size: 14px;font-weight: 700;
	}
	.detail .detail-wrapper .detail-main .supports{
		width: 80%;margin:0 auto; 
	}
	.detail .detail-wrapper .detail-main .supports .support-item{
		padding: 0 12px;margin-bottom: 12px;font-size:0;
	}
	.detail .detail-wrapper .detail-main .supports .support-item:last-child{
		margin-bottom: 0;
	}
	.detail .detail-wrapper .detail-main .supports .support-item .icon{
		display: inline-block;width: 16px;height: 16px;vertical-align: top;margin-right: 6px;
	}
	.detail .detail-wrapper .detail-main .supports .support-item .icon.decrease{
		background:url(decrease_2@2x.png) no-repeat; background-size: 16px 16px; 
	}
	.detail .detail-wrapper .detail-main .supports .support-item .icon.discount{
		background:url(discount_2@2x.png) no-repeat; background-size: 16px 16px; 
	}
	.detail .detail-wrapper .detail-main .supports .support-item .icon.gurantee{
		background:url(guarantee_2@2x.png) no-repeat; background-size: 16px 16px; 
	}
	.detail .detail-wrapper .detail-main .supports .support-item .icon.invoice{
		background:url(invoice_2@2x.png) no-repeat; background-size: 16px 16px; 
	}
	.detail .detail-wrapper .detail-main .supports .support-item .icon.special{
		background:url(special_2@2x.png) no-repeat; background-size: 16px 16px; 
	}
	.detail .detail-wrapper .detail-main .supports .support-item .text{
		line-height: 16px;font-size: 12px;
	}
	.detail .detail-wrapper .detail-main .bulletin{
		width: 80%;margin: 0 auto;
	}
	.detail .detail-wrapper .detail-main .bulletin .content{
		padding: 0 12px;line-height: 24px;font-size: 12px;
	}
	.detail .detail-close{
		position: relative;width: 32px;height: 32px;margin:-64px auto;clear: both;font-size: 32px; 
	}

</style>