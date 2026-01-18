<script setup>
import { ref, onMounted } from 'vue'

const isOpen = ref(false)
const button = ref(null)
const menu = ref(null)
const links = ref([])

function toggleMenu() {
  isOpen.value = !isOpen.value

  if (isOpen.value) {
    button.value.setAttribute('aria-expanded', 'true')
    menu.value.setAttribute('aria-hidden', 'false')
    links.value.forEach(link => link.setAttribute('tabindex', '0'))
  } else {
    button.value.setAttribute('aria-expanded', 'false')
    menu.value.setAttribute('aria-hidden', 'true')
    links.value.forEach(link => link.setAttribute('tabindex', '-1'))
  }
}

onMounted(() => {
  links.value = Array.from(menu.value.querySelectorAll('.menu-link'))
})
</script>

<template>
  <div class="dropdown-container">
    <button
        ref="button"
        class="button"
        :class="{ active: isOpen }"
        aria-expanded="false"
        aria-controls="list"
        @click="toggleMenu"
    >
      Меню
    </button>

    <ul ref="menu" class="menu" id="list" aria-hidden="true">
      <li class="menu-item">
        <a href="#" class="menu-link" tabindex="-1">один</a>
      </li>
      <li class="menu-item">
        <a href="#" class="menu-link" tabindex="-1">дыва</a>
      </li>
      <li class="menu-item">
        <a href="#" class="menu-link" tabindex="-1">три</a>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.dropdown-container {
  width: 100%;
  height: 20%;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
}

.button {
  inline-size: 100%;
  padding: 0.5lh 1.5lh;
  font: inherit;
  color: currentColor;
  background-color: #f28482;
  border: none;
  cursor: pointer;
  transition: background-color 0.3s;
}

.button:hover,
.button:focus-visible {
  background-color: #f5cac3;
}

.menu {
  position: relative;
  display: grid;
  margin-block-start: 0.5lh;
  background-color: #f28482;

  overflow: hidden;
  line-height: 0;
  color: transparent;
  transition: line-height 0.5s, color 0.5s;
}

.menu-item {
  overflow: hidden;
}

.menu-link {
  display: block;
  padding: 0.5lh 1.5lh;
  text-decoration: none;
  color: black;
}

.menu-link:hover,
.menu-link:focus-visible {
  background-color: #f5cac3;
}

.button.active ~ .menu {
  line-height: 1.2;
  color: currentColor;
}
</style>
