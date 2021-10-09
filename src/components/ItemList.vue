<template>
  <div class="item-list">
    <div class="row">
      <div
        v-for="(item, index) in list"      
        :key="`list-item-${index}`"
        class="col-4"
      >
        <item-card :item="item" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ItemList',
  components: {
    ItemCard: () => import('./ItemCard')
  },
  props: {},
  data() {
    return {
      list: [
        {
          image: 'one.jpeg',
          title: 'Neque porro',
          text: 'Neque porro quisquam est qui dolorem ipsum'
        },
        {
          image: 'two.jpeg',
          title: 'Sed enim ut sem viverra',
          text: 'Non odio euismod lacinia at quis. Risus quis varius quam quisque id.'
        },
        {
          image: 'three.jpeg',
          title: 'Id venenatis a condimentum',
          text: 'Id venenatis a condimentum vitae sapien. Id volutpat lacus laoreet non curabitur. Scelerisque eu ultrices vitae auctor eu augue ut lectus arcu.'
        },
        {
          image: 'four.jpg',
          title: 'Sit amet justo donec',
          text: 'Sit amet justo donec enim diam vulputate. Libero id faucibus nisl tincidunt. Tempor commodo ullamcorper a lacus vestibulum. Aliquet bibendum enim facilisis gravida.'
        },
        {
          image: 'five.jpeg',
          title: 'Id venenatis a condimentum',
          text: 'Id venenatis a condimentum vitae sapien. Id volutpat lacus laoreet non curabitur.'
        },
        {
          image: 'six.jpeg',
          title: 'Sit amet justo donec',
          text: 'Sit amet justo donec enim diam vulputate.'
        }
      ],
    }
  }
}
</script>

<style scoped>
.item-list {
  margin-top: 30px;
}
</style>
