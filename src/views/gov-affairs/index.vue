<template>
  <div class="gov-affairs-container">
    <!-- 服务分类导航 -->
    <el-row :gutter="20" class="service-nav">
      <el-col :xs="24" :sm="12" :md="6" v-for="(category, index) in serviceCategories" :key="index">
        <el-card shadow="hover" class="category-card" @click="handleCategoryClick(category)">
          <div class="category-content">
            <el-icon class="category-icon" :size="40">
              <component :is="category.icon" />
            </el-icon>
            <div class="category-info">
              <h3>{{ category.title }}</h3>
              <p>{{ category.description }}</p>
            </div>
          </div>
        </el-card>
      </el-col>
    </el-row>

    <!-- 办事指南 -->
    <el-card class="guide-section" shadow="hover">
      <template #header>
        <div class="card-header">
          <span>办事指南</span>
          <el-button type="primary" size="small" :icon="Plus" @click="handleAddGuide">发布指南</el-button>
        </div>
      </template>
      <el-table :data="guideList" style="width: 100%" v-loading="guideLoading" border stripe>
        <el-table-column prop="title" label="标题" min-width="200" />
        <el-table-column prop="department" label="发布部门" width="150" />
        <el-table-column prop="updateTime" label="更新时间" width="180" />
        <el-table-column prop="views" label="浏览量" width="100" />
        <el-table-column label="操作" width="140" fixed="right">
          <template #default="{ row }">
            <el-button-group>
              <el-button type="primary" :icon="View" circle @click="viewGuide(row)" title="查看" />
              <el-button type="warning" :icon="Edit" circle @click="editGuide(row)" title="编辑" />
              <el-button type="danger" :icon="Delete" circle @click="deleteGuide(row)" title="删除" />
            </el-button-group>
          </template>
        </el-table-column>
      </el-table>
    </el-card>

    <!-- 在线咨询 -->
    <el-card class="consultation-section" shadow="hover">
      <template #header>
        <div class="card-header">
          <span>在线咨询</span>
          <el-button type="primary" size="small" :icon="Plus" @click="handleNewConsultation">发起咨询</el-button>
        </div>
      </template>
      <el-table :data="consultationList" style="width: 100%" v-loading="consultationLoading" border stripe>
        <el-table-column prop="title" label="咨询主题" min-width="200" />
        <el-table-column prop="user" label="咨询人" width="120" />
        <el-table-column prop="department" label="回复部门" width="150" />
        <el-table-column prop="status" label="状态" width="100">
          <template #default="{ row }">
            <el-tag :type="row.status === '已回复' ? 'success' : 'warning'">
              {{ row.status }}
            </el-tag>
          </template>
        </el-table-column>
        <el-table-column prop="createTime" label="咨询时间" width="180" />
        <el-table-column label="操作" width="100" fixed="right">
          <template #default="{ row }">
            <el-button type="primary" :icon="View" circle @click="viewConsultation(row)" title="查看" />
          </template>
        </el-table-column>
      </el-table>
    </el-card>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import {
  Plus,
  View,
  Edit,
  Delete,
  Document
} from '@element-plus/icons-vue'

// 服务分类
const serviceCategories = [
  {
    title: '行政审批',
    description: '提供城前镇各类行政审批服务',
    icon: 'Document'
  },
  {
    title: '证件办理',
    description: '提供城前镇居民证件办理服务',
    icon: 'Document'
  },
  {
    title: '政策咨询',
    description: '提供城前镇政策咨询服务',
    icon: 'Document'
  },
  {
    title: '投诉建议',
    description: '提供城前镇投诉建议服务',
    icon: 'Document'
  }
]

// 办事指南列表
const guideList = ref([
  {
    id: 1,
    title: '城前镇宅基地审批办理指南',
    department: '自然资源所',
    updateTime: '2024-03-15 10:00',
    views: 1250
  },
  {
    id: 2,
    title: '城前镇农村建房审批流程',
    department: '规划建设所',
    updateTime: '2024-03-14 15:30',
    views: 980
  },
  {
    id: 3,
    title: '城前镇农业补贴申请指南',
    department: '农业服务中心',
    updateTime: '2024-03-13 09:15',
    views: 1560
  }
])

// 在线咨询列表
const consultationList = ref([
  {
    id: 1,
    title: '关于宅基地审批的问题咨询',
    user: '王先生',
    department: '自然资源所',
    status: '已回复',
    createTime: '2024-03-15 14:30'
  },
  {
    id: 2,
    title: '农村建房审批流程咨询',
    user: '李女士',
    department: '规划建设所',
    status: '已回复',
    createTime: '2024-03-14 16:20'
  }
])

const guideLoading = ref(false)
const consultationLoading = ref(false)

// 处理函数
const handleCategoryClick = (category: any) => {
  console.log('点击分类:', category)
}

const handleAddGuide = () => {
  console.log('添加指南')
}

const viewGuide = (row: any) => {
  console.log('查看指南:', row)
}

const editGuide = (row: any) => {
  console.log('编辑指南:', row)
}

const deleteGuide = (row: any) => {
  console.log('删除指南:', row)
}

const handleNewConsultation = () => {
  console.log('发起咨询')
}

const viewConsultation = (row: any) => {
  console.log('查看咨询:', row)
}
</script>

<style scoped>
.gov-affairs-container {
  padding: 20px;
}

.service-nav {
  margin-bottom: 20px;
}

.category-card {
  cursor: pointer;
  transition: all 0.3s;
}

.category-card:hover {
  transform: translateY(-5px);
}

.category-content {
  display: flex;
  align-items: center;
  padding: 10px;
}

.category-icon {
  margin-right: 15px;
  color: #409EFF;
}

.category-info h3 {
  margin: 0 0 5px 0;
  font-size: 16px;
}

.category-info p {
  margin: 0;
  font-size: 12px;
  color: #666;
}

.guide-section,
.consultation-section {
  margin-bottom: 20px;
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
</style> 