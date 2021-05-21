<template>
  <div v-if="event">
    <h1>{{ event.title }}</h1>
    <p>{{ event.time }} on {{ event.date }} @ {{ event.location }}</p>
    <p>{{ event.description }}</p>
    <p>
      <router-link class="go-back-link" :to="{ name: 'EventList' }"
        >Go Back</router-link
      >
    </p>
  </div>
</template>

<script>
import EventService from "@/services/EventService.js";

export default {
  props: ["id"],
  data() {
    return {
      event: null,
    };
  },
  created() {
    EventService.getEvent(this.id)
      .then((response) => {
        this.event = response.data;
      })
      .catch((error) => {
        console.log(error);
      });
  },
};
</script>

<style scoped>
.go-back-link {
  color: #2c3e50;
  font-size: 110%;
  font-weight: bold;
  text-decoration: underline;
}
</style>
