<template>
  <form class="p-3">
    <div class="form-group">
      <label for="title">标题</label>
      <input type="text" class="form-control" id="title">
    </div>
    <div class="form-group">
      <label for="category">分类</label>
      <select id="category" class="form-control">
        <option selected>Python</option>
        <option>Golang</option>
      </select>
    </div>
    <div class="form-group">
      <label for="description">描述</label>
      <textarea class="form-control" id="description" rows="3"></textarea>
    </div>
    <div class="form-group">
      <label for="content">内容</label>
      <v-md-editor v-model="text" @save="onSave" height="100vh"
                   :right-toolbar="'preview sync-scroll fullscreen'"></v-md-editor>
    </div>
    <button type="submit" class="btn btn-primary">保存</button>
  </form>

</template>

<script setup lang="ts">
const text = `# 请填写博客标题 😎
## 副标题

> 一些内容

其他的内容。。。
`;

const onSave = (text: string, html: string) => {
  alert("保存成功")
}
</script>
