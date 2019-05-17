<template>
  <div>
    <MetamaskTipButton
      address="0x32Be343B94f860124dC4fEe278FDCBD38C102D88"
      amount="1"
    ></MetamaskTipButton>
  </div>
</template>
<script>
import MetamaskTipButton from '../dist/vue-metamask-tip.umd.min';

export default {
  components: {
    MetamaskTipButton,
  },
};
</script>
