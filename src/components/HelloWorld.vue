<template>
  <v-container class="light-green">
    <v-row class="text-center d-flex justify-center mb-6">
      <v-col cols="12">
        <!-- <v-img
          :src="require('../assets/logo.svg')"
          class="my-3"
          contain
          height="200"
        /> -->
        <h1 class="display-2 font-weight-bold mb-3">
          Welcome to ponzi-detector !
        </h1>
      </v-col>
      <v-responsive width="400">
          <v-textarea
            v-model="opcode"
            color="cyan darken"
            label="Paste your opcode here"
            placeholder="Start typing..."
            row-height="10"
            rows="20"
            solo
          >
          </v-textarea>
          <v-btn @click="submit">submit</v-btn>
      </v-responsive>

      <v-responsive width="400" min-height="400" class="d-flex align-center">
        <div>
          <v-progress-circular
            indeterminate
            color="primary"
          ></v-progress-circular>
          <h1> Score: {{ score }}</h1>
          <h1 v-if="ponzi">true</h1>
          <h1 v-if="!ponzi">false</h1>
        </div>
      </v-responsive>
    </v-row>
  </v-container>
</template>

<script>
import axios from "axios";
export default {
  name: "HelloWorld",

  data: () => ({
    opcode: "",
    ponzi: true,
    score: 0,
  }),

  methods: {
    submit() {
      if (!this.opcode) {
        return;
      }
      this.ponzi = !this.ponzi;
      this.score = 12;
    },
    submit_real() {
      if (!this.opcode) {
        return;
      }
      axios
        .post("url", this.opcode, {
          headers: {
            "Content-Type": "text/plain",
          },
        })
        .then((res) => {
          // this.ponzi = !this.ponzi
          // this.score = 12
          this.ponzi = res.ponzi;
          this.score = res.score;
        });
    },
  },
};
</script>
