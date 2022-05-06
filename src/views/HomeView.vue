<template>
  <div class="home">
    <el-container>
      <el-header>Header</el-header>
      <el-container>
        <el-aside class="aside" width="400px"
          ><el-card class="box-card">
            <div class="box-card-menu">
              <draggable
                v-model="menu"
                @end="end1"
                :sort="false"
                :group="{ name: 'piece', pull: 'clone', put: false }"
                animation="300"
                :move="onMove"
              >
                <li class="menu-item" v-for="item in menu" :key="item.id">
                  {{ item.name }}
                </li>
              </draggable>
            </div>
          </el-card></el-aside
        >
        <!-- 右边内容区域 -->
        <el-main
          ><el-card class="box-card">
            <draggable
              v-model="contentList"
              @end="end2"
              :sort="true"
              :group="{ name: 'piece', pull: 'clone', put: true }"
              animation="300"
              :move="contentMove"
              @add="addFlowField"
            >
              <modelMenu
                class="conten-item"
                :type="item.id"
                v-for="(item, index) in contentList"
                :key="item.id + index"
                @click.native="currenClicked(index)"
              >
                <div class="delete" v-if="currentIndex==index"></div>
              </modelMenu>
            </draggable>
          </el-card></el-main
        >
      </el-container>
    </el-container>
  </div>
</template>

<script>
import modelMenu from "../components/modelMenu.vue";
export default {
  name: "HomeView",
  components: {
    modelMenu,
  },
  watch: {
    contentList: {
      //监听内容数组变化,更新到Vuex中
      handler(newVal, oldVal) {
        for (let i = 0; i < newVal.length; i++) {
          if (oldVal[i] != newVal[i]) {
            this.$store.state.contentList = newVal;
          }
        }
      },
    },
  },
  data() {
    return {
      currentIndex:0,
      menu: [
        { name: "输入框", id: "input" },
        { name: "文本框", id: "text" },
        { name: "数字输入框", id: "number-input" },
        { name: "下拉选择器", id: "select" },
        { name: "多选框", id: "mulit-select" },
      ],
      contentList: [],
    };
  },
  methods: {
    currenClicked(index){
       this.currentIndex=index
    },
    end1(e) {},
    end2() {},
    //只能拖拽
    onMove() {},
    contentMove(e) {
      console.log("拖拽完成", this.$store.state.contentList);
    },
    addFlowField(e) {},
  },
};
</script>
<style lang="less" scoped>
</style>
