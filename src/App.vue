<template>
  <section>
    <header>
      <h1>My Friends</h1>
    </header>

    <section>
      <new-friend @add-friend="addFriend" />
    </section>

    <p v-if="friends.length === 0"><strong> Add some friends! </strong></p>

    <ul v-else>
      <friend-contact
        v-for="friend in friends"
        :key="friend.id"
        :id="friend.id"
        :name="friend.name"
        :phone="friend.phone"
        :email="friend.email"
        :favorite="friend.favorite"
        @toggle-favorite="toggleFavorite"
        @delete="deleteFriend"
      />
    </ul>
  </section>
</template>

<script>
import FriendContact from './components/FriendContact.vue';
import NewFriend from './components/NewFriend.vue';

export default {
  components: { FriendContact, NewFriend },
  data() {
    return {
      friends: [
        {
          id: 'daniela',
          name: 'Daniela Villada',
          phone: '0123 456 789',
          email: 'ela@localhost.com',
          favorite: true,
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
  methods: {
    addFriend(friend) {
      this.friends.push(friend);
    },
    toggleFavorite(friendId) {
      const identifiedFriend = this.friends.find(
        (friend) => friend.id === friendId
      );

      identifiedFriend.favorite = !identifiedFriend.favorite;
    },
    deleteFriend(friendId) {
      this.friends = this.friends.filter((friend) => friend.id !== friendId);
    },
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Jost&display=swap');

* {
  box-sizing: border-box;
}

html {
  font-family: 'Jost', sans-serif;
}

body {
  margin: 0;
}

header {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  margin: 3rem auto;
  border-radius: 10px;
  padding: 1rem;
  background-color: #58004d;
  color: white;
  text-align: center;
  width: 90%;
  max-width: 40rem;
}

button {
  margin: 0 6px;
}

p {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  margin: 3rem auto;
  border-radius: 10px;
  padding: 1rem;
  text-align: center;
  width: 90%;
  max-width: 40rem;
}

#app ul {
  margin: 0;
  padding: 0;
  list-style: none;
}

#app li,
#app form {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  margin: 1rem auto;
  border-radius: 10px;
  padding: 1rem;
  text-align: center;
  width: 90%;
  max-width: 40rem;
}

#app h2 {
  font-size: 2rem;
  border-bottom: 4px solid #ccc;
  color: #58004d;
  margin: 0 0 1rem 0;
}

#app button {
  font: inherit;
  cursor: pointer;
  border: 1px solid #ff0077;
  background-color: #ff0077;
  color: white;
  padding: 0.05rem 1rem;
  box-shadow: 1px 1px 2px rgba(0, 0, 0, 0.26);
}

#app button:hover,
#app button:active {
  background-color: #ec3169;
  border-color: #ec3169;
  box-shadow: 1px 1px 4px rgba(0, 0, 0, 0.26);
}

#app input {
  font: inherit;
  padding: 0.15rem;
}
#app label {
  font-weight: bold;
  margin-right: 1rem;
  width: 7rem;
  display: inline-block;
}
#app form div {
  margin: 1rem 0;
}
</style>
