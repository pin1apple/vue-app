<script setup>
</script>

<template>
  <div>
    <div class="page-header">
      <h1>关于</h1>
      <p>关于这个项目</p>
    </div>

    <div class="grid-2">
      <div class="card">
        <div style="display: flex; align-items: center; gap: 16px; margin-bottom: 20px;">
          <div style="width: 56px; height: 56px; background: linear-gradient(135deg, var(--primary), #818cf8); border-radius: 14px; display: flex; align-items: center; justify-content: center; color: #fff; font-size: 24px; font-weight: 700;">
            V
          </div>
          <div>
            <h2 style="font-size: 20px; font-weight: 700;">Vue App</h2>
            <p style="font-size: 13px; color: var(--text-secondary);">v1.0.0</p>
          </div>
        </div>
        <p style="font-size: 14px; color: var(--text-secondary); line-height: 1.8;">
          这是一个使用 Vue 3 + Vue Router 构建的响应式单页应用。<br>
          采用 Composition API 和现代 CSS 布局，适配桌面端和移动端。
        </p>
      </div>

      <div class="card">
        <h3 style="font-size: 16px; font-weight: 600; margin-bottom: 16px;">技术栈</h3>
        <div style="display: flex; flex-direction: column; gap: 12px;">
          <div v-for="tech in [
            { name: 'Vue 3', desc: 'Composition API + Script Setup' },
            { name: 'Vue Router', desc: 'SPA 路由管理' },
            { name: 'Vite', desc: '构建工具' },
            { name: 'CSS', desc: 'Flexbox + Grid 响应式布局' },
          ]" :key="tech.name" style="display: flex; justify-content: space-between; align-items: center; padding: 10px 0; border-bottom: 1px solid var(--border);">
            <span style="font-weight: 600; font-size: 14px;">{{ tech.name }}</span>
            <span style="font-size: 13px; color: var(--text-secondary);">{{ tech.desc }}</span>
          </div>
        </div>
      </div>

      <div class="card" style="grid-column: 1 / -1;">
        <h3 style="font-size: 16px; font-weight: 600; margin-bottom: 12px;">功能列表</h3>
        <div class="grid-3" style="gap: 12px;">
          <div v-for="f in [
            '响应式侧边栏导航',
            '仪表盘数据概览',
            '任务清单增删改',
            '备忘录随手记',
            '移动端适配',
            '无外部依赖',
          ]" :key="f" style="display: flex; align-items: center; gap: 8px; font-size: 14px;">
            <span style="color: var(--success);">✓</span>
            {{ f }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
