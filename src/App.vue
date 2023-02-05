<script setup>
import "./style.css";
</script>

<template>
  <div class="flex justify-center items-center flex-col min-h-screen">
    <h1 class="text-xl underline capitalize mb-3 text-gray-700">
      Get Random users with RANDOMEUSERS API
    </h1>
    <div
      href="#"
      class="relative block overflow-hidden rounded-lg border border-gray-100 p-8 w-[600px] shadow-2xl"
    >
      <span
        class="absolute inset-x-0 bottom-0 h-2 bg-gradient-to-r from-green-300 via-blue-500 to-purple-600"
      ></span>

      <div class="justify-between sm:flex">
        <div>
          <h3 class="text-xl font-bold text-gray-900 capitalize">
            {{ users.name }}
          </h3>
          <p class="mt-1 text-xs font-medium text-gray-600">
            {{ users.email }}
          </p>
        </div>

        <div class="ml-3 hidden flex-shrink-0 sm:block">
          <img
            alt="Paul Clapton"
            :src="users.img"
            class="h-16 w-16 rounded-lg object-cover shadow-sm"
          />
        </div>
      </div>

      <div class="mt-4 sm:pr-8">
        <p class="text-sm text-gray-500">
          Lorem ipsum dolor sit amet consectetur, adipisicing elit. Maxime sed
          obcaecati, ratione nisi, repellendus excepturi explicabo, cupiditate
          ea sapiente cumque officia aspernatur nobis facere fugiat voluptates
          error ullam! Nobis, ut!
        </p>
      </div>

      <dl class="mt-6 flex justify-between">
        <div class="flex flex-col-reverse">
          <dt class="text-sm font-medium text-gray-600">
            {{ users.gender }}
          </dt>
          <dd class="text-xs text-gray-500">Gender</dd>
        </div>
        <button
          @click="getRandomUsers"
          class="capitalize inline-block rounded border border-current px-8 py-3 text-sm font-medium text-indigo-600 transition hover:-rotate-2 hover:scale-110 focus:outline-none focus:ring active:text-indigo-500"
        >
          generate Users
        </button>
      </dl>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      users: {
        name: "oussama ezitouni",
        email: "zitounioussama95@gmail.com",
        img: "https://randomuser.me/api/portraits/men/10.jpg",
        gender: "Male",
      },
    };
  },
  methods: {
    async getRandomUsers() {
      const res = await fetch("https://randomuser.me/api");
      const { results } = await res.json();
      console.log(results);
      this.users.name =
        results[0].name.title +
        " " +
        results[0].name.first +
        " " +
        results[0].name.last;
      this.users.email = results[0].email;
      this.users.img = results[0].picture.large;
      this.users.gender = results[0].gender;
    },
  },
};
</script>
