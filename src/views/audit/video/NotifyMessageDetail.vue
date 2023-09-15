<template>
  <Dialog v-model="dialogVisible" :max-height="500" :scroll="true" title="详情">
    <el-descriptions :column="1" border>
      <el-descriptions-item label="编号" min-width="120">
        {{ detailData.id }}
      </el-descriptions-item>
      <el-descriptions-item label="视频预览">
        <dict-tag :type="DICT_TYPE.USER_TYPE" :value="detailData.userType" />
      </el-descriptions-item>
      <el-descriptions-item label="机审结果">
        {{ detailData.userId }}
      </el-descriptions-item>
      <el-descriptions-item label="截图证据">
        {{ detailData.templateId }}
      </el-descriptions-item>
      <el-descriptions-item label="操作">
        <el-button
          link
          type="primary"
          @click="openDetail(scope.row)"
          v-hasPermi="['audit:video:query']"
        >
          通过
        </el-button>
        <el-button
          link
          type="primary"
          @click="openDetail(scope.row)"
          v-hasPermi="['audit:video:query']"
        >
          通知
        </el-button>
      </el-descriptions-item>
    </el-descriptions>
  </Dialog>
</template>
<script lang="ts" setup>
import { DICT_TYPE } from '@/utils/dict'
import { formatDate } from '@/utils/formatTime'
import * as NotifyMessageApi from '@/api/system/notify/message'

defineOptions({ name: 'SystemNotifyMessageDetail' })

const dialogVisible = ref(false) // 弹窗的是否展示
const detailLoading = ref(false) // 表单的加载中
const detailData = ref() // 详情数据

/** 打开弹窗 */
const open = async (data: NotifyMessageApi.NotifyMessageVO) => {
  dialogVisible.value = true
  // 设置数据
  detailLoading.value = true
  try {
    detailData.value = data
  } finally {
    detailLoading.value = false
  }
}
defineExpose({ open }) // 提供 open 方法，用于打开弹窗
</script>
