<template>
  <v-app>
    <v-app-bar app color="teal" dark>
      <div class="d-flex align-center">
        <h3>Phonebook</h3>
      </div>
    </v-app-bar>

    <v-main class="ma-5">
      <phonebook />
    </v-main>
  </v-app>
</template>

<script>
import Phonebook from "./components/Phonebook";

export default {
  components: {
    Phonebook,
  },
};
</script>