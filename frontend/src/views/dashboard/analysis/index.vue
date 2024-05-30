<template>
  <div class="p-4">
    <div class="w-full mt-10">
      <template v-if="list.length">
        <!--  新增    -->
        <div class="flex items-center justify-between">
          <h1 class="text-xl font-bold text-white/50 md:text-2xl">账号</h1>
          <div class="mr-5">
            <div class="flex items-center cursor-pointer" @click="openLogin">
              <span class="flex pa-2 items-center justify-center text-indigo-100 hover:bg-indigo-700 rounded-2xl">
                <UserAddOutlined :style="{fontSize: '24px',}"/>
              </span>
            </div>
          </div>
        </div>
        <!--  表格    -->
        <div class="mt-5 hidden font-mono">
          <div class="bg-gray-600 shadow-md px-5 pt-5 pb-8 mb-4 flex flex-col my-2 text-white">
            <div class="-mx-3 md:flex mb-6">
              <div class="md:w-1/2 px-3 mb-6 md:mb-0">
                <label class="block uppercase tracking-wide text-grey-darker text-xs font-bold mb-2"
                       for="grid-mark">
                  标 识
                </label>
                <input
                  class="appearance-none text-black block w-full bg-grey-lighter text-grey-darker border border-red py-1 px-2 mb-1"
                  id="grid-mark" type="text" placeholder="Jane">
                <p class="text-red-500 text-xs" id="grid-mark-msg"></p>
              </div>
              <div class="md:w-1/2 px-3">
                <label class="block uppercase tracking-wide text-grey-darker text-xs font-bold mb-2"
                       for="grid-username">
                  账 号
                </label>
                <input
                  class="appearance-none text-black block w-full bg-grey-lighter text-grey-darker border border-grey-lighter py-1 px-2"
                  id="grid-username" type="text" placeholder="Doe">
              </div>
            </div>
            <div class="-mx-3 md:flex mb-6">
              <div class="md:w-full px-3">
                <label class="block uppercase tracking-wide text-grey-darker text-xs font-bold mb-1"
                       for="grid-password">
                  密 码
                </label>
                <input
                  class="appearance-none text-black block w-full bg-grey-lighter text-grey-darker border border-grey-lighter rounded py-1 px-2 mb-1"
                  id="grid-password" type="text" placeholder="******************">
                <p class="text-red-500 text-xs" id="grid-password-msg"></p>
              </div>
            </div>
            <div class="-mx-3 md:flex mb-6">
              <div class="md:w-full px-3">
                <button onclick="CreatePassword()"
                        class="md:w-1/12 px-1 mb-1 text-xs bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 rounded">
                  添 加
                </button>
              </div>
            </div>
          </div>
        </div>
        <section class="container mx-auto font-mono mt-4">
          <div class="w-full mb-8 overflow-y-scroll  shadow-lg">
            <div class="w-full overflow-x-auto">
              <table class="w-full bg-gray-700">
                <thead>
                <tr
                  class="text-md font-semibold tracking-wide text-left text-white bg-gray-700 uppercase border-b border-gray-900">
                  <th class="px-4 py-3">id</th>
                  <th class="px-4 py-3">账号名称</th>
                  <th class="px-4 py-3">手机号</th>
                  <th class="px-4 py-3">wxid</th>
                  <th class="px-4 py-3">pid</th>
                  <th class="px-4 py-3">操作</th>
                </tr>
                </thead>
                <tbody class="bg-gray-600" id="password_list">
                <tr class="text-white border border-gray-400 hover:bg-gray-400">
                  <td class="px-4 py-3">[item.id]</td>
                  <td class="px-4 py-3 text-xs">
                  <span
                    class="px-2 py-1 font-semibold leading-tight text-green-700 bg-green-100 rounded-sm">[item.corp_short_name]</span>
                  </td>
                  <td class="px-4 py-3 text-ms font-semibold">[item.mobile ]</td>
                  <td class="px-4 py-3 text-ms font-semibold">[item.wxid ]</td>
                  <td class="px-4 py-3 text-ms font-semibold">[item.pid ]</td>
                  <td class="px-4 py-3 text-sm">
               <span
                 class="rounded-[10px] px-3 py-1 cursor-pointer hover:text-indigo-700 hover:bg-slate-50">
                  <PoweroffOutlined class="" @click="quit({id: 2})"/>
                </span>
                  </td>
                </tr>
                <tr class="text-white border border-gray-400 hover:bg-gray-400">
                  <td class="px-4 py-3">[item.id]</td>
                  <td class="px-4 py-3 text-xs">
                  <span
                    class="px-2 py-1 font-semibold leading-tight text-green-700 bg-green-100 rounded-sm">[item.corp_short_name]</span>
                  </td>
                  <td class="px-4 py-3 text-ms font-semibold">[item.mobile ]</td>
                  <td class="px-4 py-3 text-ms font-semibold">[item.wxid ]</td>
                  <td class="px-4 py-3 text-ms font-semibold">[item.pid ]</td>
                  <td class="px-4 py-3 text-sm">
                <span
                  class="rounded-[10px] px-3 py-1 cursor-pointer hover:text-indigo-700 hover:bg-slate-50">
                  <PoweroffOutlined class="" @click="quit({id: 2})"/>
                </span>
                  </td>
                </tr>
                </tbody>
              </table>
            </div>
          </div>
        </section>
      </template>

      <!--  无结果页面    -->
     <div class=" w-full flex flex-col items-center mt-48">
       <h1 class="mt-4 text-2xl font-bold tracking-tight text-white">您还未添加账号</h1>
       <div class="mt-1 cursor-pointer w-[180px] flex items-center justify-center rounded-md bg-indigo-600 px-3 py-2 text-[0.8125rem] font-semibold leading-5 text-white hover:bg-indigo-500">
         <UserAddOutlined :style="{fontSize: '18px',}" class="mr-2"/><span>立即添加账号</span>
       </div>
     </div>
    </div>
  </div>
</template>
<script lang="ts" setup>
import { ref } from 'vue'
import {PoweroffOutlined, UserAddOutlined} from '@ant-design/icons-vue';


const list = ref([])

function openLogin() {

}

function quit(item) {
  console.log(item)
}
</script>
