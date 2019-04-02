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
    > **注意，v-show 不支持 <template> 元素，也不支持 v-else**

* v-for refs
    > When ref is used together with v-for, the ref you get will be an array containing the child components mirroring the data source. **But take note that v-for refs do not guarantee the same order as your source Array.**
    [讨论](https://github.com/vuejs/vue/issues/4952)