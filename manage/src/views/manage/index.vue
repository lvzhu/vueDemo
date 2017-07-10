<template>
	<div class="manage tc">
		<button class="add" @click="add">新增</button>
		<div class="input-area" v-show="showAdd">
			<input type="text" placeholder="请输入人员姓名" v-model="nameValue"/>
			<button class="submit" @click="addName">确定</button>
		</div>
		<table class="table-block">
			<tr>
				<th width="200px">姓名</th>
				<th width="200px">操作</th>
			</tr>
			<tr v-for="(item,index) in people">
				<td>{{item.name}}</td>
				<td :id="index"><span @click="edit">编辑</span><span @click="deletName">删除</span></td>
			</tr>
		</table>
		<div class="wrap" v-show="showEdit">
			<div class="content">
				<input type="text" placeholder="请输入姓名" v-model="newName"></br>
				<button @click="cancel">取消</button>
				<button @click="editName">确定</button>
			</div>
		</div>
		<footer-nav v-bind:class="{'isManage':isCurrPage}"></footer-nav>
	</div>
</template>
<style scoped>
	.add{padding: 6px 50px;background-color: #41b883;color: #fff;border: none;cursor: pointer;border-radius: 3px;}
	.input-area{margin: 10px auto;}
	.input-area input{padding-left:6px;width: 200px;line-height: 30px;border: 1px solid #eee;outline: none;}
	.table-block {margin: 0 auto;}
	.table-block span{display: inline-block;margin-right: 10px; padding: 2px 4px;border: 1px solid #ddd;cursor: pointer;}
	.submit{padding: 8px 16px;background-color: #41b883;color: #fff;border: none;cursor: pointer;border-radius: 3px;}
	.wrap {box-sizing: border-box; position: absolute;top: 0;left: 0;background: #000;opacity: .8;width: 100%;height: 100%;
    vertical-align: middle;padding-top: 20%;}
    .content input{padding-left: 16px;margin-bottom: 14px; width: 240px;height: 35px;line-height: 35px;border: 0;background: #fff;color: #000;}
    .content button{padding: 6px 14px;background: #42b983;color: #fff;font-size: 14px;border: none;margin:0 10px;cursor: pointer;}
</style>
<script>
	import FooterNav from '../../components/footer.vue'
	export default{
		components:{
			FooterNav
		},
		data(){
			return{
				isCurrPage:true,
				showAdd:false,
				people:[{'name':'Jack'},{'name':'Joe'}],
				nameValue:'',
				showEdit:false
			}
		},
		methods:{
			add: function(){
			this.showAdd=true	
			},
			addName: function(){
				if(this.nameValue){
					var data={}
					data.name=this.nameValue
					this.people.push(data)
				}else{
					alert("请输入姓名")
				}
			},
			deletName: function(e){
				var _self=this
				var v=e.currentTarget.offsetParent.id
				_self.people.splice(v,1)
				
				
			},
			//编辑
			edit:function(e){
				var _self=this
				var id=e.target.offsetParent.id
				_self.showEdit=true
				_self.editId=id
				_self.newName=this.people[id].name
				
			},
			cancel(){
				this.showEdit=false
			},
			editName(){
				var v=this.newName
				if(v.trim()==""){
					alert("请输入姓名")
				}else{
					this.people[this.editId].name=this.newName
					this.showEdit=false
				}
			}
		}
	}
</script>