<template>
  <template v-if="props.userList">
    <a-list item-layout="horizontal" :data-source="props.userList">
      <template #renderItem="{ item }">
        <a-list-item>
          <a-list-item-meta :description="item.userProfile">
            <template #title>
              <a href="https://www.antdv.com/">{{ item.userName }}</a>
            </template>
            <template #avatar>
              <a-avatar :src="item.userAvatar" />
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
  userList: any[];
}>();
</script>

<style scoped></style>
