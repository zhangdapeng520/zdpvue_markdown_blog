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
import JSZip from 'jszip';
import {saveAs} from 'file-saver';

const options = {weekday: 'long', year: 'numeric', month: 'long', day: 'numeric'};
// @ts-ignore | ts bug: https://github.com/microsoft/TypeScript/issues/40806
const todayStr = new Date().toLocaleDateString("en-US", options);

const text = `# 请填写博客标题 😎
## 副标题

> 一些内容

其他的内容。。。
`;

const onSave = (text: string, html: string) => {
  const postTitle = `post_${todayStr.replace(/,/mg, '').replace(/\s/mg, '_')}`;
  const zip = new JSZip();
  zip.file(`${postTitle}_source.md`, text);
  zip.file(`${postTitle}_content.html`, `<!DOCTYPE html>
    <html>
      <head>
        <meta charset="UTF-8" />
        <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.6.2/dist/css/bootstrap.min.css" integrity="sha384-xOolHFLEh07PJGoPkLv1IbcEPTNtaed2xpHsD9ESMhqIYd0nLMwNLD69Npy4HI+N" crossorigin="anonymous">
      </head>
      <body>
        <div class="container p-5 mx-auto">
          ${html}
        </div>
      </body>
    </html>`);
  zip.generateAsync({type: "blob"})
      .then(function (content) {
        // see FileSaver.js
        saveAs(content, `${postTitle}.zip`);
      });
}
</script>
