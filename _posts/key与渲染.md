---
title: 7月开发记录
date: 2020-07-03 22:48:09
tags: 开发
---

### key与渲染

做图表时候引入了第三方库 [vue-grid-layout](https://github.com/jbaysolutions/vue-grid-layout) 来支持自定义布局，但是会出现切换页签+改变窗口尺寸=图表重叠的bug。看了一下源码，发现是 containerWidth 这个值更新出现了异常。旋即想到的方法是直接重新更新，或者重新渲染组件。然后想到了改变key值来渲染组件的方法。

![](https://i.loli.net/2020/07/11/BdW1bnNkAXe7xTQ.png)

直接在组件绑定了 `:key="$route.name"` 当页签切换时，重新渲染一遍来保证 containerWidth 的正确更新，来防止图标重叠。