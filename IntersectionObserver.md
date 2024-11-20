# 作用

他提供了一种异步观察目标元素与其祖先元素或窗口的指定区域是否发生碰撞的方法。其祖先元素或窗口被称为根。且在实例化完成后就不能更改他的配置。可以配置监听多个目标元素。当目标元素与根的指定区域发生碰撞后就会执行回调函数，回调函数的参数会指出有哪些目标元素与根发生了碰撞，有哪些没有发生碰撞。

# 示例

```javascript
const intersectionObserver = new IntersectionObserver((entries) => {
  // 如果 intersectionRatio 为 0，则目标在视野外，
  // 我们不需要做任何事情。
  if (entries[0].intersectionRatio <= 0) return;

  // do something...
});

// 开始监听
intersectionObserver.observe(document.querySelector(".target-element"));
// 取消监听
intersectionObserver.unobserve(document.querySelector(".target-element"));

```

# 使用场景

1、资源的懒加载。比如只有当指定元素进入可视范围之后，才去加载资源
2、元素的显示/隐藏。只有在指定元素进入可视范围内时，才展示数据；离开可视区域即隐藏。如果页面上的数据量较大，也可考虑使用此种方法移除不可见元素以提升性能
