<template>
  <section class="container">
    <h2>{{ user.name }}</h2>
    <h2>{{ user.age }}</h2>
    <h2>{{ user }}</h2>
  </section>
</template>

<script>
import { ref } from 'vue';
export default {
  setup () {
    // const uName = ref("Diego"); //better store the ref() in a vanilla JS variable. Don't use this keyword.
    //                             //ref() creates an object.
    // const uAge = ref(36);

    const user = ref({
      name: "Diego",
      age: 36
    });

    console.log(user);

    setTimeout(function () {
      // uName.value = "Didi";
      // uAge.value = 26;
      user.value.name = 'Didi';
      user.value.age = 26;
    }, 2000)

    return {
      userName: user.value.name,
      age: user.value.age,
      user: user
    };
  } //the setup method replaces the Data, Methods, Watch and computed all together. The other are untouched.
  // data() {
  //   return {
  //     userName: 'Maximilian',
  //   };
  // },
};
</script>

<style>
* {
  box-sizing: border-box;
}

html {
  font-family: sans-serif;
}

body {
  margin: 0;
}

.container {
  margin: 3rem auto;
  max-width: 30rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 1rem;
  text-align: center;
}
</style>