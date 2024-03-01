<script setup lang="ts" generic="T extends any, O extends any">
defineOptions({
  name: 'IndexPage',
})

const listData:string[] = [
  '一',
  '二',
  '三',
  '四',
  '五',
  '六',
  '七',
  '八',
  '九',
];


</script>

<template>
  <div>
    <div
      i-carbon-campsite
      inline-block
      text-4xl
    />
    <p>
      <a rel="noreferrer" href="https://github.com/antfu/vitesse-lite" target="_blank">
        Vitesse Lite
      </a>
    </p>
    <p>
      <em text-sm op75>This is a draggable list component</em>
    </p>
        <p>
        <em text-sm op75>Props: [
    "一",&nbsp;
    "二",&nbsp;
    "三",&nbsp;
    "四",&nbsp;
    "五",&nbsp;
    "六",&nbsp;
    "七",&nbsp;
    "八",&nbsp;
    "九"
  ]</em>
      </p>
    <DraggableList :list-data="listData" />
    <div py-4 />
  </div>
</template>
