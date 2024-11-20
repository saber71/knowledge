# 常见错误种类

1. SyntaxError：语法错误，无法被捕获
2. TypeError：当代码中的变量参数等类型不对时抛出。常见于试图对一个不是函数的变量/属性进行函数调用时被抛出
3. ReferenceError：引用错误，当试图访问一个空值的属性时抛出
4. RangeError：取值范围错误，当给某个对象指定一个超出取值范围的值时抛出。比如给Array对象传入一个不合法的长度参数时抛出（`Array(-1)`）
5. URIError：当使用URI相关函数处理数据时，如果传入参数不正确时抛出。例如decodeURI、decodeURIComponent、encodeURI、encodeURIComponent
6. EvalError：当eval函数执行代码发生错误时抛出。目前推荐不使用eval函数。

# 自定义错误类型

```typescript
export class NotFoundError extends Error {
  constructor(message: string) {
    super(message);
    this.name = "NotFoundError";
  }
}

// 使用
throw new NotFoundError("找不到值")

```
