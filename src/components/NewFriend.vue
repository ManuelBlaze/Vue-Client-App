<template>
  <form>
    <div>
      <label for="name">Name</label>
      <input type="text" name="name" id="name" v-model="name" />
    </div>

    <div>
      <label for="phone">Phone</label>
      <input type="tel" name="phone" id="phone" v-model="phone" />
    </div>

    <div>
      <label for="email">E-Mail</label>
      <input type="email" name="email" id="email" v-model="email" />
    </div>

    <div>
      <button @click.prevent="addFriend">Add Friend</button>
    </div>
  </form>
</template>

<script>
import CommonVars from '../common';

/**
 * returns sanitazed string
 * @param {String} str string to sanitaze
 * @returns {String} sanitazed string
 */
const sanitazeString = (str) => str.trim();

export default {
  emits: ['add-friend'],
  data() {
    return {
      name: '',
      phone: '',
      email: '',
    };
  },
  methods: {
    validateForm() {
      // sanitaze all the fields
      const parsedName = sanitazeString(this.name);
      const parsedPhone = sanitazeString(this.phone);
      const parsedEmail = sanitazeString(this.email);

      // check for name validation
      if (parsedName.length < CommonVars.nameMinLength) {
        alert('Name must have min 2 characters');
        return false;
      }

      // check for phone validation
      if (parsedPhone.length !== CommonVars.phoneMinLength) {
        alert('Please use a valid phone number');
        return false;
      }

      // check for email validation
      if (!CommonVars.emailRegex.test(parsedEmail)) {
        alert('Please use a valid email');
        return false;
      }

      return true;
    },
    addFriend() {
      // validate the fields
      const validationSucces = this.validateForm();

      // if we have errors stop the creation of the friend
      if (!validationSucces) {
        return;
      }

      // otherwise we send the info to the father component
      this.$emit('add-friend', {
        name: this.name,
        phone: this.phone,
        email: this.email,
        id: new Date().toISOString(),
        isFavorite: false,
      });

      // clean the form
      this.name = '';
      this.phone = '';
      this.email = '';
    },
  },
};
</script>
