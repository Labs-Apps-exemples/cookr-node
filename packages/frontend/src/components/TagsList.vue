<template>
  <ul>
    <li v-for="(tag, i) in tags" :key="i" class="inline-flex mr-2 my-1">
      <Tag v-bind="tag" />
    </li>
  </ul>
</template>

<script lang="ts" setup>
defineProps({
  tags: {
    type: Array,
    required: true,
  },
});
</script>
