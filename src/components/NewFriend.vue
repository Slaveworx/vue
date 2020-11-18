<template>
  <div>
    <!-- This is a button toggling the modal -->
    <button
      class="uk-button uk-button-primary uk-margin uk-margin-top uk-width-1-1"
      type="button"
      uk-toggle="target: #modal-example"
    >
      Add Friend +
    </button>

    <!-- This is the modal -->
    <div id="modal-example" uk-modal>
      <div class="uk-modal-dialog uk-modal-body">
        <button
          class="uk-modal-close-default"
          type="button"
          uk-close
          @click="resetForm"
        ></button>
        <h2 class="uk-modal-title">Add new friend</h2>
        <div v-show="this.error">
          <div class="uk-alert-danger" uk-alert>
            <p>Please fill in the details.</p>
          </div>
        </div>
        <div v-show="this.success">
          <div class="uk-alert-success" uk-alert>
            <p>Record Submitted Successfuly!</p>
          </div>
        </div>
        <section>
          <form @submit.prevent="createNewFriend">
            <div>
              <div>
                <label>Name</label>
                <div>
                  <input
                    class="uk-input"
                    type="text"
                    v-model="name"
                    placeholder="e.g Alex Smith"
                  />
                </div>
              </div>
              <div>
                <label>Email</label>
                <div>
                  <input
                    class="uk-input"
                    type="email"
                    v-model="emailAddress"
                    placeholder="e.g. alexsmith@gmail.com"
                  />
                </div>
              </div>
              <div>
                <label>Phone</label>
                <div>
                  <input
                    class="uk-input"
                    uk-input="uk-input"
                    type="tel"
                    v-model="phoneNumber"
                    placeholder="223 225 441"
                  />
                </div>
              </div>
              <button class="uk-button uk-button-primary uk-button-small uk-width-1-1 uk-margin">
                <span uk-icon="check"></span> Create new Friend
              </button>
            </div>
          </form>
        </section>
      </div>
    </div>
  </div>
</template>


<script>
export default {

  emits: ["create-friend"],

  data() {
    return {
      error: false,
      success: false,
      name: "",
      phoneNumber: "",
      emailAddress: "",
    };
  },

  methods: {
    createNewFriend() {
      if (
        this.name !== "" &&
        this.phoneNumber !== "" &&
        this.emailAddress !== ""
      ) {
        this.$emit(
          "create-friend",
          this.name,
          this.phoneNumber,
          this.emailAddress
        );
        this.resetForm();
        this.error = false;
        this.success = true;
      } else {
        this.error = true;
        this.success = false;
      }
    },

    resetForm() {
      //reset properties
      this.name = "";
      this.phoneNumber = "";
      this.emailAddress = "";
      this.success = false;
      this.error = false;
    },
  },
};
</script>