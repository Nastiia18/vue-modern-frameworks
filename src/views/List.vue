<script setup lang="ts">
import { ref } from 'vue'

const shoppingList = ref([
  { id: 1, title: 'Apples', bought: false },
  { id: 2, title: 'Bananas', bought: false },
  { id: 3, title: 'Tomato', bought: false }
])

const settingsSelection = ref([])
const newItemTitle = ref('')

const doneBought = (id: number) => {
  const items = shoppingList.value.filter(item => item.id === id)
  if (items.length > 0) {
    const item = items[0]
    item.bought = !item.bought
  }
}

const deleteItem = (id: number) => {
  shoppingList.value = shoppingList.value.filter(item => item.id !== id)
}

const addItem = () => {
  if (newItemTitle.value.trim()) {
    shoppingList.value.push({
      id: Date.now(),
      title: newItemTitle.value.trim(),
      bought: false
    })
    newItemTitle.value = ''
  }
}
</script>

<template>
  <main>
    <v-text-field
      v-model="newItemTitle"
      label="Add new item"
      append-icon="mdi-plus"
      clearable
      @click:append="addItem"
      @keyup.enter="addItem"
    />
    <v-list
      v-model:selected="settingsSelection"
      lines="three"
      select-strategy="leaf"
      class="wide-list"
    >
      <div v-for="(item, index) in shoppingList" :key="item.id">
        <v-list-item @click="doneBought(item.id)" :class="{ 'blue lighten-5': item.bought }">

          <div class="item-row">
          <v-list-item-action start>
            <v-checkbox v-model="item.bought" />
          </v-list-item-action>
          <v-list-item-title :class="{ 'text-decoration-line-through': item.bought }">
            {{ item.title }}
          </v-list-item-title>

          <v-list-item-action end class="ms-auto">
            <v-btn icon @click.stop="deleteItem(item.id)">
              <v-icon>mdi-delete</v-icon>
            </v-btn>
          </v-list-item-action>
          </div>
        </v-list-item>
        <v-divider v-if="index < shoppingList.length - 1" />
      </div>
    </v-list>
  </main>
</template>

<style scoped>
.wide-list {
  width: 400px;
}
.item-row {
  display: flex;
  align-items: center;
  gap: 10px;
}
</style>
