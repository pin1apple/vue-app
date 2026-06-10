<script setup>
import { ref } from 'vue'

const stats = ref([
  { label: '完成任务', value: 24, icon: '✅', color: '#eef2ff', change: '+12%', trend: 'up' },
  { label: '进行中', value: 6, icon: '🔄', color: '#fef3c7', change: '-3%', trend: 'down' },
  { label: '备忘录', value: 18, icon: '📝', color: '#fce7f3', change: '+5%', trend: 'up' },
  { label: '总项目', value: 8, icon: '📦', color: '#d1fae5', change: '+2%', trend: 'up' },
])

const recentTasks = ref([
  { text: '完成Vue项目搭建', done: true, tag: 'work' },
  { text: '学习响应式布局', done: true, tag: 'study' },
  { text: '写周报总结', done: false, tag: 'work' },
  { text: '整理桌面文件', done: false, tag: 'personal' },
  { text: '读Vue3官方文档', done: false, tag: 'study' },
])
</script>

<template>
  <div>
    <div class="page-header">
      <h1>仪表盘</h1>
      <p>欢迎回来，这是你的工作概览</p>
    </div>

    <!-- Stats -->
    <div class="grid-4" style="margin-bottom: 28px;">
      <div
        v-for="s in stats"
        :key="s.label"
        class="card stat-card"
      >
        <div class="stat-header">
          <span class="stat-label">{{ s.label }}</span>
          <div class="stat-icon" :style="{ background: s.color }">
            {{ s.icon }}
          </div>
        </div>
        <div class="stat-value">{{ s.value }}</div>
        <div class="stat-change" :class="s.trend">
          {{ s.change }} 较上月
        </div>
      </div>
    </div>

    <!-- Charts / Recent -->
    <div class="grid-2">
      <div class="card">
        <h3 style="font-size: 16px; font-weight: 600; margin-bottom: 16px;">
          最近任务
        </h3>
        <div
          v-for="(t, i) in recentTasks"
          :key="i"
          class="task-item"
        >
          <div class="task-check" :class="{ done: t.done }">
            {{ t.done ? '✓' : '' }}
          </div>
          <span class="task-text" :class="{ done: t.done }">{{ t.text }}</span>
          <span class="task-tag" :class="'tag-' + t.tag">{{ t.tag }}</span>
        </div>
      </div>

      <div class="card">
        <h3 style="font-size: 16px; font-weight: 600; margin-bottom: 16px;">
          快捷入口
        </h3>
        <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 12px;">
          <router-link
            to="/tasks"
            style="display: flex; flex-direction: column; align-items: center; gap: 8px; padding: 20px; border-radius: 10px; background: var(--bg); text-decoration: none; color: var(--text);"
          >
            <span style="font-size: 28px;">✅</span>
            <span style="font-size: 13px; font-weight: 500;">任务管理</span>
          </router-link>
          <router-link
            to="/notes"
            style="display: flex; flex-direction: column; align-items: center; gap: 8px; padding: 20px; border-radius: 10px; background: var(--bg); text-decoration: none; color: var(--text);"
          >
            <span style="font-size: 28px;">📝</span>
            <span style="font-size: 13px; font-weight: 500;">写备忘录</span>
          </router-link>
        </div>
      </div>
    </div>
  </div>
</template>
