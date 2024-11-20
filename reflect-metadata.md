# 作用

主要用来声明时添加和读取元数据，通常是配合装饰器一起使用。需要在程序的入口添加 `import "reflect-metadata"`。

# 获取类型信息

```typescript
function Parameter() {
  return (target: any, methodName: any, parameterIndex: number) => {
    // 如果是加在构造函数上，methodName为undefined，如果是在普通方法上则methodName是那个方法的名字
    console.log(methodName, parameterIndex); // undefined 1
    // 此处获取到的其实是这个方法的类型，如果是构造函数的话则为undefined
    console.log(Reflect.getMetadata("design:type", target, methodName));
    // 此处获取到的是这个方法的入参类型，结合parameterIndex就可以知道当前位置的入参的类型
    console.log(Reflect.getMetadata("design:paramtypes", target, methodName));// [ [Function: String], [class SomeClass], [Function: Boolean] ]
  };
}

function Prop() {
  // target是类的原型,SomeClass.prototype
  return (target: any, key: string) => {
    const type = Reflect.getMetadata('design:type', target, key);
    console.log(`${key} type: ${type.name}`); // Aprop type: string
  };
}

function Class() {
  return (target: any) => {
    const types = Reflect.getMetadata('design:paramtypes', target);// 获取方法的参数类型，此处获取构造函数的入参类型，可以指定方法名
    console.log(types.map(type => type.name));// ["String","SomeClass","Boolean"]
  };
}

@Class()
class SomeClass {
  @Prop()
  Aprop!: string;

  constructor(a: string, @Parameter() b: SomeClass, c: Boolean) {
  }
}
```

# 碰到的问题

1、在浏览器里，`Reflect.getMetadata("design:xxx", target)`获取不到类型，只返回undefined；在nodejs里则可以正常获取
2、需要注意装饰器的执行顺序，参数>方法>属性>类，并且同一类型的装饰器是后声明的先执行。
