<template>
  <section v-on='containerListeners' v-bind='containerAttrs'>
    <div v-on='contentListeners' v-bind='contentAttrs'>
      <slot></slot>
    </div>
  </section>
</template>

<script>
export default {
  inheritAttrs: false,
  name: "ContentWrapper",
  props: {
    contentPrefix: {
      type: String,
      default: 'content-'
    }
  },
  methods: {
    split(what) {
      // what:Object, set of attributes/listeners
      // splits content by keys with and without prefix (default 'content-')
      // into two objects, [container, content]

      // if argument is not Object, return empty objects
      if (what.constructor != Object)
        return [{},{}];
      
      const keys = Object.keys(what);
      
      let contentKeys = [];
      let containerKeys = [];

      // for each key
      // if key starts with the prefix,
      //    it's content property
      // else, it's container property

      keys.forEach(key => {
        if (key.indexOf(this.contentPrefix) === 0)
          contentKeys.push(key);
        else 
          containerKeys.push(key);
      });
      
      // extract values
      let content = {};
      contentKeys.forEach(key => {
        let newkey = key.substring(this.contentPrefix.length, key.length);
        content[newkey] = what[key];
      })

      let container = {};
      containerKeys.forEach(key => {
        container[key] = what[key];
      });
      
      return [container, content];
    }
  },
  computed: {
    ___splitListeners() {
      const split = this.split(this.$listeners);
      return split;
    },
    ___splitAttrs() {
      const split = this.split(this.$attrs);

      return split;
    },
    containerListeners() {
      return this.___splitListeners[0];
    },
    contentListeners() {
      return this.___splitListeners[1];
    },
    containerAttrs() {
      return this.___splitAttrs[0];
    },
    contentAttrs() {
      return this.___splitAttrs[1];
    }
  }
}
</script>
