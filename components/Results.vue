<template>
  <b-row>
    <b-col v-for="item in items.available" sm="12" class="w-100" :key="item.id">
      <div class="bg-white p-5 shadow rounded my-5">
        <div class="blockquote-custom-icon bg-info shadow-sm d-flex">
          <b-icon-minecart variant="light"></b-icon-minecart>
        </div>
        <h3>&euro; {{ item.price }}</h3>
        <p class="mb-0 mt-2">{{ item.merchant.name }}</p>
        <footer v-if="item.review.score" class="blockquote-footer pt-4 mt-4 border-top">Rating
          <cite>{{ parseFloat(item.review.score).toFixed(1) }}</cite>
        </footer>
      </div>
    </b-col>
  </b-row>
</template>
<script>
import { BIcon, BIconMinecart } from 'bootstrap-vue'

export default {
  components: {
    BIcon,
    BIconMinecart
  },
  props: ['items']
}
</script>
<style>
  .blockquote-custom-icon {
    width: 50px;
    height: 50px;
    border-radius: 50%;
    align-items: center;
    justify-content: center;
    position: absolute;
    top: 20px;
    right: 50px;
  }
</style>

