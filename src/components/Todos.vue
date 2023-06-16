<template>
  <div>
    <h3>Todos</h3>

    <div class="legend">
      <span>Double Click to mark as complete</span>
      <span>
        <span class="incomplete-box"></span> = Incomplete
      </span>
      <span>
        <span class="complete-box"> </span> = Complete
      </span>
    </div>

    <div class="todos">
      <div @dblclick.native="onDblClick(todo)"  :class="{'is-complete':todo.completed}" v-for="todo in allTodos" :key="todo.id" class="todo">
      {{ todo.title  }}
        <i @click="deleteTodo(todo.id)" class="fas fa-trash"></i>
        
    </div>
    </div>
  </div>
</template>

<script>

import { mapGetters , mapActions} from 'vuex';

export default {
  name: "Todos",
  computed:mapGetters(['allTodos']),
  methods:{
    ...mapActions(['fetchTodos','deleteTodo','updateTodos']),
    onDblClick(todo){
      const updTodo = {
        id: todo.id,
        title: todo.title,
        completed: !todo.completed
      }
      this.updateTodos(updTodo)
    }
  },
  created(){
    this.fetchTodos()
  }

};


</script>

<style scoped>

/* Styling Complete and incomplete todo */
.legend {
  display: flex;
  justify-content: space-around;
  margin-bottom: 1rem;
}

.complete-box ,
.incomplete-box{
  display: inline-block;
  width: 10px;
  height: 10px;

}
.complete-box{
  background: #35495e;
}

.incomplete-box {
  background: #41b883;
}


.is-complete {
  background: #35495e !important;
  color: #fff;
}

@media (max-width: 500px) {
  .todos {
    grid-template-columns: 1fr !important;
  }
  .legend{
    flex-direction: column !important;
  }
}

.todos{
  display: grid;
  grid-template-columns: repeat(3,1fr);
  grid-gap: 1rem;
}

.todo {
  border: 1px solid #ccc;
  background: #41b883;
  padding: 1rem;
  border-radius: 5px;
  text-align: center;
  position: relative;
  cursor: pointer;
}

i {
  position: absolute;
  bottom: 10px;
  right: 10px;
  color: #fff;
  cursor: pointer;
}

</style>
