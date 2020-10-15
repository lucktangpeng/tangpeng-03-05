1、Vue 3.0 性能提升主要是通过哪几方面体现的？

- 大幅提升运行时的性能 重写虚拟Dom，效果提升百分之三十以上
  - 跳过静态节点，只处理动态节点
  - 静态节点渲染一次就不再进行处理，所以处理的数据量会有大幅度的降低，从而大幅度提升性能
- 用proxy优化了响应式处理

2、Vue 3.0 所采用的 Composition Api 与 Vue 2.x使用的Options Api 有什么区别？

- Options API 一个功能需要在不同的vue配置项中定义属性和方法，在大型项目中不容易分清对应功能的属性方法的位置
- Composition Api 是根据逻辑功能来组织的，将同个功能的方法属性都放在一个代码块中，即使功能很多也能快速定位功能逻辑代码

3、Proxy 相对于 Object.defineProperty 有哪些优点？

- proxy 可以直接监听对象而非属性
- proxy 可以直接监听数组的变化
- Proxy 有多达 13 种拦截方法

4、Vue 3.0 在编译方面有哪些优化？

- 直接把静态节点抽离出去，她只会编译阶段创建一边，之后直接复用对象，不需要再创建

5、Vue.js 3.0 响应式系统的实现原理？

- reactive

  - 接受一个参数，判断参数是否是对象，不是对象直接返回这个参数，不做响应式处理
  - 创建拦截器对象 handler 设置get/set/deleteProperty
    - get
      - 收集依赖
      - 返回当前key值
    - set
      - 设置的新值和老值不相等时，更新为新值，并触发更新
    - deleteProperty
      - 当前对象这个Key的时候，删除这个key并触发更新
  - 返回Proxy对象

- effect

  - 收一个函数作为参数。作用是：访问响应式对象属性时去收集依赖

- track

  - 接受两个参数target 和key
  - 如果没有acticeEffect,则说明没有创建effect依赖
  - 如果有 acticeEffect, 则去判断WeakMap 集合中是否有target属性

- trigger

  - 判断WeakMap 中是否有target属性
    - WeakMap 中没有 target 属性，则没有 target 相应的依赖
    - WeakMap 中有 target 属性，则判断 target 属性的 map 值中是否有 key 属性，有的话循环触发收集的 effect()

  

