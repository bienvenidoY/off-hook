<template>
  <div class="flex flex-col items-center py-4 flex-shrink-0 w-80px bg-gray-700">
    <a href="#"
       class="flex items-center justify-center h-12 w-12 bg-indigo-100 text-indigo-800 rounded-full mt-12">
      <h1 class="font-bold">P</h1>
    </a>
    <ul class="flex flex-col space-y-2 mt-12">

      <li v-for="item in menus" :key="item.path">
        <RouterLink :to="item.path" class="flex items-center lodePage" data="pass_list">
                        <span class="flex items-center justify-center text-indigo-100 hover:bg-indigo-700 h-12 w-12 rounded-2xl">
                         {{ item.path }}
                        </span>
        </RouterLink>
      </li>
    </ul>
    <div @click="handleLoginOut" class="mt-auto flex items-center justify-center hover:text-indigo-100 text-indigo-500 h-10 w-10">
      <span class="text-white text-xs">退 出</span>
    </div>
  </div>
</template>
<script setup lang="ts">
import { RouterLink } from 'vue-router'
import { useUserStore } from '@/store/modules/user';
import {useSplitMenu} from "@/layouts/default/SimpleSider/useLayoutMenu";
import {toRef, defineProps, PropType, unref, computed} from "vue";
import {MenuSplitTyeEnum} from "@/enums/menuEnum";
const userStore = useUserStore();
const props = defineProps({
  splitType: {
    type: Number as PropType<MenuSplitTyeEnum>,
    default: MenuSplitTyeEnum.NONE,
  },
})

const { menusRef } = useSplitMenu(toRef(props, 'splitType'));
const menus = computed(() => {
  console.log(unref(menusRef))
  return unref(menusRef)
})
//  login out
function handleLoginOut() {
  userStore.confirmLoginOut();
}
</script>
