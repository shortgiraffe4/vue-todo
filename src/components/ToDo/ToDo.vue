<template>
  <div class='todo-container'>
    <ToDoPug />
    <div class='todo'>
      <h1 class='todo__header'>Vue ToDo</h1>
      <div class='todo__container'>
        <div class='todo__content'>
          <ToDoItem v-for='todo in list' :todo='todo' @delete='onDeleteItem' :key='todo.id' />
        </div>
        <form class='todo__form'>
          <input type='text' v-model='todo' v-on:keyup.enter='createNewToDoItem'>
          <input type="submit" class='todo__add' value='+' @click="createNewToDoItem"/>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import ToDoItem from './ToDoItem';
import ToDoPug from './ToDoPug';

export default {
  name: 'to-do',
  components: {
    ToDoItem,
    ToDoPug,
  },
  data() {
    return {
      list: [
        {
          id: 1,
          text: 'create vue todo',
        },
        {
          id: 2,
          text: 'create react todo',
        },
      ],
      todo: '',
    };
  },
  methods: {
    createNewToDoItem() {
      if (!this.todo) {
        // eslint-disable-next-line
        alert('Please enter a todo!');
        return;
      }
      const newId = Math.max.apply(null, this.list.map(t => t.id)) + 1;
      this.list.push({ id: newId, text: this.todo });
      this.todo = '';
    },
    onDeleteItem(todo) {
      this.list = this.list.filter(item => item !== todo);
    },
  },
};
</script>

// 'scoped' -> only applied to this file
<style lang="scss" scoped>
  @import '../../styles/_colors';

  .todo {
    display: block;

    &__add {
      color: $main;
      font-size: 18px;
    }
  }

</style>

