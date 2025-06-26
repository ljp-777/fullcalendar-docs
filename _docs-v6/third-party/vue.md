---
title: Vue组件
title_for_landing: Vue
---

FullCalendar跟Javascript的[Vue]框架完美适配。它提供了一个完美适配FullCalendar标准API的组件。
<!--FullCalendar seamlessly integrates with the [Vue] JavaScript framework. It provides a component that exactly matches the functionality of FullCalendar's standard API.-->

这个包是基于MIT许可证发布的，与FullCalendar标准版本使用的是相同的许可证。有用的链接：
<!--This package is released under an MIT license, the same license the standard version of FullCalendar uses. Useful links:-->

- [浏览Github仓库]({{ site.fullcalendar_vue_repo }}) (老铁点点关注!)
<!--- [Browse the Github repo]({{ site.fullcalendar_vue_repo }}) (老铁点点关注!)-->
- [错误报告说明](/reporting-bugs)
<!--- [Bug report instructions](/reporting-bugs)-->
- 示例项目:
  - [Vue 2 示例](https://github.com/fullcalendar/fullcalendar-examples/tree/main/vue2) (使用 [Webpack] 和 [css-loader]) - [在线运行](https://stackblitz.com/github/fullcalendar/fullcalendar-examples/tree/main/vue2)
  - [Vue 3 示例](https://github.com/fullcalendar/fullcalendar-examples/tree/main/vue3) (使用 [Vite]) - [在线运行](https://stackblitz.com/github/fullcalendar/fullcalendar-examples/tree/main/vue3)

这份指南不会深入的介绍如何初始化Vue项目。如想了解，请查看上述的示例/可运行的项目。
<!--This guide does not go into depth about initializing a Vue project. Please consult the aforementioned example/runnable projects for that.-->

第一步是安装FullCalendar相关依赖。你需要FullCalendar核心包，Vue包，还有其他计划使用的插件。
<!--The first step is to install the FullCalendar-related dependencies. You'll need FullCalendar core, the Vue adapter, and any plugins you plan to use.-->

如果在 **Vue 2**中使用：
<!--If using **Vue 2**:-->

```bash
npm install --save \
  @fullcalendar/core \
  @fullcalendar/vue
```

如果在 **Vue 3**中使用：
<!--If using **Vue 3**:-->

```bash
npm install --save \
  @fullcalendar/core \
  @fullcalendar/vue3
```
然后安装任何额外的FullCalendar插件，像 `@fullcalendar/daygrid`
<!--Then install any additional FullCalendar plugins like `@fullcalendar/daygrid`-->

你可以利用`<FullCalendar>`组件，开始写一个父组件：
<!--You may then begin to write a parent component that leverages the `<FullCalendar>` component:-->

```html
<script>
import FullCalendar from '@fullcalendar/vue3'
import dayGridPlugin from '@fullcalendar/daygrid'
import interactionPlugin from '@fullcalendar/interaction'

export default {
  components: {
    FullCalendar // 注册组件，使<FullCalendar>标签可用
  },
  data() {
    return {
      calendarOptions: {
        plugins: [ dayGridPlugin, interactionPlugin ],
        initialView: 'dayGridMonth'
      }
    }
  }
}
</script>
<template>
  <FullCalendar :options="calendarOptions" />
</template>
```

## Props and Emitted 事件

Vue has the concept of "props" (via `v-bind` or `:`) versus "events" (via `v-on` or `@`). For the FullCalendar connector, there is no distinction between props and events. Everything is passed into the master `options` object as key-value pairs. Here is an example that demonstrates passing in an `events` array and a `dateClick` handler:

```html
<script>
import FullCalendar from '@fullcalendar/vue3'
import dayGridPlugin from '@fullcalendar/daygrid'
import interactionPlugin from '@fullcalendar/interaction'

export default {
  components: {
    FullCalendar // make the <FullCalendar> tag available
  },
  data() {
    return {
      calendarOptions: {
        plugins: [ dayGridPlugin, interactionPlugin ],
        initialView: 'dayGridMonth',
        dateClick: this.handleDateClick,
        events: [
          { title: 'event 1', date: '2019-04-01' },
          { title: 'event 2', date: '2019-04-02' }
        ]
      }
    }
  },
  methods: {
    handleDateClick: function(arg) {
      alert('date click! ' + arg.dateStr)
    }
  }
}
</script>
<template>
  <FullCalendar :options="calendarOptions" />
</template>
```


## Modifying Options

You can modify your calendar's options after initialization by reassigning them within the options object. This is an example of changing the `weekends` options:

```html
<script>
import FullCalendar from '@fullcalendar/vue3'
import dayGridPlugin from '@fullcalendar/daygrid'
import interactionPlugin from '@fullcalendar/interaction'

export default {
  components: {
    FullCalendar // make the <FullCalendar> tag available
  },
  data() {
    return {
      calendarOptions: {
        plugins: [ dayGridPlugin, interactionPlugin ],
        initialView: 'dayGridMonth',
        weekends: false // initial value
      }
    }
  },
  methods: {
    toggleWeekends: function() {
      this.calendarOptions.weekends = !this.calendarOptions.weekends // toggle the boolean!
    }
  }
}
</script>
<template>
  <button @click="toggleWeekends">toggle weekends</button>
  <FullCalendar :options="calendarOptions" />
</template>
```


## Slot Templates

[Slot templates](https://vuejs.org/guide/components/slots.html#slot-content-and-outlet) can be passed to FullCalendar components. They accepts slots for all [content-injection](content-injection) settings such as [eventContent](event-render-hooks).

```html
<template>
  <FullCalendar :options="calendarOptions">
    <template v-slot:eventContent='arg'>
      <b>{% raw %}{{{% endraw %} arg.event.title {% raw %}}}{% endraw %}</b>
    </template>
  </FullCalendar>
</template>
```

All slots are [scoped slots](https://vuejs.org/guide/components/slots.html#scoped-slots) that accept an argument (explicitly named `arg` in the above example).


## Calendar API

Hopefully you won't need to do it often, but sometimes it's useful to access the underlying `Calendar` object for raw data and methods.

This is especially useful for controlling the current date. The [initialDate](initialDate) prop will set the *initial* date of the calendar, but to change it after that, you'll need to rely on the [date navigation methods](date-navigation).

To do something like this, you'll need to get ahold of the component's ref (short for "reference"). In the template:

```html
<FullCalendar ref="fullCalendar" :options="calendarOptions" />
```

Once you have the ref, you can get the underlying `Calendar` object via the `getApi` method:

```js
let calendarApi = this.$refs.fullCalendar.getApi()
calendarApi.next()
```


## Kebab-case in Markup

Some people prefer to write component names in kebab-case when writing markup. This will work fine:

```html
<full-calendar :options="calendarOptions" />
```

However, the properties within `calendarOptions` must have the same names.


## FullCalendar Premium

How do you use [FullCalendar Premium's](/pricing) plugins with Vue? They are no different than any other plugin. Just follow the same instructions as you did `dayGridPlugin` in the above example. If you plan to use resources, you'll need the `@fullcalendar/resource` package:

```sh
npm install --save \
  @fullcalendar/core \
  @fullcalendar/vue3 \
  @fullcalendar/resource \
  @fullcalendar/resource-timeline
```

Then, initialize your calendar. Make sure to include your [schedulerLicenseKey](schedulerLicenseKey):

```html
<script>
import FullCalendar from '@fullcalendar/vue3'
import resourceTimelinePlugin from '@fullcalendar/resource-timeline'

export default {
  components: {
    FullCalendar
  },
  data() {
    return {
      calendarOptions: {
        plugins: [ resourceTimelinePlugin ],
        schedulerLicenseKey: 'XXX'
      }
    }
  }
}
</script>
<template>
  <FullCalendar :options="calendarOptions" />
</template>
```


## TypeScript

For `@fullcalendar/vue3`, nothing special is needed for TypeScript integration.

For `@fullcalendar/vue` (Vue 2), it is recommended to use [class-based components](https://github.com/vuejs/vue-class-component). See an <a href='https://github.com/fullcalendar/fullcalendar-examples/tree/main/vue2-typescript' class='more-link'>example TypeScript project</a>


## Vuex

[Vuex](https://vuex.vuejs.org/) is a popular state management library for Vue that works well with the FullCalendar connector. <a href='https://github.com/fullcalendar/fullcalendar-examples/tree/main/vue2-vuex' class='more-link'>View an example project</a>


## Nuxt

If you plan to use the [Nuxt] Vue framework, you'll need special configuration. <a class='more-link' href='https://github.com/fullcalendar/fullcalendar-examples/tree/main/nuxt3'>See the example project</a>


[Vue]: https://vuejs.org/
[Webpack]: https://webpack.js.org/
[css-loader]: https://webpack.js.org/loaders/css-loader/
[docs toc]: https://fullcalendar.io/docs#toc
[Nuxt]: https://nuxtjs.org/
[TypeScript]: https://www.typescriptlang.org/
[Vite]: https://github.com/vitejs/vite
