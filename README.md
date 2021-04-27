- 云函数：处理前端请求的函数。
![](https://img-blog.csdnimg.cn/20210427164752280.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM0MjczMDU5,size_16,color_FFFFFF,t_70)
![](https://img-blog.csdnimg.cn/20210427164823676.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM0MjczMDU5,size_16,color_FFFFFF,t_70)
使用方法：
```shell
useUnicloudFunc(){
	const _this = this;
	uniCloud.callFunction({
		name:"test",
		success(res) {
			console.log(res)
			_this.title = res.result;
		}
	})
}
```

- 云数据库：存储数据,格式为json
uniapp中操作云数据库的方式：
```shell
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
```
![](https://img-blog.csdnimg.cn/20210427165224148.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM0MjczMDU5,size_16,color_FFFFFF,t_70)
![](https://img-blog.csdnimg.cn/20210427165247523.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM0MjczMDU5,size_16,color_FFFFFF,t_70)
[简单的git demo演示地址](https://github.com/smileyqp/unicloud-demo)
![](https://img-blog.csdnimg.cn/20210427171048930.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM0MjczMDU5,size_16,color_FFFFFF,t_70)
