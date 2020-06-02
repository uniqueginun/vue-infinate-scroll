<template>
  <div id="observer"></div>
</template>

<script>
export default {
  name: "Obsorver",
  data() {
    return {
      observer: null
    };
  },
  methods: {
    handleIntersection(entries) {
      entries.map(entry => {
        if (entry.isIntersecting) {
          this.$emit("intersecting");
        }
      });
    }
  },
  mounted() {
    this.observer = new IntersectionObserver(this.handleIntersection);
    this.observer.observe(this.$el);
  }
};
</script>

<style scoped>
#observer {
  height: 2px;
}
</style>