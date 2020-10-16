<template>
  <li>
    <input
      v-if="editField"
      type="text"
      placeholder="What needs to be done?"
      v-model="item.title"
      @keyup.enter="clickOnSaveBtn"
    >
    <div style="line-height: 20px">
      <input type="checkbox" :checked="state" @change="clickOnCheckbox">
      <span class="indicator" :class="{done: state}"></span>
      <span class="title" v-bind:class="{linethrough: state}">
        {{ item.title }}
      </span>
    </div>
    <button
      class="item-btn"
      @click="clickOnEditBtn"
      v-if="!editField"
    >
      Edit
    </button>
    <button
      class="item-btn"
      @click="clickOnSaveBtn"
      v-else
    >
      Save
    </button>
    <button @click="clickOnDeleteBtn" class="item-btn">Delete</button>
  </li>
</template>

<script>
export default {
  name: 'todoitem',
  data: () => ({
    editField: false,
  }),
  props: ['item', 'state'],
  methods: {
    clickOnDeleteBtn() {
      this.$emit('deleteTask', this.item.id);
    },
    clickOnCheckbox() {
      this.$emit('changeState', this.item.id);
    },
    clickOnEditBtn() {
      this.editField = true;
    },
    clickOnSaveBtn() {
      if (this.item.title === '') {
        alert('Task should not be empty, enter data or delete task');
      } else {
        this.editField = false;
        this.$emit('editTask', {
          id: this.item.id,
          title: this.item.title,
        });
      }
    },
  },
};
</script>

<style scoped lang="scss">
  li {
    list-style-type: none;
    margin: 0 10px 10px 10px;
    border-radius: 3px;
    font-size: 1rem;
    border-bottom:  1px solid lightgray;
    padding: 1rem 0 2.5rem 0;
    text-align: justify;
    & .linethrough {
      text-decoration: line-through;
    }
    & .indicator::after {
      content: "\2013";
      padding: 0 10px;
      border: 1px solid red;
      background-color: pink;
      border-radius: 3px;
      margin-right: 10px;
    }
    & .indicator.done::after {
      content: "\2713";
      padding: 0 8px;
      border: 1px solid green;
      background-color: lightgreen;
    }
    & .item-btn {
      border: 1px solid lightgray;
      border-radius: 3px;
      padding: 10px;
      color: gray;
      max-height: 35px;
      margin-left: 10px;
      cursor: pointer;
      float: right;
    }
    & .item-btn:hover {
      filter: invert(10%);
    }
    & input[type="text"] {
      flex-grow: 1;
      margin: 0 10px 10px 0;
      border-radius: 3px;
      border: 1px solid lightgray;
      padding-left: 10px;
      padding: 10px;
      font-size: 1rem;
      width: 95%;
    }
    & input[type="checkbox"] {
      margin-right: 10px;
    }
  }
</style>
