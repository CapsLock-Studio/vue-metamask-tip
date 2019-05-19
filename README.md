# vue-metamask-tip

This is a simple port from [https://github.com/MetaMask/TipButton](https://github.com/MetaMask/TipButton), you can use metamask tip button without any css selector like official.

## Install

```bash
npm install vue-metamask-tip --save
```

## Usage

in main.js

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

in index.vue

```html
<template>
  <div>
    <MetamaskTipButton
      address="0x32Be343B94f860124dC4fEe278FDCBD38C102D88"
      amount="1"
      type="1"
    ></MetamaskTipButton>
  </div>
</template>
```

## Props

|Name|Type|Default|Description|
|---|---|---|---|
|amount|String||ETH amount, use string to prevent float precision issue|
|address|String||Receiver ETH wallet|
|type|String|1|MetaMask button type|
|callback|String||This component will post `{"hash": "<ID>"}` to this url|