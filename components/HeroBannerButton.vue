<template>
  <div>
    <button
      :href="callToActionUrl"
      class="hover:bg-primary-light"
    >
      {{ callToActionName }}
    </button>
  </div>
</template>

<script>
  export default {
    props: {
      callToActionName: {
        type: String,
        default: 'call to action'
      },
       callToActionUrl: {
        type: String,
        default: 'call to action'
      },
    },
  }
</script>

<style lang="postcss" scoped>
.btn {
  @apply bg-primary text-dark text-xl rounded-full my-12 py-4 w-48 mx-3 inline-block;
}
</style>
