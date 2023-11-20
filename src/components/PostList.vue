<template>
  <template v-if="props.postList">
    <a-list item-layout="horizontal" :data-source="props.postList">
      <template #renderItem="{ item }">
        <a-list-item>
          <a-list-item-meta :description="item.content">
            <template #title>
              <a href="https://www.antdv.com/">{{ item.title }}</a>
            </template>
            <template #avatar>
              <a-avatar :src="paiqiu" />
            </template>
          </a-list-item-meta>
        </a-list-item>
      </template>
    </a-list>
  </template>
</template>

<script setup lang="ts">
import paiqiu from "../assets/paiqiu.jpeg";
// eslint-disable-next-line no-undef
const props = defineProps<{
  postList: any[];
}>();
</script>

<style scoped></style>
