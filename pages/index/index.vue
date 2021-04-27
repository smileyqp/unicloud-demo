<template>
	<view class="content">
		<image class="logo" src="/static/logo.png"></image>
		<view class="text-area">
			<text class="title">{{title}}</text>
		</view>
		<unicloud-db ref="udb" v-slot:default="{data, loading, error, options}" collection="contacts" >
			<view v-if="error">{{error.message}}</view>
			<view v-else>
				{{data}}
				<uni-list>
					<uni-list-item @click.native="update(item._id)" @longpress.native="rmItem(item._id)" v-for="item in data" :key="item._id" :title="item.name" :note="item.tel" link></uni-list-item>
				</uni-list>
		  </view>
		</unicloud-db>
		<view>
			<uni-easyinput v-model="item.name" placeholder="name"/>
			<uni-easyinput v-model="item.tel" placeholder="tel"/>		
			<button @click="confirmSubmit">提交</button>
			
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello',
				item:{
					name:'',
					tel:''
				}
			}
		},
		onLoad() {
			const _this = this;
			uniCloud.callFunction({
				name:"test",
				success(res) {
					console.log(res)
					_this.title = res.result;
				}
			})
		},
		methods: {
			//删除联系人
			rmItem(id){
				console.log(id)
				this.$refs.udb.remove(id)
			},
			//添加联系人
			confirmSubmit(){
				const db = uniCloud.database()
				db.collection("contacts").add(this.item).then((res)=>{
					console.log(res)
				})
			},
			//更新联系人
			update(id){
				const db = uniCloud.database()
				// delete id
				db.collection("contacts").doc(id).update({name:'测试',tel:'287623478'}).then((res)=>{
					console.log(res)
				})
			}
		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
</style>
