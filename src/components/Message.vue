<template>
  <div class="alert alert-success text-center" role="alert" v-show="message">
    {{ message }}
  </div>
</template>

<script>
export default {
  name: "Message",
  props: {
    message: String,
    type: String,
  },
  data() {
    return {
      success: "alert-success",
      warning: "alert-warning",
      error: "alert-danger",
    };
  },
};
</script>