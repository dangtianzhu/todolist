<template>
  <div>
    <div v-if="list.length > 0">
      <div v-for="(item, index) in list" :key="index">
        <div>正在进行{{ isComplete }}</div>
        <div class="item">
          <input type="checkbox" v-model="item.complete" />
          {{ item.title }}
          <button class="del" @click="del(item, index)">删除</button>
          <button class="update" @click="update(item, index)">修改</button>
        </div>
      </div>
    </div>
    <div v-else>
        暂无任务
    </div>
  </div>
</template>

<script>
import { defineComponent, ref } from "vue";
// import {useStore} from 'vuex'
export default defineComponent({
  name: "navMain",
  props: {
    list: {
      type: Array,
      required: true,
    },
  },

  setup(props, ctx) {
    let doing = ref(1);

    let del = (item, index) => {
      ctx.emit("del", index);
    };
    let update = (item, index) => {
      console.log(item);
    };
    return {
      doing,
      del,
      update,
    };
  },
});
</script>

<style lang="less" scoped>
// .item {
//   height: 55px;
//   line-height: 90px;
//   position: relative;
//   width: 160px;

// }

.item {
  display: flex;
  align-items: center;
  padding: 10px;
  border-bottom: 1px solid #ccc;
}

.item input[type="checkbox"] {
  margin-right: 10px;
}

.item .del,
.item .update {
  margin-left: auto;
  padding: 5px 10px;
  background-color: #f44336;
  color: white;
  border: none;
  cursor: pointer;
}

.item .update {
  background-color: #4caf50;
  margin-left: 10px;
}

.item .del:hover,
.item .update:hover {
  background-color: #d32f2f;
}

.item .update:hover {
  background-color: #388e3c;
}
</style>
