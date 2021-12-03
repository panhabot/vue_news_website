<template>
    <nav class="bg-white fixed w-full top-0 z-50">
      <div class="max-w-6xl">
        <div class="flex justify-between">
          <div class="flex my-5">
            <a href="#" class="flex items-center">
              <span
                class="font-bold text-black-500 text-2xl border-2 border-black sm:ml-4 ml-11 px-1 py-1"
                >J43</span
              >
            </a>
          </div>
          <div class="flex mt-8">
            <h1>Your Daily News</h1>
          </div>
          <!-- Mobile menu button -->
          <div class=" flex sm:px-16 items-center" @click="openNav">
            <button class="outline-none mobile-menu-button">
              <svg
                class="w-6 h-6 text-black hover:text-grey-500"
                x-show="!showMenu"
                fill="none"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                viewBox="0 0 24 24"
                stroke="currentColor"
              >
                <path d="M4 6h16M4 12h16M4 18h16"></path>
              </svg>
            </button>
          </div>
        </div>
      </div>
      <!-- mobile menu -->
      <div class="hidden mobile-menu px-7 mt-2 w-screen">
        <ul class="">
          <li>
            <a
              class="block text-sm px-2 py-4 bg-black hove r:text-white font-semibold transition duration-300"
            ></a>
          </li>
          <li class="active" v-for="item in items" :key="item">
            <a
              class="block text-sm px-2 py-4 hover:bg-black hover:text-white font-semibold transition duration-300"
              @click="scrollTo(item)"
              >{{ item }}</a
            >
          </li>
        </ul>
      </div>
    </nav>

</template>

<script>
export default {
  data() {
    return {
      items: ["Home", "Blog", "Podcasts", "Books", "About"],
    };
  },
  methods: {
    scrollTo(refName) {
            const menu = document.querySelector(".mobile-menu");

      menu.classList.toggle("hidden")
      this.$root.$emit("scrollTo1", refName);
    },
    openNav() {
      const menu = document.querySelector(".mobile-menu");
      return menu.classList.toggle("hidden");
    },
  },
};
</script>
