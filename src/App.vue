<script setup>
import { ref } from 'vue'
import { useRoute, useRouter } from 'vue-router'

const route = useRoute()
const router = useRouter()
const sidebarOpen = ref(false)

const navItems = [
  { path: '/', label: '仪表盘', icon: '📊' },
  { path: '/tasks', label: '任务清单', icon: '✅' },
  { path: '/notes', label: '备忘录', icon: '📝' },
  { path: '/about', label: '关于', icon: 'ℹ️' },
]

function isActive(path) {
  return route.path === path
}

function navigate(path) {
  router.push(path)
  sidebarOpen.value = false
}

function toggleSidebar() {
  sidebarOpen.value = !sidebarOpen.value
}
</script>

<template>
  <div class="app-layout">
    <!-- Mobile toggle -->
    <button class="sidebar-toggle" @click="toggleSidebar">
      {{ sidebarOpen ? '✕' : '☰' }}
    </button>

    <!-- Overlay -->
    <div
      class="sidebar-overlay"
      :class="{ open: sidebarOpen }"
      @click="sidebarOpen = false"
    />

    <!-- Sidebar -->
    <aside class="sidebar" :class="{ open: sidebarOpen }">
      <div class="sidebar-brand">
        <div class="logo-icon">V</div>
        <span class="brand-text">Vue App</span>
      </div>
      <nav class="sidebar-nav">
        <router-link
          v-for="item in navItems"
          :key="item.path"
          :to="item.path"
          class="nav-item"
          :class="{ active: isActive(item.path) }"
          @click="sidebarOpen = false"
        >
          <span class="nav-icon">{{ item.icon }}</span>
          <span class="nav-label">{{ item.label }}</span>
        </router-link>
      </nav>
      <div style="padding: 12px 20px; border-top: 1px solid var(--border); font-size: 12px; color: var(--text-secondary);">
        v1.0.0
      </div>
    </aside>

    <!-- Main -->
    <main class="main-content">
      <router-view />
    </main>
  </div>
</template>
