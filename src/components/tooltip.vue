<template>
  <div class="absolute">
    <div class="tt top">
      <h3 class="font-bold" v-if="headline">{{ headline }}</h3>
      <hr class="mb-2 mt-1" v-if="headline" />
      <p class="text-sm" v-if="text">{{ text }}</p>
      <i></i>
    </div>
  </div>
</template>

<script>
  export default {
    name: "tooltip",
    props: {
      headline: String,
      text: String
    }
  }
</script>

<style scoped>
.tt {
  position:absolute;
  text-align:left;
}

.tt.top {
  background-color: #ffffff;
  position:absolute;
  z-index:99999999;
  box-sizing:border-box;
  @apply rounded-md border border-gray-200 min-w-80 max-w-fit p-4;
}

.tt:hover .top {
  display:block;
}
</style>