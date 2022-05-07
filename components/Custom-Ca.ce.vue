<template>
  <div class="custom-ca">
    {{ acto }}
  </div>
</template>

<script setup>
import { ref } from "vue";
const acto = ref(props.act)
console.log('usa', acto.value)
const props = defineProps({
  act: {
    type: String,
    default: "false",
  },
});

</script>
<style scoped>

.custom-ca {
  background-color: #ca981a;
}
</style>
