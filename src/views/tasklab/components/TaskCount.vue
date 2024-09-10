<template>
  <el-card class="box-card">
    <h2>任务盘点</h2>
    <div class="inventory-counts">
      <div class="count-item">
     <!--   <el-progress type="dashboard" :percentage="50" :stroke-width="10"></el-progress>-->
        <span class="count-title">待审核：</span>
        <span class="count-number">123</span>
      </div>
      <div class="count-item">
     <!--   <el-icon><ElIconSuccess /></el-icon>-->
        <span class="count-title">紧急待处理：</span>
        <span class="count-number">13+24</span>
      </div>
    </div>
  </el-card>
</template>

<script>
//import { ElIcon, ElProgress, ElIconSuccess } from 'element-plus';
//import 'element-plus/icons';

export default {
  name: 'TaskCount',
  components: {
   // ElIcon,
   // ElProgress
  },
  data() {
    return {
      tasks: {
        // 示例数据
        
    }
    };
  },
  computed: {
    pendingCount() {
      return 123; // 返回待审核数量
    },
    urgentCount() {
      return 37; // 返回紧急待处理数量
    }
  }
};
</script>

<style scoped>
.box-card {
  width: 100%;
}
.inventory-counts {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
.count-item {
  display: flex;
  align-items: center;
  margin-right: 20px;
}
.count-title {
  margin-left: 10px;
  font-size: 14px;
  color: #999;
}
.count-number {
  margin-left: 5px;
  font-size: 16px;
  font-weight: bold;
}
</style>