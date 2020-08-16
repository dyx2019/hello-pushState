<template>
  <div>
    <div class="push_url">
      <div class="push_url-txt"> URL before pushState is:</div> {{ urlBeforePush }}
    </div>
    <div class="push_url">
      <div class="push_url-txt"> URL after pushState is:</div> {{ urlAfterPush }}
    </div>
    <div class="push_url">
      <div class="push_url-txt"> the life cycle:</div> {{ flag }}
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      urlBeforePush: '',
      urlAfterPush: '',
      flag: '',
    }
  },
  created() {
    this.urlBeforePush = window.location.href;
  },
  
  mounted() {
    console.log('mounted');
    this.flag = 'mounted';
    window.history.pushState(null, null, '192.168.1.105:8080/home');
    window.addEventListener('popstate', this.preventBack, false);
    this.urlAfterPush = window.location.href;
  },
  
  destroyed() {
    console.log('destroyed');
    this.flag = 'destroyed';
    window.removeEventListener('popstate', this.preventBack, false);
  },

  methods: {
    preventBack() {
      debugger;
      if (this.flag === 'mounted') {
        console.log('preventBack in mounted');
      } else {
        console.log('preventBack in destroyed');
      }
    }
  }
}
</script>

<style lang="stylus" scoped>
  .push_url {
    font-size: 2rem;
    color: red;
    &-txt {
      font-size: 1.5rem;
      color: black;
    }
  }
</style>