---
title: 使用ES6构建系统初始化
excerpt_separator: <!--more-->
---

对于复杂的项目，推荐使用ES6兼容构建系统如[Webpack](https://webpack.js.org/)或者[Rollup](https://rollupjs.org)。配合一个包管理器如[NPM](https://www.npmjs.com/) 或[Yarn](https://yarnpkg.com)。<!--more-->这样的安装会确保重要的文件构建在一起，打包到一个包里。你不需要担心在页面中手动引入`<script>`标签。

<!--For non-trivial projects, it is recommended to use an ES6-compatible build system like [Webpack](https://webpack.js.org/) or [Rollup](https://rollupjs.org) along with a package manager like [NPM](https://www.npmjs.com/) or [Yarn](https://yarnpkg.com). A setup like this will ensure all necessary files are compiled together into a unified bundle. You won't need to worry about manually including `<script>` tags on the page.-->

示例仓库

- [查看 **Webpack** 示例仓库 &raquo;](https://github.com/fullcalendar/fullcalendar-examples/tree/main/webpack)
- [查看 **Rollup** 示例仓库 &raquo;](https://github.com/fullcalendar/fullcalendar-examples/tree/main/rollup)


## 使用插件初始化Calendar
<!--## Initialize a Calendar with Plugins-->

FullCalendar的功能被拆分到插件里([查看插件列表](plugin-index))。如果你需要插件提供的功能时，才将其包含在内，否则你可以省略该插件，避免将其打包到资源包中，从而节省空间。默认情况下，FullCalendar的最小核心不具备任何功能。你至少*需要*使用插件来显示日历。
<!--FullCalendar's functionality is broken up into "plugins" ([see a full list](plugin-index)). You only include a plugin if you need the features it provides, otherwise, you can omit the plugin and prevent it from being compiled into your bundle, saving space. By default, the bare core of FullCalendar does not do *anything*. You'll *need* to use a plugin to display a calendar view at the very least.-->

首先，使用NPM或Yarn安装`core`包以及你计划使用的插件：
<!--First, use NPM or Yarn to install the `core` package along with any plugins you plan to use:-->

```
npm install \
  @fullcalendar/core \
  @fullcalendar/daygrid \
  @fullcalendar/timegrid \
  @fullcalendar/list
```
然后，导入插件并将它们提供给新的`Calendar`实例：
<!--Then, import your plugins and supply them to a new `Calendar` instance:-->

```js
import { Calendar } from '@fullcalendar/core';
import dayGridPlugin from '@fullcalendar/daygrid';
import timeGridPlugin from '@fullcalendar/timegrid';
import listPlugin from '@fullcalendar/list';

let calendarEl = document.getElementById('calendar');
let calendar = new Calendar(calendarEl, {
  plugins: [ dayGridPlugin, timeGridPlugin, listPlugin ],
  initialView: 'dayGridMonth',
  headerToolbar: {
    left: 'prev,next today',
    center: 'title',
    right: 'dayGridMonth,timeGridWeek,listWeek'
  }
});
calendar.render();
```

## 高级插件
<!--## Premium Plugins-->
安装[高级插件](premium)的方法类似。你需要安装`core`包，`resource`包，还有你计划使用的任何高级插件
<!--The set of [premium plugins](premium) works in the same way. You'll need to install the `core` package, the `resource` package, and any premium plugins you plan to use.-->

```
npm install --save \
  @fullcalendar/core \
  @fullcalendar/resource \
  @fullcalendar/resource-timeline
```
然后，导入插件并将它们提供给新的`Calendar`实例：
<!--Then, import your plugins and supply them to a new `Calendar` instance:-->

```js
import { Calendar } from '@fullcalendar/core';
import resourceTimelinePlugin from '@fullcalendar/resource-timeline';

let calendarEl = document.getElementById('calendar');
let calendar = new Calendar(calendarEl, {
  plugins: [ resourceTimelinePlugin ],
  initialView: 'resourceTimeline',
  resources: [
    // your resource list
  ]
});
calendar.render();
```

示例仓库

- [查看 **Webpack** + **Scheduler** 示例仓库 &raquo;](https://github.com/fullcalendar/fullcalendar-examples/tree/main/webpack-scheduler)
- [查看 **Rollup** + **Scheduler** 示例仓库 &raquo;](https://github.com/fullcalendar/fullcalendar-examples/tree/main/rollup-scheduler)
