<script setup>
import { useFoodStore } from '@/store/food';
const foodStore = useFoodStore();

const filterMenu = ref('all');

const filteredMenu = computed(() => {
  if (filterMenu.value === 'all' || !filterMenu.value) {
    return foodStore.foods;
  }
  else if (filterMenu.value === 'food' || !filterMenu.value) {
    return foodStore.foods.filter((menu) => menu.type === "food");
  }
  else if (filterMenu.value === 'sauce' || !filterMenu.value) {
    return foodStore.foods.filter((menu) => menu.type === "sauce");
  }
  else if (filterMenu.value === 'drink' || !filterMenu.value) {
    return foodStore.foods.filter((menu) => menu.type === "drink");
  }
  return foodStore.foods.filter((menu) => menu.type === filterMenu.value);
});

</script>
<template>
  <VCard>
    <VCardItem>
      <VCardTitle>
        รายการเมนูอาหารในร้านทั้งหมด        
      </VCardTitle>
    </VCardItem>
    <VCardItem>
      <VRow>
        <VCol cols="3">
          <VBtn @click="filterMenu='all'" color="primary" prepend-icon="mdi-list-box" block height="50">ทั้งหมด</VBtn>  
        </VCol>
        <VCol cols="3">
          <VBtn @click="filterMenu='food'" color="purple" prepend-icon="mdi-food" block height="50">เมนูบุฟเฟต์ / อาหาร</VBtn>  
        </VCol>
        <VCol cols="3">
          <VBtn @click="filterMenu='sauce'" color="green" prepend-icon="mdi-pot" block height="50">น้ำจิ้ม / น้ำซุป</VBtn>  
        </VCol>
        <VCol cols="3">
          <VBtn @click="filterMenu='drink'" color="red" prepend-icon="mdi-beer" block height="50">เครื่องดื่ม / อื่น ๆ</VBtn>  
        </VCol>
      </VRow>          
    </VCardItem>
    <VCardItem>
      <VDataTable :items="filteredMenu">
        <template v-slot:item.image="{ item }">
          <VCard class="my-2" elevation="2" rounded>
            <VImg :src="item.image" height="64"></VImg>
          </VCard>
        </template>
        <template v-slot:item.name="{ item }">
          <h4>{{ item.name }}</h4>
        </template>
        <template v-slot:item.price="{ item }">
          <h4>{{ item.price }} บาท</h4>
        </template>
      </VDataTable>  
    </VCardItem>
  </VCard>
</template>
