<template>
  <div class="uk-card-default uk-width-large uk-margin uk-padding">
    <header>
      <h4>
        {{ name }} {{ isFavorite ? "(Favorite)" : "" }}
        <span uk-icon="trash" id="trash-icon" @click="deleteFriendRecord"></span>
      </h4>
      <hr />
    </header>

    <div>
      <button
        class="uk-button uk-button-primary uk-button-small uk-width-1-1"
        @click="toggleDetails"
      >
        {{ !detailsAreVisible ? "Show Details" : "Hide Details" }}
      </button>
      <button
        class="uk-button uk-button-default uk-button-small uk-width-1-1"
        @click="toggleFavorite"
      >
        Toggle Favorite
      </button>
      <ul class="uk-list" v-if="detailsAreVisible">
        <li><strong>Phone:</strong> {{ phoneNumber }}</li>
        <li><strong>Email:</strong> {{ emailAddress }}</li>
      </ul>
    </div>
  </div>
</template>



<script>
export default {
  props: {
    id: {
      type: Number,
      required: true,
    },
    name: {
      type: String,
      required: true,
    },
    phoneNumber: {
      type: String,
      required: true,
    },
    emailAddress: {
      type: String,
      required: true,
    },
    isFavorite: {
      type: Boolean,
      required: false,
      default: false,
      /* validator: function (value) {
        return value === "1" || value === "0";
      }, */
    },
  },

  emits: ["toggle-favorite", "delete-friend"],

  data() {
    return {
      detailsAreVisible: false,
    };
  },

  methods: {
    toggleDetails() {
      this.detailsAreVisible = !this.detailsAreVisible;
    },

    toggleFavorite() {
      /* // isto emite dados para a main APP */
      this.$emit("toggle-favorite", this.id);
    },

    deleteFriendRecord() {
      this.$emit("delete-friend", this.id);
    },
  },
};
</script>

<style scoped>
#trash-icon {
  margin-left: 5px;
}

#trash-icon:hover {
  color: crimson;
}
</style>