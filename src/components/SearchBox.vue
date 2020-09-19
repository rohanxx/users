<template>
  <div>
    <input
      class="searchbox"
      type="text"
      placeholder="Type Something here...."
      @input="onInputChange"
    />
  </div>
</template>

<script>
export default {
  name: "SearchBox",
  methods: {
    onInputChange(event) {
      this.$emit("inputChange", event.target.value);
    }
  }
};
</script>

<style scoped>
div {
  display: flex;
  justify-content: center;
  margin: 1rem;
}

.searchbox {
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 12px 20px;
}

.searchbox:focus {
  outline: none !important;
  box-shadow: 0 0 10px #719ece;
}
</style>