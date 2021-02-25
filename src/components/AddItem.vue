<template>
    <div>
        <form @submit="addTodo">
            <input type="text" v-model="title" >
            <input type="submit" value="Submit">
        </form>
    </div>
</template>

<style scoped>
    form{
        display: flex;
    }

    input[type="text"]{
        flex: 10;
        padding: 5px;
    }

    input[type="submit"]{
        flex: 2;
    }
</style>

<script>
import {v4 as uuiddv4} from 'uuid';
export default {
    name:"AddItem",
    data(){
        return{
            title: ''
        }
    },
    methods:{
        addTodo(e){
            e.preventDefault();

            const newTodo = {
                id: uuiddv4(),
                title: this.title,
                completed:false,
            }

            this.$emit('add-todo', newTodo);
            this.title = '';
        }
    }
}
</script>