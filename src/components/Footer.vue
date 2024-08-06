<template>
  <div
      class="text-center py-2"
      :style="`background-color: ${VUE_APP_FOOTER_BG_CSS_COLOR}; color: ${VUE_APP_FOOTER_TEXT_CSS_COLOR};`"
  >
    <p class="m-0 p-0">
      版权所有 &copy;
      <a
          href="https://github.com/zhangdapeng520"
          target="_blank"
          class="text-reset">
        张大鹏
      </a>
    </p>
  </div>
</template>

<script setup lang="ts">
import {version} from '../../package.json'
import blogConfig from '../blog_config'

const {VUE_APP_FOOTER_BG_CSS_COLOR = 'darkgray', VUE_APP_FOOTER_TEXT_CSS_COLOR = 'white'} = blogConfig
</script>
