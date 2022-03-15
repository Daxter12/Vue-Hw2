<template>
  <button @click="onClick">Clicked {{ counter }} times!</button>
</template>

<script>
  export default {
    name: "MyButton",
    data() {
      return {
        counter: 0,
      };
    },
    methods: {
      onClick() {
        this.counter++;
      },
      onMouseOver() {},
    },
    beforeCreate() {},
    created() {},
    beforeMount() {},
    mounted() {
      const btn = this.$el.querySelector("button");
      if (!btn) return;
      btn.addEventListener("mouseover", this.onMouseOver);
    },
    beforeUpdate() {},
    updated() {},
    beforeDestroy() {
      const btn = this.$el.querySelector("button");
      if (!btn) return;
      btn.removeEventListener("mouseover", this.onMouseOver);
    },
    destroyed() {},
  };
</script>
