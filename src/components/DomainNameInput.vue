<template>
<label :for="name">{{ lableName  }}</label>
  <input
    type="text"
    :class="`form-control ${isInvalid}`"
    :name="name"
    placeholder="e.g. example.com"
    v-model="domain"
    v-on:change="inputChange"
  />
</template>

<script>
export default {
  props: {
    name: {
      type: String,
      default: "domain",
    },
    lableName : {
      type: String,
      default: "Extract your domain name"
    },
    isInvalid: String,
  },
  data() {
    return {
      domain: "",
    };
  },
  methods: {
    inputChange: function (event) {
      this.domain = event.target.value
        .replace(
          /http:\/\/www\.|https:\/\/www\.|www\.|http:\/\/|https:\/\//gi,
          ""
        )
        .split("/")[0];

      this.$emit("change", this.domain);
    },
  },
  mounted() {},
};
</script>
