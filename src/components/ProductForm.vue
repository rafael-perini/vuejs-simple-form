<template>
  <div>
    <label for="product">Product:</label>
    <input
      type="text"
      id="product"
      :value="value.name"
      @input="$emit('input', { ...value, name: $event.target.value })"
    />
    <label for="quantity">Quantity:</label>
    <input
      type="number"
      id="quantity"
      :value="value.quantity"
      @input="
        $emit('input', { ...value, quantity: Number($event.target.value) })
      "
    />
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: "ProductForm",

  props: { value: Object },
};
</script>