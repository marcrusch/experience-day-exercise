<template>
  <div>
    <button
      v-bind:class="{ 'bg-slate-500': isActive }"
      class="border-2 rounded-lg p-2 m-4"
    >
      -{{ text }}-
    </button>
  </div>
</template>
<script>
// make the button work, so that it will sort according to the `direction` prop
export default {
  name: "SortButton",
  props: {
    text: String,
    isActive: Boolean,
  },
};
</script>
