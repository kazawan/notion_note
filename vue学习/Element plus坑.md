# Element plus坑

### 样式动态设置

```jsx
<el-button ref="sendbtn" :type="color"  @click="addList"   
						:round="isround" 
						:circle="iscircle" 
						:loading="isloading">
```

```jsx
data(){
	return{
		isround:false,
		isloading:false,
		iscircle:false,
}
```

然后可以用this.isround改变数据  等于使用了v-bind

### el-row样式居中

style="margin-top:8px;text-align: -webkit-center;

```jsx
<el-row :gutter="20" style="margin-top:8px;text-align: -webkit-center;" >
```

col垂直居中

```jsx
style="position: relative; top:50%;transform: translateY(-50%);"
```

### 去掉输入框的边框

[element el-input 去掉边框_Hero_rong的博客-CSDN博客_el-input去除边框](http://t.csdn.cn/ek95G)