<template>
    <div class="todo-item" v-bind:class="{'is-completed':todo.completed}">
        <input type="checkbox" v-on:change="markComplete">
        <p>{{todo.title}}</p>
        <button class="del" @click="$emit('del-todo', todo.id)">x</button>
    </div>
</template>

<style scoped>
    .todo-item {
        background: #f4f4f4;
        padding: 10px;
        border-bottom: 1px #ccc dotted;
    }

    .is-completed {
        text-decoration: line-through;
    }

    .del {
        background: red;
        border: 1px black solid;
        border-radius: 25px;
    }
</style>

<script>
export default {
    name: "TodoItems",
    props:["todo"],
    methods:{
        markComplete() {
            this.todo.completed = !this.todo.completed;
        }
    }
}
</script>