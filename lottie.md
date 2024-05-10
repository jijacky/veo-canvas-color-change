

### 演示地址 [https://static-04713dad-0088-4598-9c43-be27d990a230.bspapp.com](https://static-04713dad-0088-4598-9c43-be27d990a230.bspapp.com)
### node环境安装vue-lottie
``` 
npm install --save vue-lottie
```	
### 插件使用
```	
	<ccq-lottie ref="praise" type="praise" :autoplay="false" @click="playAni"  />
	<ccq-lottie ref="goto" type="goto" :loop="true" @click="stopAni"  />
```	
``` 
	import Lottie from '@/components/lottie/lottie.vue';
	export default {
		components: {
			'lottie': Lottie
		},
		methods: {
			// 开始动画
			playAni(i) {
				 this.$refs['praise'].play();
			},
			// 停止动画
			stopAni() {
				 this.$refs['goto'].stop();
			}
		}
	}
```

--------------------------------------------------

## API 
|	属性名	|	类型	|	默认值	|	说明	|
|--	|--	|--	|--	|
|	type	|	String	|	''	|	动画名称（必填）	|
|	autoplay	|	Boolean	|	true	|	自动播放动画	|
|	loop	|	Boolean	|	false	|	是否循环播放	|
|	width	|	Number,String	|	125	|	 尺寸(宽度)px	|
|	height	|	Number,String	|	125	|	 尺寸(高度)px	|

## Events
|	事件名称	|	说明	|	返回值	|
|--	|--	|--	|
|	click	|  点击事件	|	无	|
|	this.$refs['refName'].play();	|	点击开始动画	|	无	|
|	this.$refs['refName'].stop();	|	点击暂停动画	|	无	|

## 意见建议联系
> - QQ: 1252620858  (小前端，请多多指教~)

