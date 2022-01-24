<template>
  <li>
    <h2>{{ name }} {{ isFavorite === '1' ? '(Favorite)' : '' }}</h2>
    <button @click="toggleFavorite">Toogle Favorite</button>
    <button @click="toggleDetails">
      {{ detailsVisible ? 'Hide' : 'Show' }} Details
    </button>

    <ul v-if="detailsVisible">
      <li><strong>Phone:</strong> {{ phone }}</li>
      <li><strong>Email:</strong> {{ email }}</li>
    </ul>
  </li>
</template>

<script>
/**
 * favorite values convertion
 * @constant
 * @type {Object}
 */
const CONVERTION = { '0': '1', '1': '0', };

/**
 * is favorite values
 * @constant
 * @type {String[]}
 */
const IS_FAVORITE_VALUES = ['0', '1'];

export default {
  props: {
    name: {
      type: String,
      required: true,
    },
    phone: {
      type: String,
      required: true,
    },
    email: {
      type: String,
      required: true,
    },
    favorite: {
      type: String,
      required: false,
      default: '0',
      validator: (value) => IS_FAVORITE_VALUES.includes(value),
    },
  },
  // props: ['name', 'phone', 'email', 'favorite'],
  data() {
    return {
      detailsVisible: false,
      isFavorite: this.favorite,
    };
  },
  methods: {
    toggleDetails() {
      this.detailsVisible = !this.detailsVisible;
    },
    toggleFavorite() {
      this.isFavorite = CONVERTION[this.isFavorite];
    },
  },
};
</script>
