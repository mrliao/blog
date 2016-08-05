### weex 学习

### 安装
* npm install -g weex-toolkit 

### 使用
* touch hello.we
`<template>
    <div>
        <text>Hello Weex</text>
    </div>
</template>
`
* weex hello.we
* 浏览 `http://127.0.0.1:1236/weex_tmp/h5_render/?hot-reload_controller&page=hello.js&loader=xhr`
page 需要根据文件来设置的，带hot-reload_controller 为热加载
