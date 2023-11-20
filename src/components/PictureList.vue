<!--<template>-->
<!--  <template v-for="picture in pictureList">-->
<!--    <a-card hoverable style="width: 240px">-->
<!--      <template #cover>-->
<!--        <img alt="example" :src="picture.murl" />-->
<!--      </template>-->
<!--      <a-card-meta :title="picture.title">-->
<!--        <template #description>www.instagram.com</template>-->
<!--      </a-card-meta>-->
<!--    </a-card>-->
<!--  </template>-->
<template>
  <template v-if="pictureList">
    <a-list
      item-layout="horizontal"
      :grid="{ gutter: 16, xs: 1, sm: 2, md: 4, lg: 4, xl: 6, xxl: 3 }"
      :data-source="props.pictureList"
    >
      <template #renderItem="{ item }">
        <a-list-item>
          <a-card hoverable style="width: 240px">
            <template #cover>
              <img :src="item.murl" />
            </template>
            <a-card-meta :title="item.title" />
          </a-card>
        </a-list-item>
      </template>
    </a-list>
  </template>
</template>
<script setup lang="ts">
// eslint-disable-next-line no-undef
const props = defineProps<{
  pictureList: any[];
}>();
</script>
<style scoped></style>
