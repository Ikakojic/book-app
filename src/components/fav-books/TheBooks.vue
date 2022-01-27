<template>
  <base-card>
    <base-button
      @click="setSelectedTab('stored-books')"
      :mode="storedBooksButtonMode"
      >Stored Books</base-button
    >

    <base-button @click="setSelectedTab('add-book')" :mode="addBookButtonMode"
      >Add Favourite Book</base-button
    >
  </base-card>
  <keep-alive>
    <component :is="selectedTab"></component>
  </keep-alive>
</template>

<script>
import StoredBooks from './StoredBooks.vue';
import AddBook from './AddBook.vue';
export default {
  components: {
    StoredBooks,
    AddBook,
  },
  data() {
    return {
      selectedTab: 'stored-books',
      storedBooks: [
        {
          id: 'favorite-book',
          title: 'Favorite Book',
          description: 'This is my favorite book!',
          link: 'https://vuejs.org',
        },
        {
          id: 'favorite-novel',
          title: 'Favorite Novel',
          description: 'This is my favorite novel!',
          link: 'https://vuejs.org',
        },
      ],
    };
  },
  provide() {
    return {
      books: this.storedBooks,
      addBook: this.addBook,
      deleteBook: this.removeBook,
    };
  },
  computed: {
    storedBooksButtonMode() {
      return this.selectedTab === 'stored-books' ? null : 'flat';
    },
    addBookButtonMode() {
      return this.selectedTab === 'add-book' ? null : 'flat';
    },
  },

  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
    addBook(title, description, link) {
      const newBook = {
        id: new Date().toISOString(),
        title: title,
        description: description,
        link,
      };
      this.storedBooks.unshift(newBook);
      this.selectedTab = 'stored-books';
    },
    removeBook(bookId) {
      const bookIndex = this.storedBooks.findIndex((book) => book.id == bookId);
      this.storedBooks.splice(bookIndex, 1);
    },
  },
};
</script>