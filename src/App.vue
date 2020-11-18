<template>
<div>
  <section>
    <div class="uk-grid-row">
      <div class="uk-grid-column">
        <new-friend @create-friend="createNewFriend"> </new-friend>
      </div>
    </div>
  </section>
  <section>
    <div class="uk-grid-row">
      <div class="uk-grid-column">
        <friend-contact
          v-for="friend in friends"
          :key="friend"
          :id="friend.id"
          :name="friend.name"
          :phone-number="friend.phone"
          :email-address="friend.email"
          :is-favorite="friend.isFavorite"
          @toggle-favorite="toggleFavoriteStatus"
          @delete-friend="deleteFriend"
        ></friend-contact>
      </div>
    </div>
  </section>

  <tg-button>Teste</tg-button>
</div>
</template>

<script>

import FriendContact from './components/FriendContact.vue';
import NewFriend from './components/NewFriend.vue';
import { TgButton } from 'tgcomps';

export default {
  components: {NewFriend, FriendContact, TgButton},
  data() {
    return {
      friends: [],
    };
  },

  methods: {
    deleteFriend(friendId) {
      this.friends = this.friends.filter((friend) => friend.id !== friendId);
    },

    toggleFavoriteStatus(friendId) {
      /* procura no array um match com os mesmo friend ID
      parametro desta função é captado diretamente do parametro enviado do custom event do componente */
      const identifiedFriend = this.friends.find(
        (friend) => friend.id === friendId
      );
      identifiedFriend.isFavorite = !identifiedFriend.isFavorite;
    },

    createNewFriend(name, phoneNumber, emailAddress) {
      const newFriendPush = {
        id: Date.now(),
        name: name,
        phone: phoneNumber,
        email: emailAddress,
        isFavorite: false,
      };

      this.friends.push(newFriendPush);
    },
  },
};
</script>

