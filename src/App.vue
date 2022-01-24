<template>
  <section>
    <h2>My Friends</h2>

    <ul>
      <friend-contact />
    </ul>
  </section>
</template>

<script>
export default {
  data() {
    return {
      friends: [
        {
          id: 'daniela',
          name: 'Daniela Villada',
          phone: '0123 456 789',
          email: 'ela@localhost.com',
        },
        {
          id: 'marin',
          name: 'Juan Marin',
          phone: '987 456 0123',
          email: 'pendejo@localhost.com',
        },
      ],
    };
  },
};
</script>
