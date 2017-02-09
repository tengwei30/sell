<template>
	<div class="shopcart">
		<div class="content">
			<div class="content-left">
				<div class="logo-wrappper">
					<div class="logo">
						<span class="icon-shopping_cart">购物车</span>
					</div>
				</div>
				<div class="price">
					
				</div>
				<div class="desc">
					
				</div>
			</div>
			<div class="content-right"></div>
		</div>
	</div>
</template>
<script type="text/javascript">
	export default {};
</script>
<style type="text/css">
	.shopcart{
		position: fixed;left: 0;bottom: 0;z-index: 50;width: 100%;height: 48px;
	}
	.shopcart .content{
		display: flex;background: #141d27;
	}
	.shopcart .content .content-left{
		flex: 1;
	}
	.shopcart .content .content-left .logo-wrapper{
		display: inline-block;position: relative;top: -10px;margin:0 12px;padding: 6px;width: 56px;height: 56px;box-sizing: border-box;vertical-align: top;border-radius: 50%;background: #141d27;
	}
	.shopcart .content .content-left .logo-wrapper .logo{
		width: 100%;height: 100%;border-radius: 50%;text-align: center;background: rgba(0,0,0,0.2);
	}
	.content .content-left .logo-wrapper .logo .icon-shopping_cart{
		font-size: 24px;line-height: 24px;color: #80858a;
	}
	.shopcart .content .content-left .price{
		display: inline-block;
	}
	.shopcart .content .content-left .desc{
		display: inline-block;
	}
	.shopcart .content .content-right{
		flex: 0 0 105px;width: 105px;
	}
</style>
