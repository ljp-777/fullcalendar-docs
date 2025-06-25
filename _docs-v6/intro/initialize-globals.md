---
title: 使用Script标签初始化
description: 使用预构建包和HTML的script😊
# title: Initialize with Script Tags
# description: Use pre-built bundles and HTML script tags
---

你可以在HTML的头部手动引入必要的`<script>`标签，然后使用浏览器的全局变量进行初始化。利用FullCalendar的构建包或单独包含插件之一。
<!--It's possible to manually include the necessary `<script>` tags in the head of your HTML page and then initialize a calendar via browser globals. Leverage one of FullCalendar's prebuilt bundles or include individual plugins-->

## 标准构建包
<!--## Standard Bundle-->

首先，通过以下的几种方式获取`fullcalendar`的标准构建包
<!--First, obtain the standard `fullcalendar` bundle in one of the following ways:-->

- **Download**: <a href='{{ site.fullcalendar_repo }}/releases/download/v{{ site.data.latest-releases.v6 }}/fullcalendar-{{ site.data.latest-releases.v6 }}.zip'>fullcalendar-{{ site.data.latest-releases.v6 }}.zip</a>
- **CDN:** [jsdelivr](https://www.jsdelivr.com/package/npm/fullcalendar?version={{ site.data.latest-releases.v6 }})
- **NPM:** `npm install fullcalendar`

然后，编写如下的初始化代码：
<!--Then, write the following initialization code:-->

```html
<!DOCTYPE html>
<html lang='en'>
  <head>
    <meta charset='utf-8' />
    <script src='https://cdn.jsdelivr.net/npm/fullcalendar@{{ site.data.latest-releases.v6 }}/index.global.min.js'></script>
    <script>

      document.addEventListener('DOMContentLoaded', function() {
        var calendarEl = document.getElementById('calendar');
        var calendar = new FullCalendar.Calendar(calendarEl, {
          initialView: 'dayGridMonth'
        });
        calendar.render();
      });

    </script>
  </head>
  <body>
    <div id='calendar'></div>
  </body>
</html>
```
[查看可运行的例子 &raquo;](initialize-globals-demo)
<!--[View a runnable example &raquo;](initialize-globals-demo)-->

`fullcalendar`构建包的`index.global(.min).js`文件包含以下的包：
<!-- The `fullcalendar` bundle's `index.global(.min).js` file includes the following packages:-->

- `@fullcalendar/core`
- `@fullcalendar/interaction` (功能： [日期选择](date-clicking-selecting), [拖拽事件，大小变化事件](event-dragging-resizing))
- `@fullcalendar/daygrid` (功能：[月视图](month-view) 和 [日视图](daygrid-view))
- `@fullcalendar/timegrid` (功能： [timeGrid](timegrid-view) views)
- `@fullcalendar/list` (功能： [list views](list-view))
- `@fullcalendar/multimonth` (功能： [multi-month views](multimonth-grid))


## 高级构建包

首先，通过如下的集中供暖方式获取`fullcalendar-scheduler`高级构建包
<!--First, obtain the premium `fullcalendar-scheduler` bundle in one of the following ways:-->

- **Download**: <a href='{{ site.fullcalendar_premium_repo }}/releases/download/v{{ site.data.latest-releases.v6 }}/fullcalendar-scheduler-{{ site.data.latest-releases.v6 }}.zip'>fullcalendar-scheduler-{{ site.data.latest-releases.v6 }}.zip</a>
- **CDN:** [jsdelivr](https://www.jsdelivr.com/package/npm/fullcalendar-scheduler?version={{ site.data.latest-releases.v6 }})
- **NPM:** `npm install fullcalendar-scheduler`

然后，编写如下的初始化代码：
<!--Then, write the following initialization code:-->

```html
<!DOCTYPE html>
<html lang='en'>
  <head>
    <meta charset='utf-8' />
    <script src='https://cdn.jsdelivr.net/npm/fullcalendar-scheduler@{{ site.data.latest-releases.v6 }}/index.global.min.js'></script>
    <script>

      document.addEventListener('DOMContentLoaded', function() {
        var calendarEl = document.getElementById('calendar');
        var calendar = new FullCalendar.Calendar(calendarEl, {
          initialView: 'resourceTimelineWeek'
        });
        calendar.render();
      });

    </script>
  </head>
  <body>
    <div id='calendar'></div>
  </body>
</html>
```
[查看可运行的例子 &raquo;](timeline-standard-view-demoo)
<!--[View a runnable example &raquo;](timeline-standard-view-demo)-->

你不需要引入`fullcalendar-scheduler`构建包跟`fullcalendar`构建包。`fullcalendar-scheduler`构建包含了所有内容。
<!--You won't need to include the `fullcalendar-scheduler` bundle AND the `fullcalendar` bundle. The `fullcalendar-scheduler` bundle includes everything.-->

`fullcalendar-scheduler`构建包的`index.global(.min).js`文件包含以下的包：
<!--The `fullcalendar-scheduler` bundle's `index.global(.min).js` file includes the following packages:-->

- `@fullcalendar/core`
- `@fullcalendar/interaction` (for [date selecting](date-clicking-selecting), [event dragging & resizing](event-dragging-resizing))
- `@fullcalendar/daygrid` (for [month](month-view) and [dayGrid](daygrid-view) views)
- `@fullcalendar/timegrid` (for [timeGrid](timegrid-view) views)
- `@fullcalendar/list` (for [list views](list-view))
- `@fullcalendar/multimonth` (for [multi-month views](multimonth-grid))
- `@fullcalendar/adaptive` (for [print optimization](print))
- `@fullcalendar/scrollgrid`
- `@fullcalendar/timeline` ([more info](timeline-view-no-resources))
- `@fullcalendar/resource`
- `@fullcalendar/resource-daygrid` ([more info](resource-daygrid-view))
- `@fullcalendar/resource-timegrid` ([more info](vertical-resource-view))
- `@fullcalendar/resource-timeline` ([more info](timeline-view))


## 单独插件
<!--## Individual Plugins-->

你也可以通过引入`<script>`标签来单独引入插件，例如：
<!--You can also include `<script>` tags for individual plugins. Example:-->

```html
<!DOCTYPE html>
<html lang='en'>
  <head>
    <meta charset='utf-8' />
    <script src='https://cdn.jsdelivr.net/npm/@fullcalendar/core@{{ site.data.latest-releases.v6 }}/index.global.min.js'></script>
    <script src='https://cdn.jsdelivr.net/npm/@fullcalendar/daygrid@{{ site.data.latest-releases.v6 }}/index.global.min.js'></script>
    <script>

      document.addEventListener('DOMContentLoaded', function() {
        var calendarEl = document.getElementById('calendar');
        var calendar = new FullCalendar.Calendar(calendarEl, {
          initialView: 'dayGridMonth'
        });
        calendar.render();
      });

    </script>
  </head>
  <body>
    <div id='calendar'></div>
  </body>
</html>
```
