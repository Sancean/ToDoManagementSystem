<template>
  <el-row :gutter="16">
    <el-col :span="8">
      <div class="statistic-card">
        <el-statistic :value="indexVo.total">
          <template #title>
            <div style="display: inline-flex; align-items: center">
              待办事项总数
              <el-tooltip effect="dark" content="您添加的所有的待办事项" placement="top">
                <el-icon style="margin-left: 4px" :size="12">
                  <Warning />
                </el-icon>
              </el-tooltip>
            </div>
          </template>
        </el-statistic>
      </div>
    </el-col>
    <el-col :span="8">
      <div class="statistic-card">
        <el-statistic :value="indexVo.unfinished">
          <template #title>
            <div style="display: inline-flex; align-items: center">
              未完成的待办事项
              <el-tooltip effect="dark" content="您添加的所有待办事项中，未完成的" placement="top">
                <el-icon style="margin-left: 4px" :size="12">
                  <Warning />
                </el-icon>
              </el-tooltip>
            </div>
          </template>
        </el-statistic>
      </div>
    </el-col>
    <el-col :span="8">
      <div class="statistic-card">
        <el-statistic :value="indexVo.finished">
          <template #title>
            <div style="display: inline-flex; align-items: center">
              已完成的待办事项
              <el-tooltip effect="dark" content="您已经完成的所有待办事项" placement="top">
                <el-icon style="margin-left: 4px" :size="12">
                  <Warning />
                </el-icon>
              </el-tooltip>
            </div>
          </template>
        </el-statistic>
      </div>
    </el-col>
    <el-col :span="8">
      <div class="statistic-card">
        <el-statistic :value="indexVo.expired">
          <template #title>
            <div style="display: inline-flex; align-items: center">
              已过期的待办事项
              <el-tooltip effect="dark" content="您已经完成的所有待办事项" placement="top">
                <el-icon style="margin-left: 4px" :size="12">
                  <Warning />
                </el-icon>
              </el-tooltip>
            </div>
          </template>
        </el-statistic>
      </div>
    </el-col>
  </el-row>
</template>

<script lang="ts" setup>
import { Warning, } from '@element-plus/icons-vue'
import { index } from '@/api/todo'
import { onMounted, reactive } from 'vue'
import {ElNotification} from 'element-plus'
const indexVo = reactive({
  total: 0,
  unfinished: 0,
  finished: 0,
  expired: 0
})
const getIndexData = () => {
  index().then((res) => {
    var data = res.data.data
    indexVo.total = data.total
    indexVo.unfinished = data.unfinished
    indexVo.finished = data.finished
    indexVo.expired = data.expired
  }).catch((error) => {
    console.log(error)
    ElNotification.error({
      title: 'error',
      message: error,
      offset: 100
    })
  })
}
onMounted(() => {
  getIndexData()
})
</script>

<style scoped>
:global(h2#card-usage ~ .example .example-showcase) {
  background-color: var(--el-fill-color) !important;
}

.el-statistic {
  --el-statistic-content-font-size: 28px;
}

.statistic-card {
  height: 100%;
  padding: 20px;
  border-radius: 4px;
  background-color: var(--el-bg-color-overlay);
}

.statistic-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  font-size: 12px;
  color: var(--el-text-color-regular);
  margin-top: 16px;
}

.statistic-footer .footer-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.statistic-footer .footer-item span:last-child {
  display: inline-flex;
  align-items: center;
  margin-left: 4px;
}

.green {
  color: var(--el-color-success);
}

.red {
  color: var(--el-color-error);
}
</style>
