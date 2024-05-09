<template>
  <Layout :class="prefixCls">
    <Layout :class="[layoutClass, `${prefixCls}-out`]">
      <LayoutSideBar />
      <Layout :class="`${prefixCls}-main`">
        <LayoutContent />
      </Layout>
    </Layout>
  </Layout>
</template>

<script lang="ts" setup>
  import { computed, unref } from 'vue';
  import { Layout } from 'ant-design-vue';
  import { createAsyncComponent } from '@/utils/factory/createAsyncComponent';

  import LayoutContent from './content/index.vue';
  import LayoutSideBar from './SimpleSider/index.vue';

  import { useHeaderSetting } from '@/hooks/setting/useHeaderSetting';
  import { useMenuSetting } from '@/hooks/setting/useMenuSetting';
  import { useDesign } from '@/hooks/web/useDesign';

  import { useAppInject } from '@/hooks/web/useAppInject';

  import { useMultipleTabSetting } from '@/hooks/setting/useMultipleTabSetting';

  defineOptions({ name: 'DefaultLayout' });

  const { prefixCls } = useDesign('default-layout');
  const { getShowFullHeaderRef } = useHeaderSetting();
  const {  getIsMixSidebar, getShowMenu } = useMenuSetting();
  const { getAutoCollapse } = useMultipleTabSetting();

  const layoutClass = computed(() => {
    let cls: string[] = ['ant-layout'];
    if (unref(getIsMixSidebar) || unref(getShowMenu)) {
      cls.push('ant-layout-has-sider');
    }

    if (!unref(getShowMenu) && unref(getAutoCollapse)) {
      cls.push('ant-layout-auto-collapse-tabs');
    }

    return cls;
  });
</script>
<style lang="less">
  @prefix-cls: ~'@{namespace}-default-layout';

  .@{prefix-cls} {
    display: flex;
    flex-direction: column;
    width: 100%;
    min-height: 100%;
    background-color: @content-bg;

    > .ant-layout {
      min-height: 100%;
    }

    &-main {
      width: 100%;
      margin-left: 1px;
    }
  }

  .@{prefix-cls}-out {
    &.ant-layout-has-sider {
      .@{prefix-cls} {
        &-main {
          margin-left: 1px;
        }
      }
    }
  }
</style>
