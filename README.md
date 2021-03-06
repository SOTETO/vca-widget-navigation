# WidgetNavigation

[![npm](https://img.shields.io/npm/v/heureka-widget-navigation.svg)](https://www.npmjs.com/package/heureka-widget-navigation) [![vue2](https://img.shields.io/badge/vue-2.x-brightgreen.svg)](https://vuejs.org/)

> Implements a widget showing the menu of the Pool², an instance of the Heureka! architecture.

## Widgets
This package implements the following widgets. These widgets supporting a consistent navigation of Viva con Aguas Pool².
Use it to integrate the main menu and the footer of the Pool².

### Menu
The menu implements basic HTML and a bit of CSS code to show the buttons of the main menu. During the initiation of it, 
the widget requests the content of the menu by an ajax call to Dispenser. That means all buttons with labels and targets, 
but also the structure of the menu are received from a database managed by Dispenser. Its designed to stay at the top 
of the page.

![](./src/images/menu.png)

You can use it that way:
```xml
<WidgetTopNavigation />
```
*There are no parameters for this widget*<br />
*There are no slots for this widget*

> Attention! Please consider the additional CSS style needed to create the default Pool² layout (see [Usage](#usage)).

### Footer
The footer contains a menu with secundary priority. It is designed to be the bottom of the page. 

![](./src/images/footer.png)

You can use it that way:
```xml
<WidgetBottomNavigation />
```
*There are no parameters for this widget*<br />
*There are no slots for this widget*

> Attention! Please consider the additional CSS style needed to create the default Pool² layout (see [Usage](#usage)).

## Installation

```bash
npm install --save vca-widget-navigation
```

## Usage

### Bundler (Webpack, Rollup)

Add the following to the component that uses the navigation:
```js
import { WidgetTopNavigation, WidgetBottomNavigation } from 'vca-widget-navigation';
export default {
  name: 'App', // use the name of your component
  components: { WidgetTopNavigation, WidgetBottomNavigation }
}
```

Inside your template:
```xml
<template>
  <div id="app">
      <WidgetTopNavigation />
      <div id="content">
        <router-view/>
      </div>
      <WidgetBottomNavigation />
    </div>
</template>
```

Attention! This is required to have the menu at the top and the footer at the bottom of the page. The conatiner of menu,
footer and content has to displayed flexible and its content should be a column. The container of the content (in the 
middle of menu and footer) has to grow:
```css
  #app {
    flex: 1;
    display: flex;
    flex-direction: column;
  }
  #content {
    flex-grow: 1;
    flex-shrink: 0;
    display: flex;
    overflow: auto;
  }
```

### Browser

```html
<!-- Include after Vue -->
<!-- Local files -->
<link rel="stylesheet" href="widget-user/dist/widget-user.css"></link>
<script src="vca-widget-user/dist/widget-user.js"></script>

<!-- From CDN -->
<link rel="stylesheet" href="https://unpkg.com/vca-widget-user/dist/widget-user.css"></link>
<script src="https://unpkg.com/vca-widget-user"></script>
```

#### Existing internationalization
If you already use [vue-i18n](https://www.npmjs.com/package/vue-i18n) to handle your internationalization and localization, we have to merge our messages into 
yours. You can do this in your `main.js` before you instantiate your Vue App.

```js
import Vue from 'vue';
...
import VueI18n from 'vue-i18n';
import { WidgetTopNavigation, WidgetBottomNavigation } from 'vca-widget-navigation' 

Vue.use(VueI18n);

const i18n = new VueI18n({
    locale: locale,
    messages: {
        'en-US': require('@/lang/en_US'),
        'de-DE': require('@/lang/de_VCA'),
        'ja-JA': require('../node_modules/element-ui/lib/locale/lang/ja')
    }
});

// the most important line of code here
Vue.use(WidgetTopNavigation, { 'i18n': i18n })
Vue.use(WidgetBottomNavigation, { 'i18n': i18n })

/* eslint-disable no-new */

new Vue({
  ...
  i18n,
  components: { WidgetTopNavigation, WidgetBottomNavigation },
  ...
}).$mount('#app');
```
Afterwards, you don't have to use `Vue.use(WidgetTopNavigation)` or `Vue.use(WidgetBottomNavigation)` in your components again.

## Development

### Build

Bundle the js and css of to the `dist` folder:

```bash
npm run build
```


## Publishing

The `prepublish` hook will ensure dist files are created before publishing. This
way you don't need to commit them in your repository.

```bash
# Bump the version first
# It'll also commit it and create a tag
npm version
# Push the bumped package and tags
git push --follow-tags
# Ship it 🚀
npm publish
```

## License

[MIT](http://opensource.org/licenses/MIT)
