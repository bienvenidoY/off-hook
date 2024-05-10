<template>
  <div :class="prefixCls" class="relative w-full h-full px-4 bg-purple-400 flex justify-center items-center overflow-hidden">
    <div class="absolute w-60 h-60 rounded-xl bg-purple-300 -top-5 -left-16 z-0 transform rotate-45 hidden md:block"></div>
    <div class="absolute w-48 h-48 rounded-xl bg-purple-300 -bottom-6 -right-10 transform rotate-12 hidden md:block"></div>

    <div class="relative pt-12 pb-3 px-12 bg-fff rounded-2xl shadow-xl z-20 w-[440px]">
      <LoginForm />
    </div>
    <div class="w-40 h-40 absolute bg-purple-300 rounded-full top-0 right-12 hidden md:block"></div>
    <div class="w-20 h-40 absolute bg-purple-300 rounded-full bottom-20 left-10 transform rotate-45 hidden md:block"></div>
  </div>
</template>
<script lang="ts" setup>
  import { AppDarkModeToggle, AppLocalePicker } from '@/components/Application';
  import { useGlobSetting } from '@/hooks/setting';
  import { useDesign } from '@/hooks/web/useDesign';
  import { useLocaleStore } from '@/store/modules/locale';
  import { computed } from 'vue';
  import LoginForm from './LoginForm.vue';

  defineProps({
    sessionTimeout: {
      type: Boolean,
    },
  });

  const globSetting = useGlobSetting();
  const { prefixCls } = useDesign('login');
  const localeStore = useLocaleStore();
  const title = computed(() => globSetting?.title ?? '');
</script>
<style lang="less">
  @prefix-cls: ~'@{namespace}-login';
  @logo-prefix-cls: ~'@{namespace}-app-logo';
  @countdown-prefix-cls: ~'@{namespace}-countdown-input';
  @dark-bg: #293146;

  .@{prefix-cls} {
    min-height: 100%;
    overflow: hidden;
    .@{prefix-cls}-form {
      background-color: #fff;
      width: 450px;
    }

    .@{logo-prefix-cls} {
      position: absolute;
      top: 12px;
      height: 30px;

      &__title {
        color: #fff;
        font-size: 16px;
      }

      img {
        width: 32px;
      }
    }

    .container {
      .@{logo-prefix-cls} {
        display: flex;
        width: 60%;
        height: 80px;

        &__title {
          color: #fff;
          font-size: 24px;
        }

        img {
          width: 48px;
        }
      }
    }

    &-sign-in-way {
      .anticon {
        color: #888;
        font-size: 22px;
        cursor: pointer;

        &:hover {
          color: @primary-color;
        }
      }
    }



    .@{countdown-prefix-cls} input {
      min-width: unset;
    }
  }
</style>
