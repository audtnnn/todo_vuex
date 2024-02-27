<template>
  <header>
    <h1>일정관리앱 {{completedCount}}/{{totalCount}}건 처리</h1>
  </header>
</template>

<script>
export default {
  name: "TodoHeader",
  computed: {
    completedCount() {
      let todos = this.$store.getters.fnGetTodos
      return todos.filter(item=>item.modify==true).length
    },
    totalCount() {
      let todos = this.$store.getters.fnGetTodos
      return todos.length
    }
  }
};
</script>

<style scoped>
h1 {
  background: #22b8cf;
  color: #fff;
  font-size: 24px;
  text-align: center;
  padding: 20px;
}
</style>
