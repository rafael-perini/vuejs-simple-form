<template>
  <div id="app">
    <h1>{{ title }}</h1>
    <form @submit.prevent>
      <p v-if="items.length === 0">There's no items.</p>
      <ul v-else>
        <li v-for="(item, index) in items" :key="index">
          <ProductForm v-model="items[index]">
            <input type="button" value="Remove" @click="removeItem(index)" />
          </ProductForm>
        </li>
        <li>
          <b>Total Amount: {{ totalAmount }}</b>
        </li>
      </ul>
      <ProductForm v-model="product">
        <input type="button" value="Add" @click="addItem(product)" />
      </ProductForm>
    </form>
  </div>
</template>

<script>
import ProductForm from "./components/ProductForm.vue";

export default {
  name: "App",
  components: {
    ProductForm,
  },
  data() {
    return { title: "Order", product: {}, items: [] };
  },
  filters: {
    uppercase(value) {
      return value.toString().toUpperCase();
    },
  },
  computed: {
    totalAmount() {
      return this.items.reduce((total, item) => (total += item.quantity), 0);
    },
  },
  watch: {
    items(newItems) {
      console.log("newItems", newItems);
    },
  },
  methods: {
    addItem(item) {
      this.items.push({ ...item });
    },
    removeItem(index) {
      this.items.splice(index, 1);
    },
  },
};
</script>