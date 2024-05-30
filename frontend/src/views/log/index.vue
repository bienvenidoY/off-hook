<template>
  <div class="mt-2.5 flex flex-1 flex-col md:mt-4">
    <ul class="logs-panel">
      <li class="inline-block text-[11px] leading-5" :key="index" v-for="(log, index) in logs">
        <span class="mr-2 text-orange-400">[{{ dayjs(log.time).format('YYYY-MM-DD HH:mm:ss') }}]</span>
        <span class={logMap.get(log.type)}>[{{ log.type.toUpperCase()} }]</span>
        <span> { { log.payload  }}</span>
      </li>
    </ul>
  </div>
</template>
<script>
import dayjs from 'dayjs'

const logs = ref([])

</script>
