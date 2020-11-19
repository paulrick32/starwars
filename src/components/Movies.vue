<template>
  <div>
    <center>
      <button class="btn" @click.prevent="checkName">
        Clique para ver todos os filmes:
      </button>
    </center>
    <ul class="px-3 list-disc">
      <li v-for="film in films" :key="film.url">
        Filme: {{ film.title }}, Diretor: {{ film.director }}, Ano:
        {{ film.release_date }} .
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
import { debounce } from "lodash";

export default {
  data: () => ({
    keyword: "",
    films: [],
  }),
  components: {},
  methods: {
    checkName() {
      // eslint-disable-next-line no-console
      console.log(`Checking name: ${this.keyword}`);
      axios
        .get("https://swapi.dev/api/films/", {
          params: {
            search: this.keyword,
          },
        })
        .then((res) => {
          // eslint-disable-next-line no-console
          console.log(res.data.results);
          this.films = res.data.results;
        })
        .catch((err) => {
          // eslint-disable-next-line no-console
          console.log(err);
        });
    },
  },
  created() {
    this.debounceName = debounce(this.checkName, 1000);
  },
  watch: {
    keyword() {
      if (!this.keyword) return;
      this.debounceName();
    },
  },
};
</script>

<style scoped>
.btn {
  background-color: #34495e;
  border: none;
  border-radius: 10px;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
}

ul {
  counter-reset: index;
  padding: 0;
  max-width: 400px;
}

/* List element */
li {
  counter-increment: index;
  display: flex;
  align-items: center;
  padding: 12px 0;
  box-sizing: border-box;
}

/* Element counter */
li::before {
  content: counters(index, ".", decimal-leading-zero);
  font-size: 1.5rem;
  text-align: right;
  font-weight: bold;
  min-width: 50px;
  padding-right: 12px;
  font-variant-numeric: tabular-nums;
  align-self: flex-start;
  background-image: linear-gradient(to bottom, aquamarine, orangered);
  background-attachment: fixed;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

/* Element separation */
li + li {
  border-top: 1px solid rgba(255, 255, 255, 0.2);
}
</style>
