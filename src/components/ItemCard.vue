<template>
  <div class="item-card">
    <img :src="require(`@/assets/${item.image}`)" />
    <div class="item-text">
      <p>{{ item.text }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ItemCard',
  props: {
    item: {
      type: Object,
      required: true
    }
  }
}
</script>

<style scoped>
.item-card {
  position: relative;
  margin: 30px;
  overflow: hidden;
  border-radius: 10px;
  box-shadow: 5px 5px 2px #888888;
}

.item-card img {
  width: 100%;
  height: 400px;
  object-fit: cover;
  object-position: top center;
}

.item-text {
  position: absolute;
  bottom: 0;
  width: 100%;
  padding: 10px;
  background: rgba(255, 255, 255, 0.8);
}
</style>
