# 四月

## 01
* [vue组件之间的循环引用](https://cn.vuejs.org/v2/guide/components-edge-cases.html#%E7%BB%84%E4%BB%B6%E4%B9%8B%E9%97%B4%E7%9A%84%E5%BE%AA%E7%8E%AF%E5%BC%95%E7%94%A8)
    1. beforeCreate 
    ```javascript
        beforeCreate: () => {
            this.$options.components.xxxx = require('./xxxx.vue').default
        }
    ```
    2. webpack 异步import
    ```javascript
        components: {
            xxx: () => import('./xxx.vue')
        }
    ```
 
* v-show
  > **注意 v-show不支持```<template>```, 也不支持 v-else**
    

* [v-for refs](https://cn.vuejs.org/v2/guide/components-edge-cases.html#%E8%AE%BF%E9%97%AE%E5%AD%90%E7%BB%84%E4%BB%B6%E5%AE%9E%E4%BE%8B%E6%88%96%E5%AD%90%E5%85%83%E7%B4%A0)
    > When ref is used together with v-for, the ref you get will be an array containing the child components mirroring the data source. **But take note that v-for refs do not guarantee the same order as your source Array.**  
   
   [讨论](https://github.com/vuejs/vue/issues/4952) 


## 25
* get latest version of package
    - npm show {pkg} version
    ``` javascript
        const exec = require('child_process').execSync;
        let version = exec(`npm show ${pkg} version`);
    ```
    - latest-version
    ``` javascript
        const latestVersion = require('lastest-verion');
        async function getPkgLastestVersion(pkg) {
            return await lastestVersion(pkg);
        }
    ```
