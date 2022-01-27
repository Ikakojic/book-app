<template>
  <base-dialog v-if="invalidInput" title="Input Invalid!">
    <template #default
      ><p>Sorry, one input is invalid!</p>
      <p>Please check your inputs! Thank you!</p></template
    >
    <template #actions
      ><base-button @click="confirmError">Ok</base-button></template
    >
  </base-dialog>
  <base-card>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <label for="title">Title</label>
        <input id="title" name="title" type="text" ref="titleInput" />
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea
          id="description"
          name="description"
          rows="4"
          ref="descInput"
        ></textarea>
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input id="link" name="link" type="url" ref="linkInput" />
      </div>
      <div>
        <base-button type="submit">Add Book</base-button>
      </div>
    </form>
  </base-card>
</template>

<script>
import BaseButton from '../ui/BaseButton.vue';
import BaseDialog from '../ui/BaseDialog.vue';
export default {
  components: { BaseDialog, BaseButton },
  inject: ['addBook'],
  data() {
    return {
      invalidInput: false,
    };
  },
  methods: {
    submitData() {
      const enteredTitle = this.$refs.titleInput.value;
      const enteredDesc = this.$refs.descInput.value;
      const enteredLink = this.$refs.linkInput.value;

      if (
        enteredTitle.trim() === '' ||
        enteredDesc.trim() === '' ||
        enteredLink.trim() === ''
      ) {
        this.invalidInput = true;
        return;
      }
      this.addBook(enteredTitle, enteredDesc, enteredLink);
    },
    confirmError() {
      this.invalidInput = false;
    },
  },
};
</script>
<style  scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #e8f5e6;
}

.form-control {
  margin: 1rem 0;
}
</style>