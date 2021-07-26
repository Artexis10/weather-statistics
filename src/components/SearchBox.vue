<template>
  <div class="search-box">
    <input
      type="text"
      class="search-bar"
      placeholder="Search..."
      v-model="query"
      :disabled="isDisabled"
      @keypress.enter="search(query)"
    />
  </div>
</template>

<script>
export default {
  props: ["search", "isDisabled"],
  data() {
    return {
      query: ""
    };
  }
};
</script>
