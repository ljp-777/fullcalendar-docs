---
title: Typescript 支持
#title: TypeScript Support
title_for_landing: TypeScript
excerpt_separator: <!--more-->
---

可以将Fullcalendar、[Scheduler](/pricing)跟**TypeScript**（JavaScript语言的超集）一起使用。<!--more-->TypeScript非常适合维护大型JavaScript项目，然而对于小型项目，它有点大才小用。[学习关于TypeScript &raquo;](https://www.typescriptlang.org/)
<!--It is possible to use FullCalendar and [Scheduler](/pricing) with **TypeScript**, a type-aware superset of the JavaScript language that compiles down to JavaScript. TypeScript is great for the maintainability of large JavaScript projects, however, it is probably overkill for smaller projects. [Learn more about TypeScript &raquo;](https://www.typescriptlang.org/)-->

你需要设置某种构建系统，将TypeScript编辑为Javascript。你可以使用`tsc`直接编译，或者使用复杂的系统如[Webpack](https://webpack.js.org/)。
<!--You will then need to set up some sort of build system that compiles TypeScript to JavaScript. You can use the `tsc` compiler directly or you can use a more sophisticated system like [Webpack](https://webpack.js.org/).-->

- [查看 **FullCalendar + TypeScript + Webpack** 示例仓库 &raquo;](https://github.com/fullcalendar/fullcalendar-examples/tree/main/typescript)
- [查看 **FullCalendar Scheduler + TypeScript + Webpack** 示例仓库 &raquo;](https://github.com/fullcalendar/fullcalendar-examples/tree/main/typescript-scheduler)


一旦有了自己的构建系统，你可以写具备类型感知的代码：
<!--Once you have your build system set up, you can begin to write type-aware code like this:-->

**示例.ts**:

```ts
import { Calendar } from '@fullcalendar/core';
import dayGridPlugin from '@fullcalendar/daygrid';

document.addEventListener('DOMContentLoaded', function() {
  let calendarEl: HTMLElement = document.getElementById('calendar')!;

  let calendar = new Calendar(calendarEl, {
    plugins: [ dayGridPlugin ]
    // options here
  });

  calendar.render();
});
```
