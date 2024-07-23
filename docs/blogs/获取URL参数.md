---
title: 获取URL参数
date: 2024-7-24
categories:
  - 前端
tags:
  - JavaScript
---
> 从地址栏中获取URL参数并将其作为对象返回
```javascript
// 定义一个函数用于获取URL中的所有查询参数，并将它们转换为一个JavaScript对象
function getUrlParameters() {
  // 创建一个URLSearchParams对象，该对象用于解析URL的查询字符串
  const searchParams = new URLSearchParams(window.location.search);

  // 使用Array.from或扩展运算符(...)将searchParams.entries()转换为数组，
  // 这样可以使用数组方法reduce处理每一项查询参数
  const paramsObject = [...searchParams.entries()].reduce(
    // reduce方法接收一个回调函数，用于累积数组元素
    // 第一个参数acc是累加器，初始化为一个空对象{}
    // 第二个参数是一个数组，包含查询参数的键(key)和值(value)
    (acc, [key, value]) => {
      // 将查询参数的键和值添加到累加器对象中
      // 每次迭代都会更新累加器，最终形成一个包含所有查询参数的对象
      acc[key] = value;

      // 返回更新后的累加器，供下次迭代使用
      return acc;
    },

    // reduce的第二个参数是初始值，这里是一个空对象，
    // 函数执行完毕后，此对象将包含所有的查询参数
    {}
  );

  // 函数返回包含所有查询参数的对象
  return paramsObject;
}
```