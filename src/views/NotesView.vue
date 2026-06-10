<script setup>
import { ref } from 'vue'

const newNote = ref({ title: '', content: '' })
const showForm = ref(false)

const notes = ref([
  { title: 'Vue3学习笔记', content: ' Composition API 是 Vue3 的核心特性，包括 ref、reactive、computed 等。setup 函数在组件创建之前执行。', date: '2026-06-08', color: '#eef2ff' },
  { title: '项目计划', content: '1. 完成前端页面\n2. 对接后端API\n3. 单元测试\n4. 部署上线', date: '2026-06-07', color: '#fef3c7' },
  { title: '会议纪要', content: '讨论了下个迭代的功能点：用户权限管理、数据可视化看板、消息通知系统。', date: '2026-06-05', color: '#fce7f3' },
  { title: '读书笔记', content: '《设计模式》—— 单例模式确保一个类只有一个实例，并提供一个全局访问点。', date: '2026-06-03', color: '#d1fae5' },
  { title: '周末计划', content: '周六：爬山\n周日：看电影 + 看书', date: '2026-06-01', color: '#e0e7ff' },
])

function addNote() {
  if (!newNote.value.title.trim() || !newNote.value.content.trim()) return
  const now = new Date()
  const date = `${now.getFullYear()}-${String(now.getMonth()+1).padStart(2,'0')}-${String(now.getDate()).padStart(2,'0')}`
  const colors = ['#eef2ff', '#fef3c7', '#fce7f3', '#d1fae5', '#e0e7ff']
  notes.value.unshift({
    title: newNote.value.title,
    content: newNote.value.content,
    date,
    color: colors[Math.floor(Math.random() * colors.length)],
  })
  newNote.value = { title: '', content: '' }
  showForm.value = false
}

function deleteNote(index) {
  notes.value.splice(index, 1)
}
</script>

<template>
  <div>
    <div class="page-header" style="display: flex; align-items: center; justify-content: space-between; flex-wrap: wrap; gap: 12px;">
      <div>
        <h1>备忘录</h1>
        <p>记录你的想法和笔记，共 {{ notes.length }} 条</p>
      </div>
      <button
        @click="showForm = !showForm"
        :style="{
          background: showForm ? '#fee2e2' : 'var(--primary)',
          color: showForm ? 'var(--danger)' : '#fff',
          border: 'none',
          borderRadius: '8px',
          padding: '10px 20px',
          fontSize: '14px',
          fontWeight: 600,
        }"
      >
        {{ showForm ? '取消' : '+ 新建笔记' }}
      </button>
    </div>

    <!-- New note form -->
    <div
      v-if="showForm"
      class="card"
      style="margin-bottom: 24px;"
    >
      <input
        v-model="newNote.title"
        placeholder="标题"
        style="width: 100%; border: none; border-bottom: 1px solid var(--border); padding: 8px 0; font-size: 16px; font-weight: 600; outline: none; margin-bottom: 12px;"
      />
      <textarea
        v-model="newNote.content"
        placeholder="写点什么..."
        rows="4"
        style="width: 100%; border: none; padding: 8px 0; font-size: 14px; outline: none; resize: vertical; background: transparent; font-family: inherit;"
      />
      <div style="text-align: right; margin-top: 8px;">
        <button
          @click="addNote"
          :disabled="!newNote.title.trim() || !newNote.content.trim()"
          :style="{
            background: 'var(--primary)',
            color: '#fff',
            border: 'none',
            borderRadius: '8px',
            padding: '8px 24px',
            fontSize: '14px',
            fontWeight: 600,
            opacity: (!newNote.title.trim() || !newNote.content.trim()) ? .5 : 1,
          }"
        >
          保存
        </button>
      </div>
    </div>

    <!-- Notes grid -->
    <div v-if="notes.length === 0" class="card empty-state">
      <div class="empty-icon">📝</div>
      <h3>还没有笔记</h3>
      <p>点击右上角新建第一条笔记</p>
    </div>
    <div v-else class="grid-3">
      <div
        v-for="(note, i) in notes"
        :key="i"
        class="card note-card"
        :style="{ background: note.color }"
      >
        <div style="display: flex; justify-content: space-between; align-items: flex-start;">
          <div>
            <div class="note-date">{{ note.date }}</div>
            <h3>{{ note.title }}</h3>
          </div>
          <button
            @click="deleteNote(i)"
            style="background: none; border: none; font-size: 14px; opacity: .4; cursor: pointer; padding: 4px;"
            title="删除"
          >
            ✕
          </button>
        </div>
        <p style="white-space: pre-wrap;">{{ note.content }}</p>
      </div>
    </div>
  </div>
</template>
