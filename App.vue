<template>
  <view class="container">
   <statusbar color="#4B8B3B"/>
   <header title="Todo App"/>
   <view class="inputContainer">
   	<text-input class="input" v-model="newTodoText"/>
   	<touchable-opacity class="add-btn" :on-press="newTodo"
        >
   <text class="btn-text">Add</text>
   </touchable-opacity>
      
   </view>
   <view class="todo" v-for="todo in todos" :key="todo.id">
   	<touchable-opacity  :on-press="()=>toggleDone(todo.id)">
   	<text class="todotext done" v-if="todo.completed">
   	{{todo.title}}</text>
   	<text class="todo-text" v-else>
   	{{todo.title}}</text>
   </touchable-opacity>
   <touchable-opacity class="remove-btn" :on-press="()=>removeTodo(todo.id)">
   <text class="remove-btn-text">Remove</text>
  </touchable-opacity>
   </view>
  </view>

</template>

<script >
import statusbar from './components/statusbar.vue';
import header from './components/header.vue';
export default{
		data(){
			return{
				newTodoText:'',
				todos:[{
					id:1,
					title:'Trim Fence',
					completed:false
				},
				{
					id:2,
					title:'Repair Electricity',
					completed:false
				}
				]
			}
		},
		components:{
			statusbar,
			header
		},
		methods:{
			newTodo(){
				this.todos.push({
					id:this.todos.length+1,
					title:this.newTodoText,
					completed:false
				});
				this.newTodoText=''
			},
			toggleDone(id){
				this.todos=this.todos.map(todo=>{
					if(todo.id==id) todo.done  !=todo.done;
					return todo;
				})
			},
			removeTodo(id){
				this.todos=this.todos.filter(todo=>todo.id !==id);
			}
		},
	}
</script>


<style>
.container {
  background-color: white;
  align-items: center;
  justify-content: center;
  flex: 1;
}
.inputContainer{
	width:100%;
	flex-direction:row;
	justify-content:center;
	align-items:stretch;
}
.input{
  flex:1;
  height:35px;
  background-color: #F3F3F3;
  font-size:18px;
  color: #888888;

}
.add-btn{
	width:100px;
	height:35px;
	background-color: #FFCE00;
	justify-content: center;
	align-items:center;
}
.btn-text{
	font-size:18px;
	font-weight:700;

}
.todo{
	flex-direction:row;
	justify-content: space-between;
	padding:15px;
	background-color: #FFFFFF
}
.todo-text{
	font-size:18px;

}
.done{
	color: #AAAAAA;
}
.remove-btn-text{
	font-size:18px;
	color:red;
}
</style>