# vue-manage项目笔记

1、创建项目

vue create vue-manage

- 切换淘宝下载源

cnpm config set registry ....

- Element ui的地址

​	https://element.eleme.cn/#/zh-CN

- element-ui的使用

  - 下载element-ui

    - npm i element-ui -S

  - 引入element-ui  并且引入样式文件

    ```js
    import Vue from 'vue'
    import App from './App.vue'
    //引入element-ui
    import ElementUI from 'element-ui';
    //引入element-ui样式文件
    import 'element-ui/lib/theme-chalk/index.css';
    
    
    Vue.config.productionTip = false
    //将elementui注册为全局组件
    Vue.use(ElementUI)
    
    new Vue({
      render: h => h(App),
    }).$mount('#app')
    ```

- element-ui的按需引入

  - ```js
    import Vue from 'vue'
    import App from './App.vue'
    //引入element-ui
    import {Button} from 'element-ui';
    //引入element-ui样式文件
    import 'element-ui/lib/theme-chalk/index.css';
    
    
    Vue.config.productionTip = false
    //将elementui注册为全局引入组件
    Vue.use(Button)
    
    new Vue({
      render: h => h(App),
    }).$mount('#app')
    
    ```

- 路由切换方法

```js
    clickMenu(item) {
      this.$router.push({
        name: item.name
      })
    }
```

## axios

### 特性：

- 从浏览器中创建XMLHttpRequests
- 从node.js创建http请求
- 支持Promise API
- 拦截请求和响应
- 转换请求数据和响应数据
- 取消请求
- 自动转换JSON数据
- 客户端支持防御XSRF
