<template>
  <RouterView>
    <template #default="{ Component, route }">
      <keep-alive v-if="openCache" :include="getCaches">
        <component :is="Component" :key="route.fullPath" />
      </keep-alive>
      <component v-else :is="Component" :key="route.fullPath" />
    </template>
  </RouterView>
  <FrameLayout v-if="getCanEmbedIFramePage" />
</template>

<script lang="ts" setup>
  import { computed, unref } from 'vue';

  import FrameLayout from '@/layouts/iframe/index.vue';

  import { useRootSetting } from '@/hooks/setting/useRootSetting';

  import { useMultipleTabSetting } from '@/hooks/setting/useMultipleTabSetting';


  defineOptions({ name: 'PageLayout' });

  const { getShowMultipleTab } = useMultipleTabSetting();

  const { getOpenKeepAlive, getCanEmbedIFramePage } = useRootSetting();

  const openCache = computed(() => unref(getOpenKeepAlive) && unref(getShowMultipleTab));

  const getCaches = []
</script>
