<script>
export default{
    data(){
        return{
            newTodo:'',
            todos:[]
        }
    },
    watch:{
        todos:{
            handler(){
                localStorage.todos =JSON.stringify(this.todos);
            },
            deep: true
        }
    },
    mounted(){
        if(localStorage.todos){
            this.todos = JSON.parse(localStorage.todos);
        }
    },
    methods:{
        addTodo(){
            this.todos.push({
                title: this.newTodo,
                check: false
            });
            this.newTodo='';
        },
        markDone(todo){
            todo.check = true 
        },
        DeleteTodo(index){
            this.todos.splice(index,1)
        }
    } 
}

</script>

<template>
    <div id="app" class="container">
        <h1 class="text-center">Todo App</h1>
        <form @submit.prevent="addTodo()">
            <div class="mb-3" >
                <label for="newTodo">New Todo</label>
                <input v-model="newTodo" type="text" class="form-control" id="exampleInputEmail1" aria-describedby="newTodoHelp">
                <div id="emailHelp" class="form-text">We'll never share your email with anyone else.</div>
            </div>
            <button type="submit" class="btn btn-primary">Submit</button>
        </form>
        <ul class="list-group mt-3" >
            <li class="list-group-item" v-for="(todo,i) in todos">
                <span :class="{isCheck:todo.check}">{{ todo.title }}</span>
                <button @click="markDone(todo)" v-if="!todo.check" type="button" class="btn btn-primary">done</button>
                <button @click="DeleteTodo(index)" type="button" class="btn btn-danger">Delete</button>
            </li>
        </ul>
    </div>
</template>

<style>
.isCheck{
    text-decoration: line-through;
}
li button{
    margin-left: 4px;
}
</style>
