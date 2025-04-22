<template>
  <div class="todo-footer" v-show="total">
    <label>
      <input type="checkbox" :checked="isAll" @click="checkAll" />
    </label>
    <span>
      <span>已完成 {{ doneTotal }}</span> / 全部 {{ total }}
    </span>
    <button class="btn btn-danger" @click="clearAll">清除已完成任务</button>
  </div>
</template>

<script>
export default {
  name: 'MyFooter',
  props: [
    'todos',
    'checkAllToDo',
    'clearAllToDo'
  ],
  computed: {
    total() {
      return this.todos.length
    },
    doneTotal() {
      return this.todos.filter(todo => todo.done).length
    },
    isAll() {
      return this.total > 0 && this.doneTotal === this.total
    }
  },
  methods: {
    // 全选、全不选
    checkAll(e) {
      this.checkAllToDo(e.target.checked)
    },
    // 清除已完成任务
    clearAll() {
      if (confirm('是否确认清除已完成任务？')) {
        this.clearAllToDo()
      }
    }
  },
}
</script>

<style scoped>
/*footer*/
.todo-footer {
  height: 40px;
  line-height: 40px;
  padding-left: 6px;
  margin-top: 5px;
}

.todo-footer label {
  display: inline-block;
  margin-right: 20px;
  cursor: pointer;
}

.todo-footer label input {
  position: relative;
  top: -1px;
  vertical-align: middle;
  margin-right: 5px;
}

.todo-footer button {
  float: right;
  margin-top: 5px;
}
</style>