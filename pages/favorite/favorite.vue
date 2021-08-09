<template>
	<view class="app">
		<mescroll-body
			ref="mescrollRef" 
			@init="mescrollInit" 
			:top="0" 
			@down="downCallback" 
			:up="upOption" 
			@up="loadList" 
		>
			<product-list ref="productList" :list="list" listType="column"></product-list>
			
		</mescroll-body>
		
		<mix-loading v-if="isLoading" :type="2"></mix-loading>
	</view>
</template>

<script>
	import productList from '@/pages/product/components/product-list'
	import MescrollMixin from "@/components/mescroll-uni/mescroll-mixins.js";
	export default {
		components: {
			productList
		},
		mixins: [MescrollMixin], 
		data() {
			return {
				list: [],
				upOption:{
					auto: false, // 是否自动加载
					page: {
					 	num: 0, // 当前页码,默认0,回调之前会加1,即callback(page)会从1开始
					 	size: 6 // 每页数据的数量
					},
					noMoreSize: 6
				},
			}
		},
		methods: {
			//加载热门推荐列表
			async loadList(e){
				if(this.$refs.productList){
					this.$refs.productList.loadType = e.num === 1 ? 'refresh': 'add';
				}
				/* const res = await this.$request('favorite', 'get', {
					offset: (e.num - 1) * e.size,
					limit: e.size,
				}); */
				const res = [{
						"_id": "5f057b62bc8ac30001a63bacz",
						"product": {
							"title": "海洋之星Mini颗粒 小型犬狗粮1.5k",
							"is_sales": 1,
							"market_price": 169,
							"price": 160,
							"sales": 0,
							"rating_ratio": 75,
							"thumb": "https://vkceyugu.cdn.bspapp.com/VKCEYUGU-mix-mall-admin/bf376481-1835-4b5a-9538-865c5d133859.jpg",
							"update_time": 1595649433489,
							"cate_name": "海洋之星猫/狗粮",
							"collection_num": 0,
							"content": "<p><img src=\"https://vkceyugu.cdn.bspapp.com/VKCEYUGU-mix-mall-admin/d19e2118-dba8-4479-a9eb-26a1dce285e7.jpg\" alt=\"\" /></p>\n<p><img src=\"https://vkceyugu.cdn.bspapp.com/VKCEYUGU-mix-mall-admin/432ff560-0ea5-403b-9aab-ccf54358e4b6.jpg\" alt=\"\" width=\"790\" height=\"902\" /></p>\n<p><img src=\"https://vkceyugu.cdn.bspapp.com/VKCEYUGU-mix-mall-admin/ddd92a4a-fd4e-4dbb-85ce-b09167ced01d.jpg\" alt=\"\" width=\"790\" height=\"913\" /></p>\n<p><img src=\"https://vkceyugu.cdn.bspapp.com/VKCEYUGU-mix-mall-admin/bbc187eb-7f9e-4a48-9356-9f36a99d9c24.jpg\" alt=\"\" width=\"790\" height=\"1348\" /></p>",
							"first_cate_id": "5f052145c76e2d00015f2ab9z",
							"sku": [{
								"image": "",
								"market_price": 0,
								"name": "6个月以上",
								"price": 160,
								"product_id": "5f057b62bc8ac30001a63bacz",
								"stock": 999,
								"_id": "f47f682c5f1a5fde0076256011ea6efc"
							}, {
								"market_price": 0,
								"name": "临期特价",
								"price": 128,
								"product_id": "5f057b62bc8ac30001a63bacz",
								"stock": 31,
								"_id": "f47f682c5f1a5fde007625614e7fb488",
								"image": ""
							}],
							"status": 1,
							"add_time": 1594194786201,
							"is_hot": 0,
							"look_num": 5,
							"skuData": {
								"attrList": [{
									"name": "6个月以上",
									"parent": "保质期"
								}, {
									"name": "临期特价",
									"parent": "保质期"
								}]
							},
							"stock": 1030,
							"cate_id": "5f052ff004c20400012a96ddz",
							"first_cate_name": "宠物用品",
							"images": ["https://vkceyugu.cdn.bspapp.com/VKCEYUGU-mix-mall-admin/51428abb-1afe-4b14-8b9a-3974890c1acf.jpg",
								"https://vkceyugu.cdn.bspapp.com/VKCEYUGU-mix-mall-admin/feadadb8-aebc-43f5-853a-e2101e35ce63.jpg",
								"https://vkceyugu.cdn.bspapp.com/VKCEYUGU-mix-mall-admin/c8c75c65-bbf0-4003-b236-0134c22ea3a8.jpg",
								"https://vkceyugu.cdn.bspapp.com/VKCEYUGU-mix-mall-admin/9f2c0e08-7c10-408a-b824-5d9683c6fd42.jpg"
							],
							"is_del": 0,
							"loaded": true
						}
					}]
				const curList = res.map(item=> {
					return {
						fav_id: item._id,
						...item.product
					}
				})
				if(e.num === 1){
					this.list = [];
					this.loaded && curList.forEach(item=> {item.loaded = true;})
				}
				//wwl add
				this.isLoading = false;
				//wwl end
				this.list = this.list.concat(curList); //追加新数据
				this.mescroll.endSuccess(curList.length); //结束加载状态
			},
			mescrollInit(mescroll){
				this.isLoading = true;
				this.mescroll = mescroll;
				this.mescroll.resetUpScroll(false)
			}
		}
	}
</script>

<style>
	page{
		background-color: #f8f8f8;
	}
</style>
<style scoped lang="scss">
	.app{
		padding-top: 20rpx;
		padding-bottom: 20rpx;
	}
</style>
