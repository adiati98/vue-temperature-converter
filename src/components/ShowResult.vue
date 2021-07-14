<template>
<section id="show-result">
  <p class="result">{{ result }}</p>
  <p class="message">{{ message }}</p>
</section>
</template>

<script>
export default {
  props: [ 'result', 'message' ]
}
</script>

