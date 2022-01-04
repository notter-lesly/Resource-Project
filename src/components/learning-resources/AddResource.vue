<template>
  <base-dialog v-if="inputIsInvalid" title="Invalid Input" @close="confirmError">
    <template #default>
      <p>Unfortunately, at least one input is invalid</p>
    </template>
    <template #actions>
      <base-button @click="confirmError"> Okay </base-button>
    </template>
  </base-dialog>

  <base-card>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <label for="title"> Title </label>
        <input id="title" name="title" type="text" ref="titleInput" />
      </div>
      <div class="form-control">
        <label for="description"> Description </label>
        <textarea
          id="description"
          name="description"
          rows="3"
          v-model="this.description"
          ref="descInput"
        >
        </textarea>
      </div>
      <div class="form-control">
        <label for="link"> Link </label>
        <textarea
          id="link"
          name="link"
          rows="url"
          v-model="this.link"
          ref="linkInput"
        >
        </textarea>
      </div>
      <div>
        <base-button type="submit" @submit="submitData">
          Add resource</base-button
        >
      </div>
    </form>
  </base-card>
</template>

<script>
import BaseButton from '../UI/BaseButton.vue';
import BaseDialog from '../UI/BaseDialog.vue';
export default {
  inject: ['addResource'],
  data() {
    return {
      inputIsInvalid: false,
    };
  },
  components: { BaseButton, BaseDialog },
  methods: {
    confirmError() {
      this.inputIsInvalid = false;
    },
    submitData() {
      const enteredTitle = this.$refs.titleInput.value;
      const enteredDescription = this.$refs.descInput.value;
      const enteredLink = this.$refs.linkInput.value;

      if (
        enteredTitle.trim() === '' ||
        enteredDescription.trim() === '' ||
        enteredLink.trim() === ''
      ) {
        this.inputIsInvalid = true
        return
      }

      this.addResource(enteredTitle, enteredDescription, enteredLink);
    },
  },
  
};
</script>

<style scoped>
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
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>
