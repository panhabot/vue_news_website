<template>
  <div class="max-w-6xl mx-auto px-4 mt-10">
    <div v-if="isLoading" class="flex justify-center items-center h-screen">
      <div
        class="animate-spin rounded-full h-32 w-32 border-b-2 border-gray-900"
      ></div>
    </div>
    <div ref="Home" v-else class="flex sm:flex-col">
      <div
        class="flex-initial sm:flex-1 sm:w-auto w-4/6 hover:opacity-80 hover:z-0 cursor-pointer"
      >
        <img :src="topNews.urlToImage" alt="" />
        <div class="flex-row justify-between mt-2">
          <div class="flex flex-row">
            <p class="text-gray-400 text-xs">Feb 11</p>
            <p class="ml-1 text-gray-400 text-xs">. 5 min read</p>
          </div>
          <p class="text-gray-400 text-xs">By {{ topNews.author }}</p>
        </div>
        <p class="sm:text-sm text-3xl font-bold">{{ topNews.title }}</p>
        <p class="sm:text-xs">{{ topNews.description }}</p>
      </div>
      <div class="sm:hidden mx-4 border bg-black border-black"></div>
      <div class="sm:flex-1 flex-1 md:w-72">
        <div
          v-for="item in computedRightNews"
          :key="item.title"
          @click="gotoSite(item.url)"
          class="hover:opacity-80 cursor-pointer"
        >
          <img :src="item.urlToImage" alt="" />
          <div class="flex flex-row justify-between mt-1">
            <div class="flex flex-row">
              <p class="text-gray-400 text-xs">Feb 11</p>
              <p class="ml-1 text-gray-400 text-xs">. 5 min read</p>
            </div>
            <p class="ml-1 text-gray-400 text-xs">By {{ item.author }}</p>
          </div>
          <p class="text-sm mt-3 font-bold">{{ item.title }}</p>
          <p class="text-xs mt-1 mb-3">{{ item.description }}</p>
        </div>
      </div>
    </div>
    <div class="mt-10" ref="Blog">
      <div class="border bg-black border-black"></div>
      <div class="flex flex-row justify-between py-3">
        <p class="text-lg font-semibold">TODAY'S TRENDING</p>
        <p
          class="text-sm border-b-2 border-black hover:opacity-80 cursor-pointer"
        >
          View More
        </p>
      </div>
      <div class="border bg-black border-black"></div>
    </div>
    <div class="sm:hidden mt-10">
      <carousel perPage="3" autoplay="true" class="w-full">
        <slide v-for="news in trendNews" :key="news" class="px-2">
          <div class="">
            <img :src="news.urlToImage" alt="" class="w-96 h-56 object-cover" />
            <div class="flex flex-row justify-between mt-1">
              <div class="flex flex-row">
                <p class="text-gray-400 text-xs">Feb 11</p>
                <p class="ml-1 text-gray-400 text-xs">. 5 min read</p>
              </div>
              <p class="ml-1 text-gray-400 text-xs">By {{ news.author }}</p>
            </div>
            <p class="text-lg mt-3 font-bold">{{ news.title }}</p>
            <p class="text-xs mt-1">{{ news.description }}</p>
          </div>
        </slide>
      </carousel>
    </div>
    <div class="hidden sm:block mt-10">
      <carousel perPage="1" autoplay="true" class="w-full">
        <slide v-for="news in trendNews" :key="news" class="px-2">
          <div class="">
            <img :src="news.urlToImage" alt="" />
            <div class="flex flex-row justify-between mt-1">
              <div class="flex flex-row">
                <p class="text-gray-400 text-xs">Feb 11</p>
                <p class="ml-1 text-gray-400 text-xs">. 5 min read</p>
              </div>
              <p class="ml-1 text-gray-400 text-xs">By {{ news.author }}</p>
            </div>
            <p class="text-lg mt-3 font-bold">{{ news.title }}</p>
            <p class="text-xs mt-1 mb-3">{{ news.description }}</p>
          </div>
        </slide>
      </carousel>
    </div>
    <div class="mt-10">
      <div class="border bg-black border-black"></div>
      <div class="flex flex-row justify-between py-3">
        <p class="text-lg font-semibold">THE LATEST ARTICLES</p>
        <p
          class="text-sm border-b-2 border-black hover:opacity-80 cursor-pointer"
        >
          View More
        </p>
      </div>
      <div class="border bg-black border-black"></div>
    </div>
    <div
      class="flex flex-row mt-10"
      v-for="news in computedLatestNews"
      :key="news"
    >
      <div class="flex flex-row sm:flex-col">
        <div class="flex-initial">
          <img :src="news.urlToImage" alt="" class="h-40 object-contain" />
        </div>
        <div class="flex-1 w-full pl-10 sm:pl-0">
          <p class="text-xs text-gray-500">- {{ news.author }}</p>
          <p class="text-2xl sm:text-sm font-bold">{{ news.title }}</p>
          <p class="text-xs">{{ news.title }}</p>
        </div>
      </div>
    </div>
    <div ref="Books" class="mt-10">
      <div class="border bg-black border-black"></div>
      <div class="flex flex-row justify-between py-3">
        <p class="text-lg font-semibold">BESTSELLERS OF THE MONTH</p>
        <p
          class="text-sm border-b-2 border-black hover:opacity-80 cursor-pointer"
        >
          View More
        </p>
      </div>
      <div class="border bg-black border-black"></div>
    </div>
    <div class="sm:hidden mt-10">
      <carousel perPage="4" class="w-full">
        <slide v-for="book in booksData" :key="book" class="px-2 sm:px-0">
          <div class="">
            <img :src="book.url" alt="" class="h-96 w-64 object-cover" />
            <p class="text-lg mt-3 font-bold">{{ book.title }}</p>
            <p class="text-sm text-gray-500">By {{ book.author }}</p>
            <button
              class="mt-10 text-center w-full border-solid border px-4 py-4 hover:bg-black hover:text-white transform duration-200 border-black"
            >
              Buy for {{ book.price }}
            </button>
          </div>
        </slide>
      </carousel>
    </div>
    <div class="hidden sm:block mt-10">
      <carousel perPage="1" class="w-full">
        <slide v-for="book in booksData" :key="book" class="px-2">
          <div class="">
            <img :src="book.url" alt="" class="h-96 object-cover" />
            <p class="text-lg mt-3 font-bold">{{ book.title }}</p>
            <p class="text-sm text-gray-500">By {{ book.author }}</p>
            <button
              class="mt-10 text-center w-full border-solid border px-4 py-4 hover:bg-black hover:text-white transform duration-200 border-black"
            >
              Buy for {{ book.price }}
            </button>
          </div>
        </slide>
      </carousel>
    </div>
    <div class="py-10">
      <div class="border bg-black border-black"></div>

      <div class="py-10">
        <p class="text-center font-semibold sm:text-lg text-4xl py-5">
          SUBCRIBE TO GET MORE
        </p>
        <p class="text-gray-500 sm:text-xs text-center sm:px-1 py-3 px-20">
          You are the sum total of everything you've ever seen, heard, eaten,
          smelled, been, told, forgot, - it's all there. Everything influences
          each of us and because of that I try to make sure that my experience
          are positive.
        </p>
        <div class="flex justify-center sm:flex-col">
          <a
            href="#"
            class="border sm:text-sm py-3 sm:my-1 text-center text-white px-5 mx-2 hover:bg-white hover:text-black border-black bg-black transform duration-200"
            >Learn More</a
          >
          <a
            href="#"
            class="border sm:text-sm py-3 sm:my-1 text-center text-white px-5 mx-2 hover:bg-white hover:text-black border-black bg-black transform duration-200"
            >Buy Now for $10.99/Monthly</a
          >
        </div>
      </div>
      <div class="border bg-black border-black"></div>
    </div>
    <div class="flex sm:flex-col flex-row justify-between py-12 sm:py-5">
      <div class="flex-1">
        <p class="font-semibold text-xl">Send Me News</p>
        <input class="w-72 mt-5 border-b border-black" placeholder="Enter Your Email" type="text" />
      </div>
      <div class="flex-1">
        <div class="flex flex-row sm:mt-4 justify-between">
          <div class="flex flex-col text-right sm:text-left">
            <p class="font-semibold ">CONTENT</p>
            <a href="" class="text-sm ">Blog</a>
            <a href=""  class="text-sm ">Podcasts</a>
            <a href="" class="text-sm ">Books</a>
            <a href="" class="text-sm ">Subscription</a>
          </div>
          <div class="flex flex-col text-right sm:text-left">
            <p class="font-semibold">COMPANY</p>
            <a href="" class="text-sm ">About</a>
            <a href="" class="text-sm ">Contact Us</a>
            <a href="" class="text-sm ">Partnership</a>
            <a href="" class="text-sm ">Careers</a>
          </div>
          <div class="flex flex-col text-right sm:text-left">
            <p class="font-semibold">SOCIAL</p>
            <a href="" class="text-sm ">Instagram</a>
            <a href="" class="text-sm ">Facebook</a>
            <a href="" class="text-sm ">Linkedin</a>
            <a href="" class="text-sm ">Youtube</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { Carousel, Slide } from "vue-carousel";
import book1 from "../assets/book1.jpg";
import book2 from "../assets/book2.jpg";
import book3 from "../assets/book3.jpg";
import book4 from "../assets/book4.jpg";
import book5 from "../assets/book5.jpeg";
export default {
  name: "Home",
  components: {
    Carousel,
    Slide,
  },
  data() {
    return {
      topNews: {},
      newsData: [],
      trendNews: [],
      lastestData: [],
      booksData: [
        {
          url: book1,
          title: "Harry Potter and the Sorserers Stone",
          author: "J.K. Rowling",
          price: "$15.20",
        },
        {
          url: book2,
          title: "Harry Potter and the Philosopher's Stone",
          author: "J.K. Rowling",
          price: "$50.00",
        },
        {
          url: book3,
          title: "Harry Potter and the Goblet of Fire",
          author: "J.K. Rowling",
          price: "$35.30",
        },
        {
          url: book4,
          title: "Harry Potter and the Goblet of Fire",
          author: "J.K. Rowling",
          price: "$8.20",
        },
        {
          url: book5,
          title: "Harry Potter and the Goblet of Fire",
          author: "J.K. Rowling",
          price: "$12.99",
        },
      ],
      isLoading: true,
    };
  },
  methods: {
    async getNewsData() {
      const res = await axios(
        "https://newsapi.org/v2/top-headlines?sources=bbc-news&apiKey=93b9ab3ddc2b4795bc0063e23323ccc6"
      );
      console.log(res.data);
      return res.data;
    },
    gotoSite(url) {
      return window.location.assign(url);
    },
    async getTrendingData() {
      const res = await axios(
        "https://newsapi.org/v2/top-headlines?sources=techcrunch&apiKey=93b9ab3ddc2b4795bc0063e23323ccc6"
      );
      return res.data;
    },
    async getLatestData() {
      const res = await axios(
        "https://newsapi.org/v2/everything?domains=wsj.com&apiKey=93b9ab3ddc2b4795bc0063e23323ccc6"
      );
      return res.data;
    },
  },
  async created() {
    const data = await this.getNewsData();
    const trendData = await this.getTrendingData();
    const latestDatas = await this.getLatestData();
    this.topNews =
      data.articles[Math.floor(Math.random() * data.articles.length)];
    this.newsData = data.articles.filter((x) => x.title != this.topNews.title);

    this.trendNews = trendData.articles.slice(
      trendData.articles.length - (trendData.articles.length - 4)
    );
    this.lastestData = latestDatas.articles;
    this.isLoading = false;
    console.log(this.newsData);
  },
  computed: {
    computedRightNews() {
      const random =
        this.newsData[Math.floor(Math.random() * this.newsData.length)];
      return this.newsData.slice(
        this.newsData.indexOf(random),
        this.newsData.indexOf(random) + 2
      );
    },
    computedLatestNews() {
      const random =
        this.lastestData[Math.floor(Math.random() * this.lastestData.length)];
      return this.lastestData.slice(this.lastestData.indexOf(random));
    },
  },
  mounted() {
    this.$root.$on("scrollTo1", (refName) => {
      console.log(refName);
      var element = this.$refs[refName];
      return element.scrollIntoView({ behavior: "smooth" });
    });
  },
};
</script>
