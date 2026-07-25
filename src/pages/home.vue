<script setup>
import { ref } from "vue"

// 選択中のサブスク
const selectedItem = ref(null)

// ダイアログ表示状態
const dialog = ref(false)

// ダミーデータ
const items = ref([
  {
    id: 1,
    name: "Netflix",
    category: "動画配信",
    price: 1980,
    payment: "15日"
  },
  {
    id: 2,
    name: "Spotify",
    category: "音楽配信",
    price: 980,
    payment: "1日"
  },
  {
    id: 3,
    name: "ChatGPT Plus",
    category: "AIサービス",
    price: 3000,
    payment: "22日"
  }
])

// カードクリック
function openDetail(item) {
  selectedItem.value = item
  dialog.value = true
}
</script>


<template>
  <v-container>
    <v-row>
      <!-- カード一覧 -->
      <v-col v-for="item in items" :key="item.id">
        <v-card class="pa-4" elevation="4" @click="openDetail(item)">
          <v-card-title>
            {{ item.name }}
          </v-card-title>
          <v-card-subtitle>
            {{ item.category }}
          </v-card-subtitle>
          <v-card-text>
            ¥{{ item.price }} / 月
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>

    <!-- 詳細ダイアログ -->
    <v-dialog v-model="dialog" max-width="500">
      <v-card v-if="selectedItem">
        <v-card-title>
          {{ selectedItem.name }}
        </v-card-title>
        <v-card-text>
          <p>
            カテゴリ：
            {{ selectedItem.category }}
          </p>
          <p>
            月額：
            ¥{{ selectedItem.price }}
          </p>
          <p>
            支払日：
            {{ selectedItem.payment }}
          </p>
        </v-card-text>
        <v-card-actions>
          <v-btn>
            編集
          </v-btn>
          <v-btn color="error">
            削除
          </v-btn>
          <v-spacer />
          <v-btn @click="dialog = false">
            閉じる
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-container>
</template>