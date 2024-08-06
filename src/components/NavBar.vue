<template>
  <nav
      class="navbar navbar-expand-md navbar-light mb-0"
      :style="`background-color: ${VUE_APP_NAVBAR_BG_CSS_COLOR}; color: ${VUE_APP_NAVBAR_TEXT_CSS_COLOR};`"
  >
    <router-link
        class="navbar-brand"
        :to="'/'"
        :style="`color: ${VUE_APP_NAVBAR_TEXT_CSS_COLOR};`"
    >
      {{ title }}
    </router-link>
    <button
        :class="`navbar-toggler collapsed`"
        type="button"
        aria-label="Toggle navigation"
        @click.prevent="showDropdown = !showDropdown"
    >
      <span
          class="navbar-toggler-icon"
          :style="`background-color: ${VUE_APP_NAVBAR_TEXT_CSS_COLOR};`"
      />
    </button>

    <div
        id="navbarNavDropdown"
        class="navbar-collapse"
    >
      <ul class="navbar-nav ml-auto top-right"
          @focusout="focusOut"
          tabindex="1">
        <li class="category">Python</li>
        <li class="category">Golang</li>
        <li class="nav-item">
          <router-link
              class="nav-link border rounded py-2 px-3 mr-2"
              :to="'/login'"
              :style="`color: ${VUE_APP_NAVBAR_TEXT_CSS_COLOR};`"
          >
            登录
          </router-link>
        </li>
        <li v-if="router.currentRoute.value.path !== '/editor'" class="nav-item">
          <router-link
              class="nav-link border rounded py-2 px-3"
              :to="'/editor'"
              :style="`color: ${VUE_APP_NAVBAR_TEXT_CSS_COLOR};`"
          >
            写作
          </router-link>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script setup lang="ts">
import {ref} from 'vue';
import blogConfig from '../blog_config'
import router from '../router';

const {VUE_APP_NAVBAR_BG_CSS_COLOR = 'black', VUE_APP_NAVBAR_TEXT_CSS_COLOR = 'white'} = blogConfig

defineProps({
  title: {
    type: String,
    default: ''
  },
  sections: {
    type: Object,
    default: () => ({})
  }
});

const showDropdown = ref(false)

const focusOut = ({relatedTarget}: any) => {
  if (!(Array.from(relatedTarget?.classList ?? []).includes('dropdown-item'))) {
    showDropdown.value = false
  }
}
</script>

<style scoped>
.top-right {
  display: flex;
  align-items: center;
  justify-content: center;
}

.top-right .category {
  margin-right: 15px;
}

.top-right .category:hover {
  color: cornflowerblue;
  cursor: pointer;
}
</style>
