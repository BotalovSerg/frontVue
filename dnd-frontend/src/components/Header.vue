<!-- Header.vue -->
<template>
  <header class="header">
    <div class="container">
      <div class="header-content">
        <router-link to="/" class="logo">
          <h1>DndLab</h1>
        </router-link>

        <nav :class="['nav', { active: isMenuOpen }]">
          <ul class="nav-list">
            <li v-for="link in navLinks" :key="link.to" class="nav-item">
              <router-link :to="link.to" class="nav-link" active-class="active" @click="closeMenu">
                {{ link.text }}
              </router-link>
            </li>
          </ul>
        </nav>

        <button class="menu-toggle" @click="toggleMenu" aria-label="Меню">
          <span v-if="!isMenuOpen">☰</span>
          <span v-else>✕</span>
        </button>
      </div>
    </div>
  </header>
</template>

<script setup>
import { ref } from 'vue'

const isMenuOpen = ref(false)

const navLinks = [
  { to: '/', text: 'Главная' },
  { to: '/about', text: 'О нас' },
  { to: '/services', text: 'Услуги' },
  { to: '/contact', text: 'Контакты' },
]

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
}

const closeMenu = () => {
  isMenuOpen.value = false
}
</script>

<style scoped>
.header {
  background-color: #2c3e50;
  color: white;
  padding: 1rem 0;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 1.5rem;
}

.header-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
}

.logo h1 {
  margin: 0;
  font-size: 1.5rem;
  color: white;
  text-decoration: none;
}

.logo:hover h1 {
  color: #3498db;
}

.nav {
  display: flex;
  align-items: center;
}

.nav-list {
  display: flex;
  list-style: none;
  margin: 0;
  padding: 0;
  gap: 2rem;
}

.nav-item {
  display: inline;
}

.nav-link {
  color: white;
  text-decoration: none;
  font-size: 1rem;
  transition: color 0.3s;
  padding: 0.5rem 0;
}

.nav-link:hover,
.nav-link.active {
  color: #3498db;
}

.menu-toggle {
  display: none;
  background: none;
  border: none;
  color: white;
  font-size: 1.5rem;
  cursor: pointer;
}

@media (max-width: 768px) {
  .nav {
    width: 100%;
    display: none;
  }

  .nav.active {
    display: block;
    margin-top: 1rem;
  }

  .nav-list {
    flex-direction: column;
    gap: 1rem;
    align-items: center;
  }

  .menu-toggle {
    display: block;
  }
}
</style>
