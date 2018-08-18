<template lang="pug">
  section(v-on='containerListeners' v-bind='containerAttrs')
    div(v-on='contentListeners' v-bind='contentAttrs')
      slot
</template>

<script>
export default {
  inheritAttrs: false,
  name: "ContentWrapper",
  props: {
    prefix: {
      type: String,
      default: 'content-'
    }
  },
  methods: {
    split(what) {
      // splits content-* and *
      if (what.constructor != Object)
        return [[],[]];
      
      const keys = Object.keys(what);
      const content = [];
      const container = [];

      keys.forEach(
        key => key.indexOf(this.prefix) === 0 ? 
          content.push(key.substring(this.prefix.length, key.length)) : container(key));

      return [content, container];
    }
  },
  computed: {
    ___splitListeners() {
      const keys = Object.keys(this.$listeners);
      const split = this.split(keys);
      return split;
    },
    ___splitAttrs() {
      const keys = Object.keys(this.$listeners);
      const split = this.split(keys);
      return split;
    },
    containerListeners() {
      return this.___splitListeners()[0];
    },
    contentListeners() {
      return this.___splitListeners()[1];
    },
    containerAttrs() {
      return this.___splitAttrs()[0];
    },
    contentAttrs() {
      return this.___splitAttrs()[1];
    }
  }
}
</script>
