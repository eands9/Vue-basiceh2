<template>
    <h2>{{ product.id }}</h2>
    <h2>{{ product.name }}</h2>
</template>

<script>
export default {
  props: ['product'],
}
</script>