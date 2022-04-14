<!-- This example requires Tailwind CSS v2.0+ -->
<template>
  <h1 class="text-xl mb-8 text-center">Simpson Quotes</h1>
  <SortButton
    v-on:click="sort('up')"
    :isActive="sortDirection === 'up'"
    direction="up"
    text="Sort ascending"
  />
  <SortButton
    v-on:click="sort('down')"
    direction="down"
    :isActive="sortDirection === 'down'"
    text="Sort descending"
  />
  <div class="grid grid-cols-1 sm:grid-cols-3 lg:grid-cols-5 gap-8">
    <div
      v-for="character in simpsons"
      :key="character"
      class="bg-gradient-to-br from-cyan-100 rounded-lg shadow"
    >
      <div class="flex-1 flex flex-col p-8">
        <img
          class="
            w-32
            h-32
            flex-shrink-0
            mx-auto
            rounded-full
            shadow-xl
            bg-white
          "
          :src="character.image"
          alt="image of quote.character"
        />
        <h3 class="mt-6 text-gray-900 text-xs text-center">
          {{ character.quote }}
        </h3>
        <h2 class="mt-4 text-sm text-center">{{ character.character }}</h2>
      </div>
    </div>
  </div>
  <div>
    <button class="border-2 rounded-lg p-2 m-4" v-on:click="getSimpsons(5)">
      5 Quotes are good
    </button>
    <button class="border-2 rounded-lg p-2 m-4" v-on:click="getSimpsons(10)">
      10 Quotes are good
    </button>
    <button class="border-2 rounded-lg p-2 m-4" v-on:click="getSimpsons(15)">
      15 Quotes are good
    </button>
  </div>
</template>

<script>
import { MailIcon, PhoneIcon } from "@heroicons/vue/solid";
import SortButton from "./SortButton.vue";

const getSimpsons = (amount) => {
  const simpsonsData = fetch(
    `https://thesimpsonsquoteapi.glitch.me/quotes?count=${amount}`
  ).then((res) => res.json());
  return simpsonsData;
};

export default {
  name: "Simpsons",
  components: { SortButton },
  data() {
    return {
      simpsons: [],
      sortDirection: "up",
    };
  },
  methods: {
    async getSimpsons(amount) {
      this.simpsons = await getSimpsons(amount);
    },
    sort(direction) {
      if (direction !== this.sortDirection) {
        this.simpsons.sort((a, b) => {
          if (a.character < b.character) {
            return -1;
          }
          if (a.character > b.character) {
            return 1;
          }
          return 0;
        });
        if (direction === "down") {
          this.simpsons.reverse();
        }
        this.sortDirection = direction;
      }
    },
  },
};
</script>
