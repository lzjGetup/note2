# 创建vue项目

1. 检查nodejs环境 `node -v`,nodejs要求的版本至少要求18.0
2. `npm create vue@latest`创建项目,初始化名字,和基本配置
3. `npm run dev`运行vue3项目


# 目录结构
>![[Pasted image 20231226120949.png]]

# 使用element-plus

1. 使用npm下载
```npm
npm install element-plus --save
```

2. 起步配置
先参考官网起步
```txt
App.vue
<template>
  <el-button>我是 ElButton</el-button>
</template>
<script>
  import { ElButton } from 'element-plus'
  export default {
    components: { ElButton },
  }
</script>

vite.config.js
import { defineConfig } from 'vite';
import vue from '@vitejs/plugin-vue';
import AutoImport from 'unplugin-auto-import/vite';
import Components from 'unplugin-vue-components/vite';
import { ElementPlusResolver } from 'unplugin-vue-components/resolvers';
import ElementPlus from 'unplugin-element-plus/vite';

export default defineConfig({
  plugins: [
    ElementPlus(),
    vue(),
    AutoImport({
      resolvers: [ElementPlusResolver()],
    }),
    Components({
      resolvers: [ElementPlusResolver()],
    }),
  ],
  resolve: {
    alias: {
      '@': '/src' // 你的源代码路径
    }
  },
  css: {
    modules: {
      localsConvention: 'camelCase' // 如果你使用了CSS模块，可以添加这个配置
    }
  }
});

jsconfig.json
{
  "compilerOptions": {
    "paths": {
      "@/*": ["./src/*"]
    }
  },
  "types": ["element-plus/global"],
  "exclude": ["node_modules", "dist"]
}

main.js
import { createApp } from 'vue'
import ElementPlus from 'element-plus'
import 'element-plus/dist/index.css'
import App from './App.vue'
const app = createApp(App)
app.use(ElementPlus)
app.mount('#app')
```

# 使用Axios
1. 安装
`npm install axios`

2. 在当前vue组件导入
`import axios from 'axios';`


# 打包vue项目

```sh
npm run build
```


# 查看某端口

```sh
netstat -ano | findstr :端口号
```









