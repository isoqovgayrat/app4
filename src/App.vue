<template>
  <div class="flex justify-center items-center min-h-screen">
    <div class="flex flex-col justify-center items-center">
      <div class="relative mb-8">
        <div class="absolute left-1/2 - top-2 bg-white rounded-full px-4 py1 text-lg transform -translate-x-1/2">
          {{ gender }}
        </div>
        <img class="w-64 h-64 rounded-full border-8" :class="checkGender" v-bind:src="img" :alt="firstname">
        <!--        (attributlar bilan  ishlatiladigan direktivlarni (v-bind) o'zini  yoki (:) ikki nuqta qo'yib ketsak ham bo'ladi)-->
      </div>
      <div class="text-center space-y-1">

        <h1 class="text-4xl font-bold">Salom, mening ismim {{ fullname }}</h1>
        <p class="text-lg text-gray-500">{{ email }}</p>
        <p class="text-lg text-gray-500">{{ phone_number }}</p>
      </div>
      <button class="bg-black text-white px-6 py-2 rounded font-bold mt-6" @click="randomUser">Tasodifiy inson</button>

    </div>
  </div>
</template>

<script>


export default {
  name: 'App',
  data() {
    return {
      firstname: "Anjelina",
      lastname: "Wood",
      email: "anjeLina@example.com",
      gender: "female",
      phone_number: "(526) -184-2430",
      img: "https://randomuser.me/api/portraits/women/63.jpg"
    }
  },
  methods: {
    async randomUser() {
      const res = await fetch("https://randomuser.me/api/");
      const {results} = await res.json();
      const user = results[0];
      this.firstname = user.name.first
      this.lastname = user.name.last
      this.email = user.email
      this.gender = user.gender
      this.phone_number = user.phone
      this.img = user.picture.large

    }
  },
  computed: {
    checkGender() {
      return {
        "border-pink-500": this.gender === 'female',
        "border-green-500": this.gender === 'male'

      }
    },
    fullname(){
      return this.firstname + " " + this.lastname
    }
  }


}
</script>

<style>

</style>
