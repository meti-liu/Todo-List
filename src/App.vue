<template>
    <div class="app-container">
        <el-card class="todo-card">
            <template #header>
                <div class="card-header">
                    <h2>Todo List</h2>
                </div>
            </template>
        
            <div class="input-section">
                <el-input
                    v-model="newTodoText"
                    placeholder="Add a new todo"
                    @keyup.enter="addTodo"
                    clearable
                >
                </el-input>
                <el-button type="primary" @click="addTodo">Add</el-button>
            </div>

            <div class="list-section">
            
                <div v-for="todo in todos" :key="todo.id" class="todo-item">
                    {{ todo.text }}
                </div>
            </div>

            <p v-if="todos.length===0">暂无任务</p>

        </el-card>
        
    </div>

</template>

<script setup>

import { ref } from "vue";//ref是用来创建响应式数据的
const newTodoText = ref("");//newTodoText是一个字符串，存放输入框的内容
const todos = ref([]);//todos是一个数组，存放多个todo对象

const addTodo=()=>
{
    if(newTodoText.value.trim()!=="")//trim()去掉字符串前后的空格
    {
        todos.value.push
        ({
            id:Date.now(),//Date.now()返回当前时间的时间戳，作为id
            text:newTodoText.value.trim(),
            completed:false//completed表示是否完成，默认是false
        });
        newTodoText.value="";//添加完后清空输入框
    }
}


const removeTodo=(id)=>
{
    todos.value=todos.value.filter(todo=>todo.id!==id);//filter()返回一个新数组，包含所有不符合条件的元素
}
</script>

<style>

</style>