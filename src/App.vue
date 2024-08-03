<script setup>
import { ref } from 'vue'
const products = ref([
  {
    id: 1,
    name: '珍珠奶茶',
    desc: '香濃奶茶搭配QQ珍珠',
    price: 50,
    stock: 20
  },
  {
    id: 2,
    name: '冬瓜檸檬',
    desc: '清新冬瓜配上新鮮檸檬',
    price: 45,
    stock: 18
  },
  {
    id: 3,
    name: '翡翠檸檬',
    desc: '綠茶與檸檬的完美結合',
    price: 55,
    stock: 34
  },
  {
    id: 4,
    name: '四季春茶',
    desc: '香醇四季春茶，回甘無比',
    price: 45,
    stock: 10
  },
  {
    id: 5,
    name: '阿薩姆奶茶',
    desc: '阿薩姆紅茶搭配香醇鮮奶',
    price: 50,
    stock: 25
  },
  {
    id: 6,
    name: '檸檬冰茶',
    desc: '檸檬與冰茶的清新組合',
    price: 45,
    stock: 37
  },
  {
    id: 7,
    name: '芒果綠茶',
    desc: '芒果與綠茶的獨特風味',
    price: 55,
    stock: 4
  },
  {
    id: 8,
    name: '抹茶拿鐵',
    desc: '抹茶與鮮奶的絕配',
    price: 60,
    stock: 20
  }
])
const tempEditItem = ref({})

const updateStock = (product, event) => {
  if (event === 'add') {
    product.stock++
  }
  if (event === 'minus' && product.stock > 0) {
    product.stock--
  }
}
const editName = (item) => {
  tempEditItem.value = { ...item }
}
const confirmEdit = () => {
  const index = products.value.findIndex((item) => item.id === tempEditItem.value.id)
  products.value[index] = tempEditItem.value
  tempEditItem.value = {}
}
</script>

<template>
  <div>
    <table class="table">
      <thead>
        <tr>
          <th scope="col" width="30%">品項</th>
          <th scope="col" width="30%">描述</th>
          <th scope="col" width="20%">價格</th>
          <th scope="col" width="20%">庫存</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="product in products" :key="product.id">
          <td class="productName">
            <div>
              <span v-if="tempEditItem.id === product.id">
                <input type="text" v-model="tempEditItem.name" />
                <button type="button" @click="confirmEdit">確認</button>
                <button v-if="tempEditItem.id" type="button" @click="tempEditItem = {}">
                  取消
                </button>
              </span>
              <span v-else>{{ product.name }}</span>
              <button
                class="editButton"
                v-if="!tempEditItem.id"
                type="button"
                @click="editName(product)"
              >
                編輯
              </button>
            </div>
          </td>
          <td>
            <small>{{ product.desc }}</small>
          </td>
          <td>{{ product.price }}</td>
          <td>
            <button type="button" @click="updateStock(product, 'minus')">-</button>
            <span class="text">{{ product.stock }}</span>
            <button type="button" @click="updateStock(product, 'add')">+</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style scoped>
.table {
  width: 100%;
  text-align: center;
}
button {
  cursor: pointer;
}
.text {
  display: inline-block;
  width: 30px;
}
.productName {
  display: flex;
  justify-content: center;
}
.editButton {
  margin-left: 5px;
}
</style>
