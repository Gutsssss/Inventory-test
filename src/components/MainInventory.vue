<template>
    <div
    v-for="item,index in itemsArr"
    :key="item.id"
    draggable="true"
    @dragstart="$emit('dragStart',$event,item,index)"
    @drop="$emit('dragDrop',$event,index)"
    @dragend.prevent
    @dragover.prevent
    >
        <InventoryItem :item="item" @open="openDialog"/>
    </div>
    <ModalItem class="MainInventory__modal" @close-modal="showDialog = !showDialog" :item="itemData as InventoryItemType" v-model:showDialog="showDialog" @delete-item-quantity="deleteQuantity"/>
</template>

<script setup lang="ts">
import { defineProps,defineEmits, ref } from 'vue';
import type { InventoryItemType } from '../types';
import InventoryItem from './InventoryItem.vue';
import ModalItem from './ModalItem.vue';

const itemData = ref({})
const showDialog = ref(false)
const openDialog = (item:Object) => {
    itemData.value = item
    showDialog.value = true
}
defineProps({
    itemsArr:{
        type:Array<InventoryItemType>
    }
})
const emit = defineEmits(['dragStart','dragDrop','deleteQuantity'])
const deleteQuantity = (quantity:Number,item:InventoryItemType) =>{
    emit('deleteQuantity',quantity,item)
    showDialog.value = false
}
</script>

<style scoped>
.MainInventory {
    position: relative;
}
</style>