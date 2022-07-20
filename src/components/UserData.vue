<template>
  <div>
    <h1>Start components</h1>
    <h2>First name:{{ firstName }}</h2>
    <h2>Last name: {{ lastName }}</h2>
    <h3>{{ age }}</h3>
    <h2>Full name: {{ uName }}</h2>
    <h1>End component</h1>
  </div>
</template>

<script>
import { computed } from 'vue';
export default {
  props: ['firstName', 'lastName', 'age'],
  setup(props, context) {
    const uName = computed(function () {
      return props.firstName + ' ' + props.lastName;
    });

    console.log(context);
    return {
      uName,
    };
  },
};
</script>
