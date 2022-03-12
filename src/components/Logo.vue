<template>
  <h1>{{ title }}</h1>
</template>

<script>
export default {
  name: "Logo",
  props: {
    title: {
      type: String,
      default: "Logo",
    },
  },
};
</script>

<style lang="scss" scoped>
h1 {
  color: white;
  font-size: 0.9rem;
  font-weight: 600;
}
</style>