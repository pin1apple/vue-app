<script setup>
import { ref } from 'vue'

const tasks = ref([
  { text: '完成Vue项目搭建', done: true, tag: 'work' },
  { text: '学习响应式布局', done: true, tag: 'study' },
  { text: '写周报总结', done: false, tag: 'work' },
  { text: '整理桌面文件', done: false, tag: 'personal' },
  { text: '读Vue3官方文档', done: false, tag: 'study' },
  { text: '设计数据库表结构', done: false, tag: 'work' },
  { text: '买日用品', done: false, tag: 'personal' },
  { text: '复习JavaScript基础', done: false, tag: 'study' },
])

const filter = ref('all')
const newTaskText = ref('')

function toggleDone(index) {
  tasks.value[index].done = !tasks.value[index].done
}

function addTask() {
  const text = newTaskText.value.trim()
  if (!text) return
  tasks.value.unshift({ text, done: false, tag: 'personal' })
  newTaskText.value = ''
}

function deleteTask(index) {
  tasks.value.splice(index, 1)
}

const filteredTasks = computed(() => {
  if (filter.value === 'done') return tasks.value.filter(t => t.done)
  if (filter.value === 'pending') return tasks.value.filter(t => !t.done)
  return tasks.value
})

import { computed } from 'vue'

const pendingCount = computed(() => tasks.value.filter(t => !t.done).length)
</script>

<template>
  <div>
    <div class="page-header">
      <h1>任务清单</h1>
      <p>管理你的日常任务，共 {{ tasks.length }} 项，{{ pendingCount }} 项待完成</p>
    </div>

    <!-- Add task -->
    <div class="card" style="margin-bottom: 20px; display: flex; gap: 12px; padding: 16px 20px;">
      <input
        v-model="newTaskText"
        @keyup.enter="addTask"
        placeholder="添加新任务..."
        style="flex: 1; border: 1px solid var(--border); border-radius: 8px; padding: 10px 14px; font-size: 14px; outline: none; background: var(--bg);"
      />
      <button
        @click="addTask"
        style="background: var(--primary); color: #fff; border: none; border-radius: 8px; padding: 10px 20px; font-size: 14px; font-weight: 600; white-space: nowrap;"
      >
        添加
      </button>
    </div>

    <!-- Filters -->
    <div style="display: flex; gap: 8px; margin-bottom: 16px; flex-wrap: wrap;">
      <button
        v-for="f in [{ key: 'all', label: '全部' }, { key: 'pending', label: '待完成' }, { key: 'done', label: '已完成' }]"
        :key="f.key"
        @click="filter = f.key"
        :style="{
          padding: '6px 16px',
          borderRadius: '20px',
          border: '1px solid var(--border)',
          fontSize: '13px',
          fontWeight: 600,
          background: filter === f.key ? 'var(--primary)' : 'transparent',
          color: filter === f.key ? '#fff' : 'var(--text-secondary)',
        }"
      >
        {{ f.label }}
      </button>
    </div>

    <!-- Task list -->
    <div class="card" style="padding: 0 20px;">
      <div v-if="filteredTasks.length === 0" class="empty-state">
        <div class="empty-icon">🎉</div>
        <h3>没有任务</h3>
        <p>当前筛选条件下没有任务</p>
      </div>
      <div
        v-for="(t, i) in filteredTasks"
        :key="i"
        class="task-item"
      >
        <button
          class="task-check"
          :class="{ done: t.done }"
          @click="toggleDone(i)"
        >
          {{ t.done ? '✓' : '' }}
        </button>
        <span class="task-text" :class="{ done: t.done }">{{ t.text }}</span>
        <span class="task-tag" :class="'tag-' + t.tag">{{ t.tag }}</span>
        <button
          @click="deleteTask(i)"
          style="background: none; border: none; color: var(--text-secondary); font-size: 16px; padding: 4px; opacity: .5;"
          title="删除"
        >
          🗑️
        </button>
      </div>
    </div>
  </div>
</template>
