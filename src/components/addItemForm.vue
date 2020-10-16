<template>
  <form v-on:submit.prevent="">
    <input
      placeholder="What needs to be done?"
      v-model="inputText"
    >
    <button
      @click="onEnterTaskInForm"
      @keyup.enter="onEnterTaskInForm"
    >&#x2b; Add</button>
  </form>
</template>

<script>

export default {
  name: 'addItemForm',
  data: () => ({
    inputText: '',
  }),
  methods: {
    onEnterTaskInForm() {
      this.$emit('enterTask', this.inputText);
      this.inputText = '';
    },
  },
};
</script>

<style scoped lang="scss">
  form {
    padding: 1rem;
    display: flex;
    flex-wrap: wrap;
    & button {
      min-width: 200px;
      background: #33ccff;
      border-radius: 3px;
      color: #fff;
      font-size: 1.5rem;
      line-height: 2rem;
      padding: 0 2rem;
      transition: all 0.6s ease;
      margin-bottom: 10px;
      margin-right: 20px;
      cursor: pointer;
    }
    & button:hover {
      filter: invert(10%);
    }
    & input {
      flex-grow: 1;
      margin: 0 10px 10px 0;
      border-radius: 3px;
      border: 1px solid lightgray;
      padding-left: 10px;
      padding: 10px;
      font-size: 1rem;
    }
  }
</style>
