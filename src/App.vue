<template>
  <section class="container">
    <user-data
    :firstName="firstName"
    :last-name="lastName"
    ></user-data>
    <h2>{{ userName }}</h2>
    <h2>{{ user.age }}</h2>
    <h2>uAge: {{ uAge}}</h2>
    <h2>{{ user }}</h2>
    <button @click="setAge">Change Age</button>
    <div>
      <input type="text" placeholder="first name" v-model="firstName"/>
      <input type="text" placeholder="last name" ref="lastNameInput"/>
      <button @click="setLastName">Set Last Name</button>
    </div>

  </section>
</template>

<script>
import { reactive, ref, computed, watch, provide } from 'vue';
import UserData from './components/UserData.vue';

// import { isReactive, isRef } from 'vue'; 
// the isReactive and isRef are helpers to check is a value is reactive or not. it's a function that return true or false.

// import { toRefs } from 'vue';
//the toRefs function receives an object as parameters, any object (including the one in reactive()) and turns all the properties
//inside of it to refs, so it will be reactive.
// using that, I can expose uName.value in return and they'll be reactive.
export default {
  components: {
    UserData
  },
  setup () {
    const firstName = ref('');
    const lastName = ref('');
    const lastNameInput = ref(null);
    const uAge = ref(36);

   const uName =  computed(function () {
      return firstName.value + ' ' + lastName.value;
    });

  function setLastName() {
    lastName.value = lastNameInput.value.value;
  }


     watch([uAge, uName], function(newValues, oldValues) {
        console.log("Old age: " + oldValues[0]);
        console.log("New age: " + newValues[0]);
        console.log("Old name: " + oldValues[1]);
        console.log("New name: " + newValues[1]);
    })

    provide('userAge', uAge);
    //the provide function takes two argument. A name of your choice and the actual value to be provided.


  // function setFirstName(event) {
  //   firstName.value = event.target.value;
  // }

  // function setLastName(event) {
  //   lastName.value = event.target.value
  // }
    // const uName = ref("Diego"); //better store the ref() in a vanilla JS variable. Don't use this keyword.
    //                             //ref() creates an object.
    // const uAge = ref(36);

    const user = reactive({
      // name: "Diego",
      age: 36
    }); //reactive is specialized to work with objects. refs is for any data, including object.

      function setNewAge() {
        user.age++;
        uAge.value++;
      } // to expose functions, just create a function in the setup and expose it in the return.


      return {
      user: user,
      setAge: setNewAge,
      firstName,
      lastName,
      userName: uName,
      uAge,
      setLastName,
      lastNameInput
    };// the ref() and reactive() objective are reactive, that means they change when data is changed.
      // in the other hand, the value inside them are not reactive. So it's important to return the object, no the
      //value inside them.
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