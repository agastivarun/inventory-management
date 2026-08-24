<template>
  <div class="app-shell">
    <aside class="sidebar" :class="{ collapsed: sidebarCollapsed }">
      <div class="sidebar-brand">
        <div class="brand-mark">{{ t('nav.companyName').charAt(0) }}</div>
        <div class="brand-text">
          <h1>{{ t('nav.companyName') }}</h1>
          <span class="subtitle">{{ t('nav.subtitle') }}</span>
        </div>
      </div>

      <div class="sidebar-toggle-row">
        <button
          type="button"
          class="sidebar-toggle"
          :aria-label="sidebarCollapsed ? 'Expand sidebar' : 'Collapse sidebar'"
          @click="toggleSidebar"
        >
          <svg class="toggle-icon" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path v-if="!sidebarCollapsed" d="M12.5 4L7 10L12.5 16" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
            <path v-else d="M7.5 4L13 10L7.5 16" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
        </button>
      </div>

      <nav class="sidebar-nav">
        <router-link to="/" :class="{ active: $route.path === '/' }" :title="t('nav.overview')">
          <svg class="nav-icon" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M3 8.5L10 3L17 8.5" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M5 7.5V16C5 16.5523 5.44772 17 6 17H8.5V13C8.5 12.4477 8.94772 12 9.5 12H10.5C11.0523 12 11.5 12.4477 11.5 13V17H14C14.5523 17 15 16.5523 15 16V7.5" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
          <span class="nav-label">{{ t('nav.overview') }}</span>
        </router-link>
        <router-link to="/inventory" :class="{ active: $route.path === '/inventory' }" :title="t('nav.inventory')">
          <svg class="nav-icon" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M10 2.5L17 6.25V13.75L10 17.5L3 13.75V6.25L10 2.5Z" stroke="currentColor" stroke-width="1.5" stroke-linejoin="round"/>
            <path d="M3 6.25L10 10L17 6.25" stroke="currentColor" stroke-width="1.5" stroke-linejoin="round"/>
            <path d="M10 10V17.5" stroke="currentColor" stroke-width="1.5"/>
          </svg>
          <span class="nav-label">{{ t('nav.inventory') }}</span>
        </router-link>
        <router-link to="/orders" :class="{ active: $route.path === '/orders' }" :title="t('nav.orders')">
          <svg class="nav-icon" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
            <rect x="5" y="3.5" width="10" height="14" rx="1.5" stroke="currentColor" stroke-width="1.5"/>
            <path d="M7.5 3.5V2.75C7.5 2.33579 7.83579 2 8.25 2H11.75C12.1642 2 12.5 2.33579 12.5 2.75V3.5" stroke="currentColor" stroke-width="1.5"/>
            <path d="M7.5 8.5H12.5" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
            <path d="M7.5 11.5H12.5" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
            <path d="M7.5 14.5H10.5" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
          </svg>
          <span class="nav-label">{{ t('nav.orders') }}</span>
        </router-link>
        <router-link to="/spending" :class="{ active: $route.path === '/spending' }" :title="t('nav.finance')">
          <svg class="nav-icon" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M10 3V17" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
            <path d="M13.5 6.5C13.5 5.11929 12.0711 4 10 4C7.92893 4 6.5 5.11929 6.5 6.5C6.5 7.88071 7.92893 8.5 10 8.5C12.0711 8.5 13.5 9.11929 13.5 10.5C13.5 11.8807 12.0711 13 10 13C7.92893 13 6.5 11.8807 6.5 10.5" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
          </svg>
          <span class="nav-label">{{ t('nav.finance') }}</span>
        </router-link>
        <router-link to="/demand" :class="{ active: $route.path === '/demand' }" :title="t('nav.demandForecast')">
          <svg class="nav-icon" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M3 14L8 9L11.5 12.5L17 6" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M12.5 6H17V10.5" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
          <span class="nav-label">{{ t('nav.demandForecast') }}</span>
        </router-link>
        <router-link to="/reports" :class="{ active: $route.path === '/reports' }" title="Reports">
          <svg class="nav-icon" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M4 16V6" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
            <path d="M8 16V10" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
            <path d="M12 16V4" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
            <path d="M16 16V8" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
            <path d="M2 16H18" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
          </svg>
          <span class="nav-label">Reports</span>
        </router-link>
      </nav>

      <div class="sidebar-footer">
        <LanguageSwitcher />
        <ProfileMenu
          @show-profile-details="showProfileDetails = true"
          @show-tasks="showTasks = true"
        />
      </div>
    </aside>

    <div class="content-area">
      <header class="content-topbar">
        <FilterBar />
      </header>
      <main class="main-content">
        <router-view />
      </main>
    </div>

    <ProfileDetailsModal
      :is-open="showProfileDetails"
      @close="showProfileDetails = false"
    />

    <TasksModal
      :is-open="showTasks"
      :tasks="tasks"
      @close="showTasks = false"
      @add-task="addTask"
      @delete-task="deleteTask"
      @toggle-task="toggleTask"
    />
  </div>
</template>

<script>
import { ref, onMounted, computed } from 'vue'
import { api } from './api'
import { useAuth } from './composables/useAuth'
import { useI18n } from './composables/useI18n'
import FilterBar from './components/FilterBar.vue'
import ProfileMenu from './components/ProfileMenu.vue'
import ProfileDetailsModal from './components/ProfileDetailsModal.vue'
import TasksModal from './components/TasksModal.vue'
import LanguageSwitcher from './components/LanguageSwitcher.vue'

export default {
  name: 'App',
  components: {
    FilterBar,
    ProfileMenu,
    ProfileDetailsModal,
    TasksModal,
    LanguageSwitcher
  },
  setup() {
    const { currentUser } = useAuth()
    const { t } = useI18n()
    const showProfileDetails = ref(false)
    const showTasks = ref(false)
    const apiTasks = ref([])
    const sidebarCollapsed = ref(localStorage.getItem('sidebarCollapsed') === 'true')

    const toggleSidebar = () => {
      sidebarCollapsed.value = !sidebarCollapsed.value
      localStorage.setItem('sidebarCollapsed', sidebarCollapsed.value)
    }

    // Merge mock tasks from currentUser with API tasks
    const tasks = computed(() => {
      return [...currentUser.value.tasks, ...apiTasks.value]
    })

    const loadTasks = async () => {
      try {
        apiTasks.value = await api.getTasks()
      } catch (err) {
        console.error('Failed to load tasks:', err)
      }
    }

    const addTask = async (taskData) => {
      try {
        const newTask = await api.createTask(taskData)
        // Add new task to the beginning of the array
        apiTasks.value.unshift(newTask)
      } catch (err) {
        console.error('Failed to add task:', err)
      }
    }

    const deleteTask = async (taskId) => {
      try {
        // Check if it's a mock task (from currentUser)
        const isMockTask = currentUser.value.tasks.some(t => t.id === taskId)

        if (isMockTask) {
          // Remove from mock tasks
          const index = currentUser.value.tasks.findIndex(t => t.id === taskId)
          if (index !== -1) {
            currentUser.value.tasks.splice(index, 1)
          }
        } else {
          // Remove from API tasks
          await api.deleteTask(taskId)
          apiTasks.value = apiTasks.value.filter(t => t.id !== taskId)
        }
      } catch (err) {
        console.error('Failed to delete task:', err)
      }
    }

    const toggleTask = async (taskId) => {
      try {
        // Check if it's a mock task (from currentUser)
        const mockTask = currentUser.value.tasks.find(t => t.id === taskId)

        if (mockTask) {
          // Toggle mock task status
          mockTask.status = mockTask.status === 'pending' ? 'completed' : 'pending'
        } else {
          // Toggle API task
          const updatedTask = await api.toggleTask(taskId)
          const index = apiTasks.value.findIndex(t => t.id === taskId)
          if (index !== -1) {
            apiTasks.value[index] = updatedTask
          }
        }
      } catch (err) {
        console.error('Failed to toggle task:', err)
      }
    }

    onMounted(loadTasks)

    return {
      t,
      showProfileDetails,
      showTasks,
      tasks,
      addTask,
      deleteTask,
      toggleTask,
      sidebarCollapsed,
      toggleSidebar
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
  background: #f8fafc;
  color: #1e293b;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.app-shell {
  display: flex;
  height: 100vh;
  overflow: hidden;
}

/* Sidebar */
.sidebar {
  width: 260px;
  flex-shrink: 0;
  height: 100vh;
  position: sticky;
  top: 0;
  display: flex;
  flex-direction: column;
  background: #f8fafc;
  border-right: 1px solid #e2e8f0;
  overflow-y: auto;
  transition: width 0.2s ease;
}

.sidebar-brand {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 1.75rem 1.5rem 1.5rem;
}

.brand-mark {
  width: 36px;
  height: 36px;
  border-radius: 10px;
  background: #2563eb;
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 700;
  font-size: 1rem;
  flex-shrink: 0;
  letter-spacing: 0;
}

.brand-text {
  display: flex;
  flex-direction: column;
  gap: 0.125rem;
  min-width: 0;
}

.brand-text h1 {
  font-size: 1.125rem;
  font-weight: 700;
  color: #0f172a;
  letter-spacing: -0.025em;
  line-height: 1.25;
}

.subtitle {
  font-size: 0.75rem;
  color: #64748b;
  font-weight: 500;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.sidebar-toggle-row {
  display: flex;
  justify-content: flex-end;
  padding: 0 1rem 0.5rem;
}

.sidebar-toggle {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 28px;
  height: 28px;
  border-radius: 8px;
  border: 1px solid #e2e8f0;
  background: white;
  color: #64748b;
  cursor: pointer;
  flex-shrink: 0;
  transition: all 0.15s ease;
}

.sidebar-toggle:hover {
  color: #0f172a;
  background: #f1f5f9;
  border-color: #cbd5e1;
}

.toggle-icon {
  width: 16px;
  height: 16px;
}

.sidebar-nav {
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
  padding: 0.5rem 0.75rem;
  flex: 1;
}

.sidebar-nav a {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 0.75rem 1rem;
  color: #64748b;
  text-decoration: none;
  font-weight: 500;
  font-size: 0.9rem;
  border-radius: 8px;
  border-left: 3px solid transparent;
  transition: all 0.15s ease;
}

.sidebar-nav a .nav-icon {
  width: 20px;
  height: 20px;
  flex-shrink: 0;
}

.sidebar-nav a:hover {
  color: #0f172a;
  background: #f1f5f9;
}

.sidebar-nav a.active {
  color: #2563eb;
  background: #eff6ff;
  border-left-color: #2563eb;
}

.sidebar-footer {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  padding: 1rem 0.75rem;
  margin-top: auto;
  border-top: 1px solid #e2e8f0;
}

.sidebar-footer .language-switcher,
.sidebar-footer .profile-menu {
  width: 100%;
}

.sidebar-footer .language-button,
.sidebar-footer .profile-button {
  width: 100%;
  justify-content: flex-start;
}

.sidebar-footer .profile-name {
  flex: 1;
  min-width: 0;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  text-align: left;
}

.sidebar-footer .language-label {
  flex: 1;
  text-align: left;
}

.sidebar-footer .dropdown-menu {
  top: auto;
  bottom: calc(100% + 0.5rem);
  left: 0;
  right: 0;
  min-width: 0;
}

/*
 * Icon-only sidebar look, shared between the manual `.collapsed` toggle
 * and the forced narrow-viewport state in the media query below.
 * Keep both rule sets in sync if you change this look.
 */
.sidebar.collapsed {
  width: 76px;
}

.sidebar.collapsed .sidebar-brand {
  padding: 1.5rem 0 1rem;
  justify-content: center;
}

.sidebar.collapsed .brand-text {
  display: none;
}

.sidebar.collapsed .sidebar-toggle-row {
  justify-content: center;
  padding: 0 0 0.5rem;
}

.sidebar.collapsed .sidebar-nav a {
  justify-content: center;
  padding: 0.75rem;
}

.sidebar.collapsed .nav-label {
  display: none;
}

.sidebar.collapsed .sidebar-footer {
  align-items: center;
}

.sidebar.collapsed .sidebar-footer .language-label,
.sidebar.collapsed .sidebar-footer .profile-name,
.sidebar.collapsed .sidebar-footer .chevron {
  display: none;
}

.sidebar.collapsed .sidebar-footer .language-button,
.sidebar.collapsed .sidebar-footer .profile-button {
  justify-content: center;
  padding: 0.5rem;
}

/* Content area */
.content-area {
  flex: 1;
  min-width: 0;
  height: 100vh;
  overflow-y: auto;
  display: flex;
  flex-direction: column;
}

.content-topbar {
  position: sticky;
  top: 0;
  z-index: 90;
}

.main-content {
  flex: 1;
  width: 100%;
  padding: 2rem 2.5rem;
}

@media (max-width: 900px) {
  .sidebar {
    width: 76px;
  }

  .sidebar-brand {
    padding: 1.5rem 0 1rem;
    justify-content: center;
  }

  .brand-text {
    display: none;
  }

  .sidebar-toggle-row {
    justify-content: center;
    padding: 0 0 0.5rem;
  }

  .sidebar-toggle {
    display: none;
  }

  .sidebar-nav a {
    justify-content: center;
    padding: 0.75rem;
  }

  .nav-label {
    display: none;
  }

  .sidebar-footer {
    align-items: center;
  }

  .sidebar-footer .language-label,
  .sidebar-footer .profile-name,
  .sidebar-footer .chevron {
    display: none;
  }

  .sidebar-footer .language-button,
  .sidebar-footer .profile-button {
    justify-content: center;
    padding: 0.5rem;
  }
}

.page-header {
  margin-bottom: 1.5rem;
}

.page-header h2 {
  font-size: 1.875rem;
  font-weight: 700;
  color: #0f172a;
  margin-bottom: 0.375rem;
  letter-spacing: -0.025em;
}

.page-header p {
  color: #64748b;
  font-size: 0.938rem;
}

.stats-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 1.5rem;
  margin-bottom: 2rem;
}

.stat-card {
  background: white;
  padding: 1.5rem;
  border-radius: 14px;
  border: 1px solid rgba(226, 232, 240, 0.6);
  box-shadow: 0 4px 16px rgba(15, 23, 42, 0.06);
  transition: all 0.2s ease;
}

.stat-card:hover {
  box-shadow: 0 8px 24px rgba(15, 23, 42, 0.08);
}

.stat-label {
  color: #64748b;
  font-size: 0.875rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  margin-bottom: 0.625rem;
}

.stat-value {
  font-size: 2.25rem;
  font-weight: 700;
  color: #0f172a;
  letter-spacing: -0.025em;
}

.stat-card.warning .stat-value {
  color: #ea580c;
}

.stat-card.success .stat-value {
  color: #059669;
}

.stat-card.danger .stat-value {
  color: #dc2626;
}

.stat-card.info .stat-value {
  color: #2563eb;
}

.card {
  background: white;
  border-radius: 14px;
  padding: 1.75rem;
  border: 1px solid rgba(226, 232, 240, 0.6);
  box-shadow: 0 4px 16px rgba(15, 23, 42, 0.06);
  margin-bottom: 1.75rem;
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1.25rem;
  padding-bottom: 1rem;
  border-bottom: 1px solid #e2e8f0;
}

.card-title {
  font-size: 1.125rem;
  font-weight: 700;
  color: #0f172a;
  letter-spacing: -0.025em;
}

.table-container {
  overflow-x: auto;
}

table {
  width: 100%;
  border-collapse: collapse;
}

thead {
  background: #f8fafc;
  border-top: 1px solid #e2e8f0;
  border-bottom: 1px solid #e2e8f0;
}

th {
  text-align: left;
  padding: 0.75rem 1rem;
  font-weight: 600;
  color: #475569;
  font-size: 0.75rem;
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

td {
  padding: 0.75rem 1rem;
  border-top: 1px solid #f1f5f9;
  color: #334155;
  font-size: 0.875rem;
}

tbody tr {
  transition: background-color 0.15s ease;
}

tbody tr:hover {
  background: #f8fafc;
}

.badge {
  display: inline-block;
  padding: 0.313rem 0.75rem;
  border-radius: 6px;
  font-size: 0.75rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.025em;
}

.badge.success {
  background: #d1fae5;
  color: #065f46;
}

.badge.warning {
  background: #fed7aa;
  color: #92400e;
}

.badge.danger {
  background: #fecaca;
  color: #991b1b;
}

.badge.info {
  background: #dbeafe;
  color: #1e40af;
}

.badge.increasing {
  background: #d1fae5;
  color: #065f46;
}

.badge.decreasing {
  background: #fecaca;
  color: #991b1b;
}

.badge.stable {
  background: #e0e7ff;
  color: #3730a3;
}

.badge.high {
  background: #fecaca;
  color: #991b1b;
}

.badge.medium {
  background: #fed7aa;
  color: #92400e;
}

.badge.low {
  background: #dbeafe;
  color: #1e40af;
}

.loading {
  text-align: center;
  padding: 3rem;
  color: #64748b;
  font-size: 0.938rem;
}

.error {
  background: #fef2f2;
  border: 1px solid #fecaca;
  color: #991b1b;
  padding: 1rem;
  border-radius: 8px;
  margin: 1rem 0;
  font-size: 0.938rem;
}
</style>
