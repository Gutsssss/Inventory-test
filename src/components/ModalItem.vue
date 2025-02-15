<template>
  <div class="modal" v-show="showDialog">
    <img @click="closeModal" class="close_btn" src="../assets/close.svg"/>
    <img
      style="width: 130px; height: 130px; margin: auto"
      :src="item?.img as string"
    />
    <SkeletonItem/>
    <div class="buttons">
      <button
        class="mainDeleteButton"
        v-show="!showAnotherButtons"
        @click="showAnotherButtons = true"
      >
        Удалить предмет
      </button>
      <div v-show="showAnotherButtons" class="buttons__delete">
        <input
          class="buttons__delete__input"
          placeholder="Введите количество"
          v-model="quantityForDelete"
        />
        <button class="buttons__delete__cancel" @click="showAnotherButtons = false">Отмена</button>
        <button class="buttons__delete__withQuantity" @click="deleteItemQuantity(quantityForDelete,item as InventoryItemType)">
          Подтвердить
        </button>
      </div>
    </div>
    
  </div>
</template>

<script setup lang="ts">
import { defineProps, ref, defineEmits } from "vue";
import type { InventoryItemType } from "../types";
import type { PropType } from "vue";
import SkeletonItem from "./SkeletonItem.vue";
defineProps({
  item: {
    type: Object as PropType<InventoryItemType>,
  },
  showDialog: {
    type: Boolean,
    default: false,
  },
});
const showAnotherButtons = ref(false);
const quantityForDelete = ref(null);
const emit = defineEmits(["deleteItemQuantity",'closeModal']);
const deleteItemQuantity = (quantity:Number | null,item:InventoryItemType | null) => {
    emit('deleteItemQuantity', quantity, item)
    quantityForDelete.value = null
    showAnotherButtons.value = false
}
const closeModal = () => {
  emit('closeModal')
  showAnotherButtons.value = false
}

</script>

<style scoped>
.modal {
  display: flex;
  width: 250px;
  height: 507px;
  flex-direction: column;
}
.buttons__delete {
  display: grid;
  grid-template-columns: 2fr 1fr 1fr;
  gap: 10px;
  padding: 10px;
  
}
.buttons__delete__input {
  grid-column-start: 1;
  grid-column-end: 4;
  grid-row-start: 1;
  grid-row-end: 3;
  padding: 10px;
  background:rgba(38, 38, 38, 1);
  border-radius: 5px;
  color:rgba(77, 77, 77, 1);
  font-weight: 500;
}
.mainDeleteButton {
  width: 220px;
  height: 39px;
  background: rgba(250, 114, 114, 1);
  color: white;
  border-radius: 8px;
  padding: 0;
  margin:18px;
}
.buttons__delete__cancel {
    border-radius: 8px;
    color: rgba(45, 45, 45, 1);
    height: 33px;
    width: 88px;
}
.buttons__delete__withQuantity {
    border-radius: 8px;
    color: white;
    height: 33px;
    width: 112px;
    background: rgba(250, 114, 114, 1);
}
.close_btn {
    width: 12px;
    height: 12px;
    position: absolute;
    top: 0;
    right: 0;
    padding: 10px;
}
</style>
