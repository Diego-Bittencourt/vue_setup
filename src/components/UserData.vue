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
import { computed, inject } from 'vue';
export default {
  props: ['firstName', 'lastName'],
  setup(props, context) {
    //the context has information about slot, if being used and emit events.
    // the emit event can be used with context.emit('event');
    const uName = computed(function () {
      return props.firstName + ' ' + props.lastName;
    });

    const age = inject('userAge');
    //the inject function must be imported from vue and injected like this. The variable then must be exposed in the
    //return object. NEVER change the value in the injected end. Always change the value from the provided end.


    console.log(context);
    return {
      uName,
      age
    };
  },
};
</script>
