<script setup>
import { ref } from 'vue'

const userItems = [
  { id: 1, name: "Shoes 1" },
  { id: 2, name: "Shoes 2" },
  { id: 3, name: "Shoes 3" },
  { id: 4, name: "Shoes 4" },
  { id: 5, name: "T-shirt 1" },
  { id: 6, name: "T-shirt 2" },
  { id: 7, name: "T-shirt 3" },
  { id: 8, name: "T-shirt 4" }
]

const choiceItems = [
  { id: 11, name: "Jacket 1" },
  { id: 12, name: "Jacket 2" },
  { id: 13, name: "Jacket 3" },
  { id: 14, name: "Jacket 4" },
  { id: 15, name: "Hoodie 1" },
  { id: 16, name: "Hoodie 2" },
  { id: 17, name: "Hoodie 3" },
  { id: 18, name: "Hoodie 4" }
]

const selectedUser = ref([])
const selectedChoice = ref(null)

function selectUserItem(item) {
  if (selectedUser.value.length < 6 && !selectedUser.value.some(i => i.id === item.id)) {
    selectedUser.value.push(item)
  }
}

function selectChoiceItem(item) {
  selectedChoice.value = item
}
</script>

<template>
  <div class="container">
    <div class="block top-left">
      <h3>Selected User Items</h3>
      <div v-for="item in selectedUser" :key="item.id" class="item">
        {{ item.name }}
      </div>
    </div>
    <div class="block top-right">
      <h3>Selected Choice Item</h3>
      <div v-if="selectedChoice" class="item">
        {{ selectedChoice.name }}
      </div>
    </div>
    <div class="block bottom-left">
      <h3>User Items</h3>
      <div v-for="item in userItems" :key="item.id" class="item selectable" @click="selectUserItem(item)">
        {{ item.name }}
      </div>
    </div>
    <div class="block bottom-right">
      <h3>Choice Items</h3>
      <div v-for="item in choiceItems" :key="item.id" class="item selectable" @click="selectChoiceItem(item)">
        {{ item.name }}
      </div>
    </div>
  </div>
</template>

<style scoped>
.container {
  display: grid;
  grid-template-areas:
    "top-left top-right"
    "bottom-left bottom-right";
  grid-template-columns: 1fr 1fr;
  grid-template-rows: auto auto;
  gap: 20px;
  padding: 20px;
  height: 100vh;
  box-sizing: border-box;
}

.block {
  border: 1px solid #ccc;
  padding: 10px;
  display: flex;
  flex-direction: column;
}

.top-left {
  grid-area: top-left;
}

.top-right {
  grid-area: top-right;
}

.bottom-left {
  grid-area: bottom-left;
}

.bottom-right {
  grid-area: bottom-right;
}

.item {
  padding: 5px;
  margin: 2px 0;
  background-color: #f9f9f9;
  border-radius: 4px;
}

.selectable {
  cursor: pointer;
}

.selectable:hover {
  background-color: #e0e0e0;
}
</style>
