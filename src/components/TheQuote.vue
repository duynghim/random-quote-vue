<template>
  <div class="wrapper">
    <div v-if="quote">
      <blockquote class="shadow">
        <p>
          {{ quote.quote }}
        </p>
        <p class="author">
          {{ quote.author }}
        </p>
      </blockquote>
      <button class="button-9" role="button" v-on:click="newQuote">
        New Quote
      </button>
    </div>
    <div v-if="!quote">
      <pulse-loader :loading="!quote" color="blue"></pulse-loader>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import PulseLoader from "vue-spinner/src/PulseLoader.vue";

export default {
  name: "TheQuote",
  data() {
    return {
      quote: null,
    };
  },
  methods: {
    newQuote() {
      console.log("call");
      const apiKey = "vZULp0SHku3j80chHb74QA==3b7cZkIf2Mz6pNSO";
      const apiUrl = "https://api.api-ninjas.com/v1/quotes";
      axios
        .get(apiUrl, {
          headers: {
            "X-Api-Key": apiKey,
          },
        })
        .then((res) => (this.quote = res.data[0]));
    },
  },
  mounted() {
    const fetchQuote = async () => {
      const apiKey = "vZULp0SHku3j80chHb74QA==3b7cZkIf2Mz6pNSO";
      const apiUrl = "https://api.api-ninjas.com/v1/quotes";
      const res = await axios.get(apiUrl, {
        headers: {
          "X-Api-Key": apiKey,
        },
      });

      this.quote = res.data[0];
    };
    fetchQuote();
  },
};
</script>

<style scoped>
@import url(https://fonts.googleapis.com/css?family=Noto+Sans);

* {
  color: #0000ff;
  font-family: "Noto Sans", sans-serif;
}

.wrapper {
  margin: 0 auto;
  width: 90%;
  padding-bottom: 50px;
}

blockquote {
  background: white;
  padding: 20px 30px 20px 30px;
  margin: 50px auto;
  width: 80%;
  max-width: 800px;
}

.shadow {
  border: solid 2px;
  box-shadow: 15px 15px 0 0 #0000ff;
}

p {
  font-size: 1.15rem;
}

.author {
  text-align: right;
}

@import url(https://fonts.googleapis.com/css?family=Noto+Sans);

.button-9 {
  appearance: button;
  backface-visibility: hidden;
  background-color: #405cf5;
  border-radius: 6px;
  border-width: 0;
  box-shadow: rgba(50, 50, 93, 0.1) 0 0 0 1px inset,
    rgba(50, 50, 93, 0.1) 0 2px 5px 0, rgba(0, 0, 0, 0.07) 0 1px 1px 0;
  box-sizing: border-box;
  color: #fff;
  cursor: pointer;
  font-family: "Noto Sans", sans-serif;
  font-size: 100%;
  height: 44px;
  line-height: 1.15;
  margin: 12px 0 0;
  outline: none;
  overflow: hidden;
  padding: 0 25px;
  position: relative;
  text-align: center;
  text-transform: none;
  transform: translateZ(0);
  transition: all 0.2s, box-shadow 0.08s ease-in;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  width: 30%;
}

.button-9:disabled {
  cursor: default;
}

.button-9:focus {
  box-shadow: rgba(50, 50, 93, 0.1) 0 0 0 1px inset,
    rgba(50, 50, 93, 0.2) 0 6px 15px 0, rgba(0, 0, 0, 0.1) 0 2px 2px 0,
    rgba(50, 151, 211, 0.3) 0 0 0 4px;
}
</style>
