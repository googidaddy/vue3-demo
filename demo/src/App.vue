<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <div>
    <h2>hello</h2>
    <div>请选择</div>
  </div>
  <div>
    <button
      v-for="(item, index) in boys"
      :key="index"
      @click="selectBoyFun(index)"
    >
      {{ index }} : {{ item }}
    </button>
  </div>
  <div>你选择了{{ selectBoy }} 为你服务</div>
</template>

<script lang="ts">
import { defineComponent, toRefs, reactive, ref, watch } from "vue";
// 接口：类型注解
interface DataProps {
  boys: string[];
  selectBoy: string;
  selectBoyFun: (index: number) => void;
}

export default defineComponent({
  name: "App",
  setup() {
    // reactive仅暴露一个函数
    const data: DataProps = reactive({
      boys: ["小红", "小白", "小绿"],
      selectBoy: "",
      selectBoyFun: (index: number) => {
        data.selectBoy = data.boys[index];
      },
    });
    const overText = ref("红");
    watch(overText, (newValue, oldValue) => {
      document.title = newValue;
    });
    const refData = toRefs(data);
    // !...:扩展符配合toRefs才能使用
    return {
      ...refData,
    };
  },
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
