<template>
  <div class="counter">
    <h1>{{ label }}</h1>
    <h2>{{ value }}</h2>
  </div>
</template>

<script>
export default {
  name: "Counter",
  props: ["label", "value"]
};
</script>

<style>
.counter {
  border: 1px solid #000;
  margin-top: 20px;
  padding: 20px;
}
.counter h1,
.counter h2 {
  margin: 0;
}
</style>
