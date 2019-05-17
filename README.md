# vue-metamask-tip

This is a simple port from [https://github.com/MetaMask/TipButton](https://github.com/MetaMask/TipButton), you can use metamask tip button without any css selector like official.

## Install

```bash
npm install vue-metamask-tip --save
```

## Usage

```js
import Vue from 'vue';
import MetamaskTipButton from 'vue-metamask-tip';
import App from './App.vue';

import 'vue-metamask-tip/dist/vue-metamask-tip.css';

new Vue({
  el: '#app',
  components: {
    MetamaskTipButton
  },
  render: h => h(App),
});
```