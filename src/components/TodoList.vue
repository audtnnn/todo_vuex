<template>
  <section>
      <transition-group name="fade" tag="ul">
      <li v-for="item in todos" :key="item.id">
        <input type="checkbox" v-model="item.modify" @click="onToggle(item.id)">
        <label :for="item.id"><i :class="{'fa-solid':true, 'fa-pen-to-square':item.update, 'fa-floppy-disk':!item.update}" @click="onUpdate(item.id)"></i></label>
        {{item.id}}번 <input id="item.id" type="text" :class="{on:item.modify}" :value ="item.text" :disabled="item.update" @input="onInput(item.id, $event)">
        <button type="button" @click="onRemove(item.id)">
          <i class="fa-solid fa-trash-can"></i>
        </button>
      </li>
      </transition-group>
  </section>
</template>

<script>
export default {
  name: "TodoList",
  computed: {
    todos(){
      return this.$store.getters.fnGetTodos
    }
  },
  methods: {
    onRemove(id){
      let answer = confirm("정말로 삭제하시겠습니까?")
      if (answer) {
      // this.$emit("onRemove", id)
      this.$store.commit("on__Remove", id)
      }
    },
    onToggle(id){
      // this.$emit("onToggle", id)
      this.$store.commit("on__Toggle", id)
    },
    onUpdate(id){
      this.$store.commit("on__Update", id)
    },
    onInput(id, e){
      this.$store.commit("on__Input", {id:id, value:e.target.value})
    }
  }
};
</script>

<style lang="scss" scoped>
  section {
    ul {
      li {
        display:flex;
        height:60px; 
        margin:5px 0; 
        padding:0 16px; 
        border-bottom:1px solid #ddd;
        align-items:center;
        span {margin:0 10px}
        input[type=text] {
           flex:1;  padding: 5px; margin:0 10px; font-size:20px; background: none;
           &.on {
            text-decoration:line-through; color:#999
           }
         }
        button { color:red; font-size:20px;  }
      }
    }
  }


  .fade-enter-active, .fade-leave-active {
    transition: all 0.5s;
  }
  .fade-enter, .fade-leave-to {
    opacity: 0;
    transform: translateX(50px);
  }
</style>
