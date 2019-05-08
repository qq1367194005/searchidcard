<template>
	<view>
		<cu-custom bgColor="bg-gradual-blue" :isBack="false">
			<block slot="backText">返回</block>
			<block slot="content">查询信息</block>
		</cu-custom>
		<view class="cu-bar bg-white search fixed" :style="[{top:CustomBar + 'px'}]">
			<view class="search-form round">
				<text class="cuIcon-search"></text>
				<input type="text" placeholder="请输入身份证号码" confirm-type="search"></input>
			</view>
			<view class="action">
				<button class="cu-btn bg-gradual-green shadow-blur round">搜索</button>
			</view>
		</view>
		<scroll-view scroll-y class="indexes" :scroll-into-view="'indexes-'+ listCurID" :style="[{height:'calc(100vh - '+ CustomBar + 'px - 50px)'}]"
		 :scroll-with-animation="true" :enable-back-to-top="true">
			<view v-for="(item,index) in userlist" class="fixed">
				<view class="cu-bar bg-white solid-bottom ">
					<view class="action" >
						<text class="cuIcon-titles text-orange"></text> {{item.SKFMC}}
					</view>
					<view class="action">
						<switch :class="item.isCard?'checked':''" :checked="item.isCard?true:false" @change="IsCard(index)"></switch>
					</view>
					
				</view>
				<view style="display:none" class="cu-card case no-card" :class="item.isCard?'show':''">
					<form>
						<view class="cu-form-group">
							<view class="title">发票号码</view>
							<input disabled :placeholder="item.FP" name="input"></input>
						</view>
						<view class="cu-form-group">
							<view class="title">姓名</view>
							<input disabled :placeholder="item.SKFMC" name="input"></input>
						</view>
						<view class="cu-form-group">
							<view class="title">身份证号</view>
							<input disabled :placeholder="item.SKFSBH" name="input"></input>
						</view>
						<view class="cu-form-group">
							<view class="title">代开网点</view>
							<input disabled :placeholder="item['BRCH_NAME']" name="input"></input>
						</view>
					</form>
				</view>
			</view>
		</scroll-view>
		
		<!--选择显示-->
		<view v-show="!hidden" class="indexToast">
			{{listCur}}
		</view>
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
						isCard:false,
						FP:'14206195300200090802',
						SKFMC:'沈小平',
						SKFSBH:'420683196610093144',
						'BRCH_NAME':'枣阳县鹿头支局'
					},
					{
						isCard:false,
						FP:'14207195300200013354',
						SKFMC:'张远团',
						SKFSBH:'420700197011137079',
						'BRCH_NAME':'鄂州市沼山邮政支局'
					}
				]
			};
		},
		onLoad() {
			
		},
		onReady() {
			
		},
		methods: {
			IsCard(e) {
				// this.isCard = e.detail.value
				console.log(e);
				this.userlist[e].isCard = !this.userlist[e].isCard;
			}
		}
	}
</script>

<style>
	page {
		padding-top: 100upx;
	}

	.indexes {
		position: relative;
	}

	.indexBar {
		position: fixed;
		right: 0px;
		bottom: 0px;
		padding: 20upx 20upx 20upx 60upx;
		display: flex;
		align-items: center;
	}

	.indexBar .indexBar-box {
		width: 40upx;
		height: auto;
		background: #fff;
		display: flex;
		flex-direction: column;
		box-shadow: 0 0 20upx rgba(0, 0, 0, 0.1);
		border-radius: 10upx;
	}

	.indexBar-item {
		flex: 1;
		width: 40upx;
		height: 40upx;
		display: flex;
		align-items: center;
		justify-content: center;
		font-size: 24upx;
		color: #888;
	}

	movable-view.indexBar-item {
		width: 40upx;
		height: 40upx;
		z-index: 9;
		position: relative;
	}

	movable-view.indexBar-item::before {
		content: "";
		display: block;
		position: absolute;
		left: 0;
		top: 10upx;
		height: 20upx;
		width: 4upx;
		background-color: #f37b1d;
	}

	.indexToast {
		position: fixed;
		top: 0;
		right: 80upx;
		bottom: 0;
		background: rgba(0, 0, 0, 0.5);
		width: 100upx;
		height: 100upx;
		border-radius: 10upx;
		margin: auto;
		color: #fff;
		line-height: 100upx;
		text-align: center;
		font-size: 48upx;
	}
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
