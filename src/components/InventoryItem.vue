<template>
    <div class="inventoryItem" :class="{disabled:!item?.quantity}" @click="$emit('open',item)">
        <img :src="item?.img as string"/>
        <p :class="[(item?.quantity !== 0) ? 'inventoryItem__quantity' : 'inventoryItem__quantity__zero']">{{ item?.quantity }}</p>
    </div>
</template>

<script setup lang="ts">
import { defineProps,defineEmits} from 'vue'
import type { InventoryItemType } from '../types'
import type {PropType} from 'vue'

defineProps({
    item:{
        type:Object as PropType<InventoryItemType>,
    }
})
defineEmits(['open'])
</script>

<style scoped>
.inventoryItem {
    width: 105px;
    height: 100px;
    border: 1px solid rgba(77, 77, 77, 1);
    cursor: pointer;
    text-align: center;
    position: relative;
}
.disabled {
    pointer-events: none;
    opacity: 0.4;
}
.inventoryItem__quantity {
    position: absolute;
    color: white;
    font-weight: 500;
    font-size: 10px;
    bottom: 0px;
    right: 0px;
    margin: 0;
    border: 1px solid rgba(77, 77, 77, 1);
    border-top-left-radius:6px;
    width: 16px;
    height: 16px;
}
.inventoryItem__quantity__zero {
    display: none;
}
.inventoryItem:hover {
    background: rgba(47, 47, 47, 1);
}
</style>