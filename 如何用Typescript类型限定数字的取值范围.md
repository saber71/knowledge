# 如何用Typescript类型限定数字的取值范围

```typescript
// 使用递归的条件类型
export type Enumerate<
  T extends number,
  R extends number[] = [],
> = R["length"] extends T ? R[number] : Enumerate<T, [R["length"], ...R]>;

// [min,max), only integer
export type RangeNumber<Min extends number, Max extends number> = Exclude<
  Enumerate<Max>,
  Enumerate<Min>
>;

// [min,max], only integer
export type RangeMaxInclude<Min extends number, Max extends number> = Exclude<
  Enumerate<Max> | Max,
  Enumerate<Min>
>;

// (min,max), only integer
export type RangeMinExclude<Min extends number, Max extends number> = Exclude<
  Enumerate<Max>,
  Enumerate<Min> | Min
>;

// 0.1 | 0.2 ... 0.999 | 1.0
type AlphaChannel = `0.${Enumerate<999>}` | "0.999" | "1.0";
type AlphaValue<T extends number> = `${T}` extends AlphaChannel ? T : never;
```
