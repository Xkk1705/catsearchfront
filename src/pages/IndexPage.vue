<template>
  <div class="home">
    <a-space direction="vertical" class="searchTba">
      <a-input-search
        v-model:value="searchText"
        placeholder="input search text"
        enter-button="Search"
        size="large"
        @search="onSearch"
      />
    </a-space>
    <div style="margin-bottom: 5px"></div>
    <a-tabs
      v-model:activeKey="activeKey"
      centered
      @change="doChangeTab"
      class="fenyetab"
    >
      <a-tab-pane key="post" tab="文章">
        <PostList :post-list="postListData" />
      </a-tab-pane>
      <a-tab-pane key="picture" tab="图片" force-render>
        <PictureList />
      </a-tab-pane>
      <a-tab-pane key="user" tab="用户">
        <UserList :user-list="userListData" />
        {{ userListData }}
      </a-tab-pane>
    </a-tabs>
  </div>
</template>

<script setup lang="ts">
import { onMounted, ref, watchEffect } from "vue";
import { useRouter } from "vue-router";
import PictureList from "@/components/PictureList.vue";
import UserList from "@/components/UserList.vue";
import PostList from "@/components/PostList.vue";
import myAxios from "@/plugins/myAxios";

const router = useRouter();

const searchText = ref<string>("");
const activeKey = ref("post");
const postListData = ref([]);
const userListData = ref([]);
const pictureListData = ref([]);
const initParams = ref({
  type: activeKey.value,
  text: searchText.value,
  pageSize: 10,
  pageNum: 1,
});

// 加载单类数据
const onLoadData = async (params: any) => {
  const postQuery = {
    ...params,
    searchText: params.text,
  };
  const postRes: any = await myAxios
    .post("/post/list/page/vo", postQuery)
    .then((postRes) => {
      postListData.value = postRes.records;
    });

  const userQuery = {
    ...params,
    userName: params.text,
  };
  const userRes: any = await myAxios
    .post("/user/list/page/vo", userQuery)
    .then((userRes) => {
      userListData.value = userRes.records;
    });

  const pictureQuery = {
    ...params,
    searchText: params.text,
  };
  const pictureRes: any = await myAxios
    .post("/picture/list/page/vo", pictureQuery)
    .then((pictureRes) => {
      pictureListData.value = pictureRes.records;
    });
};
const searchParams = ref(initParams);
// eslint-disable-next-line no-undef
watchEffect(() => {
  searchParams.value = {
    ...initParams,
    text: searchText.value,
    type: activeKey.value,
  } as any;
  onLoadData(searchParams.value);
});
// onMounted(async () => {
//   const postRes: any = await myAxios
//     .post("/post/list/page/vo", {})
//     .then((postRes) => {
//       postListData.value = postRes.records;
//     });
//
//   const userRes: any = await myAxios
//     .post("/user/list/page/vo", {})
//     .then((userRes) => {
//       userListData.value = userRes.records;
//     });
// });
const onSearch = (searchValue: string) => {
  router.push({
    name: "home",
    query: {
      type: activeKey.value,
      text: searchValue,
      pageSize: 10,
      pageNum: 1,
    },
  });
};

const doChangeTab = () => {
  router.push({
    path: `/${activeKey.value}`,
    query: {
      type: activeKey.value,
      text: searchText.value,
      pageSize: 10,
      pageNum: 1,
    },
  });
};
</script>

<style scoped>
.searchTba {
  width: 80%;
}

.fenyetab {
  width: 100%;
}
</style>
