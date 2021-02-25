<template>
  <div id="app">
    <Header />
    <AddItem v-on:add-todo="addTodo" />
    <Todos v-bind:todos = "todos" v-on:del-todo="deleteTodo" />
    <Footer />
  </div>
</template>

<script>
import Header   from '@/components/layouts/Header';
import Footer   from '@/components/layouts/Footer';
import Todos    from '@/components/Todos';
import AddItem  from '@/components/AddItem';
import axios    from 'axios';
export default {
  
  name:"App",
  components:{
      Todos,
      Header,
      Footer,
      AddItem,
  },
  data(){
    return{
      todos:[
        // static
        // {id:1,title:"title1",completed:true},
        // {id:2,title:"title2",completed:true}
      ]
    }
  },
   methods:{
    deleteTodo(id){
      // this.todos = this.todos.filter(todo => todo.id != id); 

      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then(res => this.todos = this.todos.filter(todo => todo.id != id,res))
      .catch(err => console.log(err));

    },
    addTodo(newTodo){
      // this.todos = [...this.todos,newTodo];
      const {title, completed} = newTodo;
      axios.post(`https://jsonplaceholder.typicode.com/todos/`,{title,completed})
      .then(res => this.todos = [...this.todos,res.data])
      .catch(err => console.log(err));
    }
  },
  created(){
      axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
      .then(res => this.todos = res.data)
      .catch(err => console.log(err));
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
