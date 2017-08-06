# vue-custom-keyboard

> A Vue.js component for keyboard

## Installation

``` bash
npm i vue-custom-keyboard --save
```

## Usage

Impoart and use it in a single file component.

```vue
<template>
  <VueCustomKeyboard></VueCustomKeyboard>
</template>

<script>
  import VueCustomKeyboard from 'vue-custom-keyboard'
  import 'vue-custom-keyboard/dist/vue-custom-keyboard.min.css'

  export default {
    name: 'componentWithKeyboard',
    components: {
        VueCustomKeyboard
    }
  }
</script>
```

## Props config

``` javascript
props: {
  /**
   * Visibility for keyboard.
   * @default false
   * @type {Boolean}
   */
  isOpen: {
    type: Boolean,
    default: true
  },
  level1: {
    type: String,
    default: '粤京津泸鲁冀云辽黑湘皖新苏浙赣鄂桂甘晋蒙陕吉闽贵青藏川宁琼豫渝台港澳'
  },
  level2: {
    type: String,
    default: '1234567890QWERTYUPASDFGHJKLZXCVBNM'
  },
  maxLength: {
    type: Number,
    default: 7
  },
  onChange: {
    type: Function
  },
  onBlur: {
    type: Function
  },
  onDone: {
    type: Function
  },
  /**
   * For remembering previous value.
   * @default ''
   * @type {String}
   */
  defaultValue: {
    type: String,
    default: ''
  }
}
```

## Demo

Check [vue-custom-keyboard-demo](https://github.com/ttzshawn/vue-custom-keyboard-demo) and show case below.

![Show case](https://raw.githubusercontent.com/ttzshawn/vue-custom-keyboard-demo/master/assets/keyboard-demo.png)