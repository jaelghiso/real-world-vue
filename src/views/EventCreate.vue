<template>
  <div>
    <h1>Create an Event</h1>
    <form @submit.prevent="createEvent">
      <label>Select a category</label>
      <select v-model="event.category">
        <option value="" v-for="cat in categories" :key="cat">{{ cat }}</option>
      </select>
      <h3>Name and describe your event</h3>
      <div class="field">
        <label for="">Title</label>
        <input
          type="text"
          v-model="event.title"
          placeholder="Add an event title"
        />
      </div>
      <div class="field">
        <label for="">Description</label>
        <input
          type="text"
          v-model="event.description"
          placeholder="Add a description"
        />
      </div>
      <h3>Where is your event?</h3>
      <div class="field">
        <label for="">Location</label>
        <input
          type="text"
          v-model="event.location"
          placeholder="Add a location"
        />
      </div>
      <h3>When is your event?</h3>
      <div class="field">
        <label for="">Date</label>
        <datepicker v-model="event.date" placeholder="Select a date" />
      </div>
      <div class="field">
        <label for="">Select a time</label>
        <select v-model="event.time">
          <option value="" v-for="time in times" :key="time">{{ time }}</option>
        </select>
      </div>
      <button type="submit" class="button -fill-gradient" value="Submit">
        Submit
      </button>
    </form>
  </div>
</template>
<script>
import Datepicker from "vuejs-datepicker";
export default {
  components: {
    Datepicker,
  },
  data() {
    const times = [];
    for (let i = 1; i <= 24; i++) {
      times.push(i + ":00");
    }
    return {
      times,
      categories: this.$store.state.categories,
      event: this.createFreshEventObject(),
    };
  },
  methods: {
    createEvent() {
      this.$store
        .dispatch("event/createEvent", this.event)
        .then(() => {
          this.$router.push({
            name: "event-show",
            params: { id: this.event.id },
          });
          this.event = this.createFreshEventObject();
        })
        .catch(() => {});
    },
    createFreshEventObject() {
      const user = this.$store.state.user.user;
      const id = Math.floor(Math.random() * 10000000);

      return {
        id: id,
        user: user,
        category: "",
        organizer: user,
        title: "",
        description: "",
        location: "",
        date: "",
        times: "",
        attendess: [],
      };
    },
  },
};
</script>
<style scoped>
.field {
  margin-bottom: 24px;
}
</style>
