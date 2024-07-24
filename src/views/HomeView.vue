<template>
  <div>
    <nav-header @add="add"></nav-header>
    <nav-main :list="list" @del='del'></nav-main>
    <nav-footer :list="list"></nav-footer>
  </div>
</template>

<script>
import NavHeader from "@/components/navHeader/NavHeader.vue";
import NavMain from "@/components/navMain/NavMain.vue";
import NavFooter from "@/components/navFooter/NavFooter.vue";
import { defineComponent, ref, computed } from "vue";
import { useStore } from "vuex";

export default defineComponent({
  name: "HomeView",
  components: {
    NavMain,
    NavHeader,
    NavFooter,
  },
  setup() {
    let list = computed(() => {
      return store.state.list;
    });
    let store = useStore();
    let value = ref("");
    let add = (val) => {
      value.value = val;
      let flag = true;
      list.value.map((item) => {
        if (item.title === value.value) {
          flag = false
          alert("任务已经存在");
        }
      });
      if (flag) {
        store.commit("addTodo", {
          title: value.value,
          complete: false,
        });
      }
    };
    let del = (val) =>{
        store.commit('delTodo',val)
    }

    return {
      add,
      value,
      list,
      del
    };
  },
});
</script>

<style lang="less" scoped>
</style>
