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
import {
  computed,
  inject,
  onBeforeMount,
  onBeforeUnmount,
  onMounted,
  onUnmounted,
  onUpdated,
  onBeforeUpdate,
} from 'vue';

export default {
  props: ['firstName', 'lastName'],
  setup(props, context) {


    //The hook cycles are being replaced by these function that can be imported from vue. 
    //Only the Created and BeforeCreated are replaced by the setup() itself.
    //All the lyfe cycles receives a function that runs in that cycle.
    onBeforeUpdate(function() {
        console.log("Before Updated");
    })
onBeforeMount( function() {
    console.log("On before mount")
})
  onBeforeUnmount(function() {
    console.log("Before unmount")
  })
  onMounted(function() {
    console.log("On Mounted")
  })
  onUnmounted(function() {
    console.log("On Unmounted")
  })
  onUpdated(function() {
    console.log("On Update")
  })
  onBeforeUpdate(function() {
    console.log("Before Update")
  })


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
      age,
    };
  },
};
</script>
