<template>
  <button :class="mode">
    <slot></slot>
  </button>
</template>
<script>
export default {
  props: ['mode'],
};
</script>

<style  scoped>
button {
  padding: 0.75rem 1.5rem;
  font-family: inherit;
  background-color: #084227;
  border: 1px solid #322d79;
  color: white;
  cursor: pointer;
}

button:hover,
button:active {
  background-color: #0d3a5f;
  border-color: #102a72;
}

.flat {
  background-color: transparent;
  color: #18af4a;
}

.flat:hover,
.flat:active {
  background-color: #384e6e;
}
</style>