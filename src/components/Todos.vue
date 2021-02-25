<template>
    <div>
        <div v-for="todo in todos" v-bind:key="todo">
            <TodoItems v-bind:todo = "todo" v-on:del-todo="$emit('del-todo',todo.id)"/>
        </div>
    </div>
</template>

<style scoped>

</style>

<script>
import TodoItems from '@/components/TodoItems';

export default {
    name:"Todos",
    components:{
        TodoItems
    },
    props: ["todos"],
}
</script>