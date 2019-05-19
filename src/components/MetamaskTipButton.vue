<template>
  <div>
    <div
      v-bind:class="`tip-button
        tip-button-type${type}
        ${isDisabled ? `tip-button-type${type}-disable` : ''}`"
      v-on:click="onMouseClick"
    >
    </div>
    <notifications></notifications>
  </div>
</template>
<script>
import axios from 'axios';
import Notification from 'vue-notification';
import Vue from 'vue';

Vue.use(Notification);

export default {
  name: 'metamask-tip',
  data() {
    return {
      isDisabled: false,
    };
  },
  props: {
    type: {
      type: String,
      default: '1',
    },
    address: {
      type: String,
      required: true,
    },
    amount: {
      type: String,
      required: true,
    },
    callback: {
      type: String,
    },
  },
  mounted() {
    if (typeof web3 === 'undefined') {
      this.isDisabled = true;

      this.$notify(
        {
          type: 'error',
          title: 'Error!',
          text: 'You need to install MetaMask to use this feature.  <a href="https://metamask.io">https://metamask.io</a>',
          duration: 60000,
        },
      );
    }
  },
  methods: {
    onMouseClick() {
      window
        .ethereum
        .enable()
        .then(() => {
          const web3js = new window.Web3(window.web3.currentProvider);
          const [user] = web3js.eth.accounts;

          if (user) {
            web3js.eth.sendTransaction(
              {
                to: this.address,
                from: user,
                value: web3js.toWei(this.amount, 'ether'),
              },
              (error, hash) => {
                if (error) {
                  this.$notify(
                    {
                      type: 'error',
                      title: 'Error!',
                      text: error.message,
                      duration: 5000,
                    },
                  );
                } else {
                  this.$notify(
                    {
                      type: 'sucess',
                      title: 'Success!',
                      text: `Transaction complete! hash: ${hash}`,
                      duration: 5000,
                    },
                  );

                  if (this.callback) {
                    axios.post(this.callback, { hash });
                  }
                }
              },
            );
          } else {
            this.$notify(
              {
                type: 'error',
                title: 'Error!',
                text: 'You have to create your ETH wallet first',
                duration: 5000,
              },
            );
          }
        });
    },
  },
};
</script>
<style scoped>
  .tip-button {
    width: 304px;
    height: 89px;
    background-size: 100%;
    cursor: pointer;
  }

  .tip-button-type1 {
    background-image: url(../assets/images/1_pay_mm_off.png);
  }

  .tip-button-type1:hover {
    background-image: url(../assets/images/1_pay_mm_over.png);
  }

  .tip-button-type1:active {
    background-image: url(../assets/images/1_pay_mm_off.png);
  }

  .tip-button-type1-disable {
    background-image: url(../assets/images/1_pay_mm_off.png) !important;
    cursor: not-allowed !important;
    pointer-events: none;
  }

  .tip-button-type2 {
    background-image: url(../assets/images/2_pay_mm_off.png);
  }

  .tip-button-type2:hover {
    background-image: url(../assets/images/2_pay_mm_over.png);
  }

  .tip-button-type2:active {
    background-image: url(../assets/images/2_pay_mm_off.png);
  }

  .tip-button-type2-disable {
    background-image: url(../assets/images/2_pay_mm_off.png) !important;
    cursor: not-allowed !important;
    pointer-events: none;
  }

  .tip-button-type3 {
    background-image: url(../assets/images/3_pay_mm_off.png);
  }

  .tip-button-type3:hover {
    background-image: url(../assets/images/3_pay_mm_over.png);
  }

  .tip-button-type3:active {
    background-image: url(../assets/images/3_pay_mm_off.png);
  }

  .tip-button-type3-disable {
    background-image: url(../assets/images/3_pay_mm_off.png) !important;
    cursor: not-allowed !important;
    pointer-events: none;
  }

  .tip-button-type4 {
    background-image: url(../assets/images/4_pay_mm_off.png);
  }

  .tip-button-type4:hover {
    background-image: url(../assets/images/4_pay_mm_over.png);
  }

  .tip-button-type4:active {
    background-image: url(../assets/images/4_pay_mm_off.png);
  }

  .tip-button-type4-disable {
    background-image: url(../assets/images/4_pay_mm_off.png) !important;
    cursor: not-allowed !important;
    pointer-events: none;
  }

  .tip-button-type5 {
    background-image: url(../assets/images/5_pay_mm_off.png);
  }

  .tip-button-type5:hover {
    background-image: url(../assets/images/5_pay_mm_over.png);
  }

  .tip-button-type5:active {
    background-image: url(../assets/images/5_pay_mm_off.png);
  }

  .tip-button-type5-disable {
    background-image: url(../assets/images/5_pay_mm_off.png) !important;
    cursor: not-allowed !important;
    pointer-events: none;
  }

  .tip-button-type6 {
    background-image: url(../assets/images/6_pay_mm_off.png);
  }

  .tip-button-type6:hover {
    background-image: url(../assets/images/6_pay_mm_over.png);
  }

  .tip-button-type6:active {
    background-image: url(../assets/images/6_pay_mm_off.png);
  }

  .tip-button-type6-disable {
    background-image: url(../assets/images/6_pay_mm_off.png) !important;
    cursor: not-allowed !important;
    pointer-events: none;
  }
</style>
<style lang="scss">
  .notification-content {
    a {
      color: white;
    }
  }
</style>
