<template>
  <div class="App">
  <LeftLayout/>
  <div class="App__mainInventory">
    <MainInventory  :items-arr="inventoryItems" @drag-start="startDrag" @drag-drop="onDrop" @delete-quantity="deleteQuantity" />
  </div>
</div>
<BottomLayout/>
</template>

<script setup lang="ts">
import { ref, watch } from 'vue';
import img1 from './assets/img1.svg'
import img2 from './assets/img2.svg'
import img3 from './assets/img3.svg'
import type {InventoryItemType} from './types'
import MainInventory from './components/MainInventory.vue';
import LeftLayout from './components/LeftLayout.vue';
import BottomLayout from './components/BottomLayout.vue';
const inventoryItems = ref([
    {id:1,img:img1,quantity:4},
    {id:2,img:img2,quantity:2},
    {id:3,img:img3,quantity:5},
    {id:4,img:null,quantity:0},
    {id:5,img:null,quantity:0},
    {id:6,img:null,quantity:0},
    {id:7,img:null,quantity:0},
    {id:8,img:null,quantity:0},
    {id:9,img:null,quantity:0},
    {id:10,img:null,quantity:0},
    {id:11,img:null,quantity:0},
    {id:12,img:null,quantity:0},
    {id:13,img:null,quantity:0},
    {id:14,img:null,quantity:0},
    {id:15,img:null,quantity:0},
    {id:16,img:null,quantity:0},
    {id:17,img:null,quantity:0},
    {id:18,img:null,quantity:0},
    {id:19,img:null,quantity:0},
    {id:20,img:null,quantity:0},
    {id:21,img:null,quantity:0},
    {id:22,img:null,quantity:0},
    {id:23,img:null,quantity:0},
    {id:24,img:null,quantity:0},
    {id:25,img:null,quantity:0},
])

function swap(arr: Array<InventoryItemType>, a: number, b: number) {
  [arr[a],arr[b]] = [arr[b],arr[a]]
}

const startDrag = (event: any, item: InventoryItemType) => {
  event.dataTransfer.dropEffect = 'move';
  event.dataTransfer.effectAllowed = 'move';
  event.dataTransfer.setData('itemID', item?.id);
};

const savedItems = localStorage.getItem('inventoryItem')
if(savedItems) {
  inventoryItems.value = JSON.parse(savedItems)
}
const onDrop = async (event: any, index: any) => {
  const itemID = event.dataTransfer.getData('itemID');

  const getSwapIndex = inventoryItems.value.findIndex(item => item.id == itemID);
   
  if (getSwapIndex !== -1) {
    swap(inventoryItems.value, getSwapIndex, index);
  }
};
const deleteQuantity = (quantity:Number | any,itemIn:InventoryItemType) => {
  inventoryItems.value.find(item => {
    if(item.id === itemIn.id) {
      item.quantity = item.quantity - quantity
    }
  })
}
watch(inventoryItems.value,(newVal) => {
  localStorage.setItem('inventoryItem',JSON.stringify(newVal))
})
</script>

<style >

</style>