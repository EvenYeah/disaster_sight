<template>
  <div>
  <!--  <router-view/>-->
  <TaskCount/>

  <el-card class="box-card">
   <!-- 点击切换任务类型 -->
    <div class="type-selector">
      <el-button type="primary" size="small" @click="handleClick('urgentTasks')">紧急任务</el-button>
      <el-button type="primary" size="small" @click="handleClick('normalTasks')">普通任务</el-button>
    </div>
    <!-- 展示任务 -->
    <div v-if="tasks[selectedType].length > 0">
      <br>
      <el-row :gutter="20">
        <el-col :span="8" v-for="(task, index) in tasks[selectedType]" :key="index">
          <el-card :body-style="{ padding: '0px' }">
            <img :src="task.thumbnail" class="image" />
            <div style="padding: 14px;">
              <span>{{ task.title }}</span>
              <div class="bottom clearfix">
                <time class="time">{{ task.date }}</time>
                <el-button text type="text" @click="viewDetails(task)">查看详情</el-button>
              </div>
            </div>
          </el-card>
        </el-col>
      </el-row>
    </div>
    <div v-else>
      <p>暂无{{ selectedType }}</p>
    </div>


    <!-- 分页 -->
    <el-pagination
      background
      layout="prev, pager, next"
      :total="totalTasks"
      @current-change="handleCurrentChange"
    ></el-pagination>
  </el-card>
  </div>
</template>


    


<script>
import TaskCount from './components/TaskCount.vue';

export default {
  data() {
    return {
      selectedType: 'urgentTasks', // 默认显示紧急任务
      tasks: {
        urgentTasks: [ 
          {
          id: 1,
          thumbnail: 'https://via.placeholder.com/150x150', // 替换为实际的缩略图URL
          title: '视频标题1',
          date: '2024-09-01'
        },
        {
          id: 2,
          thumbnail: 'https://via.placeholder.com/150x150', // 替换为实际的缩略图URL
          title: '视频标题2',
          date: '2024-09-02'
        }
         ], // 紧急任务的数据
        normalTasks: [ 
          {
          id: 3,
          thumbnail: 'https://via.placeholder.com/150x150', // 替换为实际的缩略图URL
          title: '视频标题3',
          date: '2024-09-03'
        },
        {
          id: 4,
          thumbnail: 'https://via.placeholder.com/150x150', // 替换为实际的缩略图URL
          title: '视频标题4',
          date: '2024-09-04'
        }
         ]  // 普通任务的数据
       
      },
      currentPage: 1,
      totalTasks: 20
    };
  },
  methods: {
    handleCurrentChange(val) {
      this.currentPage = val;
      console.log(`当前页: ${val}`);
    },
    handleClick(type) {
    this.selectedType = type;
    }
  },
  components: {
    TaskCount
  }
  
};
</script>

<style scoped>
.box-card {
  width: 100%;
}
.image {
  width: 100%;
  display: block;
}
.clearfix:before,
.clearfix:after {
  display: table;
  content: "";
}
.clearfix:after {
  clear: both;
}
.time {
  font-size: 13px;
  color: #999;
}
</style>