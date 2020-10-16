<template>
  <div>
    <addItemForm
      v-on:enterTask="addTaskToList"
    />
    <h2>Todo List</h2>
    <ul>
      <todoitem
        v-for="item in items"
        :key="item.id"
        :item="item"
        :state="item.state"
        @deleteTask="deleteTask"
        @changeState="changeItemState"
        @editTask="editTaskTitle"
      />
    </ul>
  </div>
</template>

<script>
import todoitem from './todoitem.vue';
import addItemForm from './addItemForm.vue';

export default {
  name: 'todolist',
  components: {
    todoitem,
    addItemForm,
  },
  data: () => ({
    items: JSON.parse(localStorage.getItem('todos')) || [],
  }),
  methods: {
    generateTodoID() {
      return (new Date() - Math.random()).toString(36).substr(1, 9);
    },
    addTaskToList(value) {
      if (value === '') {
        alert('Task should not be empty');
      } else {
        this.items.unshift({
          title: value,
          state: false,
          id: this.generateTodoID(),
        });
        this.sendDataToLS();
      }
    },
    deleteTask(itemId) {
      this.items.forEach((item, index) => {
        if (item.id === itemId) {
          this.items.splice(index, 1);
          this.sendDataToLS();
          return null;
        }
        return null;
      });
    },
    changeItemState(itemId) {
      this.items.forEach((item, index) => {
        if (item.id === itemId) {
          this.items[index].state = !this.items[index].state;
          this.sendDataToLS();
          return null;
        }
        return null;
      });
    },
    editTaskTitle(todoObj) {
      this.items.forEach((item, index) => {
        if (item.id === todoObj.id) {
          this.items[index].title = todoObj.title;
          this.sendDataToLS();
          return null;
        }
        return null;
      });
    },
    sendDataToLS() {
      localStorage.setItem('todos', JSON.stringify(this.items));
    },
  },
};
</script>

<style scoped lang="scss">
  h2 {
    color: black;
    border: 1px solid lightgray;
    border-radius: 3px 3px 0 0;
    padding: 1rem;
    background: #fff;
    margin:  20px 0 0 0;
  }
  ul {
    border: 1px solid lightgray;
    border-radius: 0 0 3px 3px;
    border-top: 0px;
    background: #fff;
    padding: 1rem;
    margin: 0;
  }
</style>
