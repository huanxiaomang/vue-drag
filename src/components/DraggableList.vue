<script setup lang='ts'>
import { Ref } from 'vue';
const props = defineProps<{ listData: string[] }>();

const targetItem = ref<HTMLDivElement>();
let targetIndex: number;
const dragContainer = ref<HTMLDivElement>();
// const itemCount: number = 7;
const listData = ref(props.listData) as Ref<string[]>;
// useStorage('list-data',listData);

const colorList = [
  'bg-yellow-300',
  'bg-blue-300',
  'bg-green-300',
  'bg-red-300',
  'bg-orange-300',
  'bg-pink-300',
  'bg-purple-300',
  'bg-gray-300',
]
const map: Map<string, number> = new Map();
listData.value.map((val, i) => {
  map.set(val, i % colorList.length);
})

function getClass(data: string) {

  return colorList[map.get(data)!];
}



function handleDragEnter(e: DragEvent) {
  const target = e.target as any;

  if (target && target.parentElement.className === 'container') {
    const { key } = target.dataset
    targetItem.value = target

    targetIndex = parseInt(key);

  }
}

function handleDragEnd(e: DragEvent, dragIndex: number) {
  const dragTarget = e.target;
  if (dragTarget) {
    insert(dragIndex);
  }
  (e.target as any).style.opacity = 1;
}

function insert(dragIndex: number) {
  if (dragIndex > targetIndex) {

    listData.value.splice(targetIndex, 0, listData.value[dragIndex]);
    listData.value = listData.value.filter((_, i) => i !== dragIndex + 1);

  }
  else if (dragIndex < targetIndex) {
    listData.value.splice(targetIndex + 1, 0, listData.value[dragIndex]);
    listData.value = listData.value.filter((_, i) => i !== dragIndex);

  }
}

function handleDragStart(e: any) {
  e.target.style.opacity = 0.6;
  }

watchEffect(() => {


})
</script>

<template>
  <div ref="dragContainer" class="container" @dragover.prevent @dragenter="handleDragEnter($event)">
    <TheItem v-for="(data, i) in listData" :key="data" draggable="true" :item-class="getClass(data)" :data-key="i"
      @dragend="handleDragEnd($event, i)" @dragstart="handleDragStart($event)">
      {{ data }}
    </TheItem>
  </div>
</template>

<style lang="less" scoped></style>
