<template>
  <div class="banner">
    <carousel :perPage=1 :autoplay=true :autoplayTimeout=3000 :loop=true :navigationEnabled=true paginationPosition="bottom-overlay" paginationActiveColor="#ffffff" paginationColor="#666666" class="carousel">
      <slide v-for="book in books" :key="book.sys.id" class="carousel-item">
        <img :src="book.fields.image.fields.file.url" class="carousel-book-image"/>
        <div class="book-content">
          <h2>{{book.fields.title}}</h2>
          <h5>{{book.fields.author}}</h5>
          <div class="book-detail">{{book.fields.detail}}</div>
          <a :href="book.fields.link">Amazonで開く</a>
        </div>
      </slide>
    </carousel>
  </div>
</template>

<script>
import { Carousel, Slide } from 'vue-carousel'

export default {
  components: {
    Carousel,
    Slide,
  },
  props: {
    books: Array,
  }
}
</script>

<style>
.carousel-item {
  background-color: rgba(0,0,0,0.5);
  width: 100%;
  min-height: 300px;
  max-height: 400px;
  padding: 40px 80px;
  display: flex;
}

.carousel-book-image {
  width: 200px;
  object-fit: contain;
}

.book-content {
  margin-left: 40px;
  color: white;
  overflow: auto;
}

.book-content > a {
  color: white;
  margin-top: 20px;
  display: block;
}

.book-detail {
  margin-top: 20px;
}

.VueCarousel-navigation-button {
  font-size: 30px;
  color: white !important;
}

.VueCarousel-navigation-next {
  transform: translate(0%, -50%) !important;
}

.VueCarousel-navigation-prev {
  transform: translate(0%, -50%) !important;
}

@media screen and (max-width: 896px) {
  .carousel-book-image {
    width: 150px;
  }
}

@media screen and (max-width: 480px) {
  .banner {
    display: none;
  }
}
</style>

