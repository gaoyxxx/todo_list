<template>
  <li>
    <label>
      <!-- 这里不建议写 v-model，虽然可以实现，但实际上是钻了空子 -->
      <!-- props 数据为只读，不建议修改，应传递给父组件，让父组件来修改 -->
      <!-- <input type="checkbox" v-model="todo.done" /> -->
      <input type="checkbox" :checked="todo.done" @click="handleCheckDone(todo.id)" />
      <span>{{ todo.title }}</span>
    </label>
    <button class="btn btn-danger" @click="handleDelete(todo.id)">删除</button>
  </li>
</template>

<script>
export default {
  name: "MyItem",
  props: [
    'todo', 
    'checkToDoDone',
    'deleteToDo'
  ],
  methods: {
    // 勾选、取消勾选
    handleCheckDone(id) {
      // 通知 App 组件将对应 ToDo 的 done 值取反
      this.checkToDoDone(id)
    },
    // 删除一个 ToDo
    handleDelete(id) {
      if (confirm('是否确认删除')) {
        this.deleteToDo(id)
      }
    }
  },
};
</script>

<style scoped>
/*item*/
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid #ddd;
}

li label {
  float: left;
  cursor: pointer;
}

li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}

li button {
  float: right;
  display: none;
  margin-top: 3px;
}

li:before {
  content: initial;
}

li:last-child {
  border-bottom: none;
}

li:hover {
  background: #f5f5f5;
}

li:hover button{
  display: block;
}

</style>