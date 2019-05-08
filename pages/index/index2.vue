<template>
	<view class="content">
		<cu-custom bgColor="bg-gradual-blue" :isBack="false">
			<block slot="backText">返回</block>
			<block slot="content">查询信息</block>
		</cu-custom>
		<view class="cu-bar bg-white search fixed" :style="[{top:CustomBar + 'px'}]">
			<view class="search-form round">
				<text class="cuIcon-search"></text>
				<input type="text" placeholder="输入搜索的关键词" confirm-type="search"></input>
			</view>
			<view class="action">
				<button class="cu-btn bg-gradual-green shadow-blur round">搜索</button>
			</view>
		</view>
		<scroll-view scroll-y class="indexes" :scroll-into-view="'indexes-'+ listCurID" :scroll-with-animation="true" :enable-back-to-top="true">
			<view v-for="(item,index) in userlist" class="fixed">
				<view class="cu-bar bg-white solid-bottom ">
					<view class="action" >
						<text class="cuIcon-titles text-orange"></text> {{item.name}}
					</view>
					<view class="action">
						<switch :class="item.isCard?'checked':''" :checked="item.isCard?true:false" @change="IsCard(index)"></switch>
					</view>
					
				</view>
				<view style="display:none" class="cu-card case no-card" :class="item.isCard?'show':''">
					<form>
						<view class="cu-form-group">
							<view class="title">邮件</view>
							<input disabled placeholder="两字短标题" name="input"></input>
						</view>
						<view class="cu-form-group">
							<view class="title">输入框</view>
							<input disabled placeholder="三字标题" name="input"></input>
						</view>
						<view class="cu-form-group">
							<view class="title">收货地址</view>
							<input disabled placeholder="统一标题的宽度" name="input"></input>
						</view>
						<view class="cu-form-group">
							<view class="title">收货地址</view>
							<input disabled placeholder="输入框带个图标" name="input"></input>
						</view>
					</form>
				</view>
			</view>
		</scroll-view>
	</view>
	
</template>

<script>
	export default {
		data() {
			return {
				StatusBar: this.StatusBar,
				CustomBar: this.CustomBar,
				hidden: true,
				listCurID: '',
				list: [],
				listCur: '',
				userlist:[
					{
						name:'用户1',
						isCard:false
					},
					{
						name:'用户2',
						isCard:false
					}
				]
			};
		},
		methods: {
			IsCard(e) {
				console.log(e);
				this.userlist[e].isCard = !this.userlist[e].isCard;
			},
		}
	}
</script>

<style>
	.cu-form-group .title {
		min-width: calc(4em + 15px);
	}
	.show{
		display:block!important;
		border-bottom: 1px solid #eee;
		background: #f2f2f2;
	}
	.cu-form-group+.cu-form-group{
		border: 0px solid;
	}
	.indexes {
		position: relative;
	}
</style>
