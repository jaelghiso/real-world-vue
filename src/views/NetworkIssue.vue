<template>
  <div>
    <h1>Uh-Oh!</h1>
    <h3>
      It´s look like you're experiencing some network issues, please click the
      back button and try again!
    </h3>
    <router-link :to="{ name: 'event-list' }"
      >&larr; Or go back to Home</router-link
    >
  </div>
</template>
<script>
export default {};
</script>
