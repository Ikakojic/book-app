<template>
  <li>
    <base-card>
      <header>
        <h3>{{ title }}</h3>
        <base-button mode="flat" @click="deleteBook(id)">Delete</base-button>
      </header>

      <p>{{ description }}</p>
      <nav>
        <a :href="link">View Book</a>
        <!--v-bind with link prop-->
      </nav>
    </base-card>
  </li>
</template>
<script>
import BaseButton from '../ui/BaseButton.vue';

export default {
  components: { BaseButton },
  props: ['id', 'title', 'description', 'link'],
  inject: ['deleteBook'],
};
</script>
<style scoped>
li {
  margin: auto;
  max-width: 40rem;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

h3 {
  font-size: 1.25rem;
  margin: 0.5rem 0;
}

p {
  margin: 0.5rem 0;
}

a {
  text-decoration: none;
  color: #0c8657;
}

a:hover,
a:active {
  color: #2b9c0f;
}
</style>