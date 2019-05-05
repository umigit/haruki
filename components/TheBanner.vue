<template>
  <div class="banner">
    <carousel :perPage=1 :autoplay=true :autoplayTimeout=3000 :loop=true :navigationEnabled=true paginationPosition="bottom-overlay" paginationActiveColor="#ffffff" paginationColor="#666666" class="carousel">
      <slide class="carousel-item first">
        <img :src="books[0].fields.image.fields.file.url" class="book-image"/>
        <div class="book-content">
          <h2>{{books[0].fields.title}}</h2>
          <h5>{{books[0].fields.author}}</h5>
          <div class="book-detail">{{books[0].fields.detail}}</div>
          <a :href="books[0].fields.link">Amazonで開く</a>
        </div>
      </slide>
      <slide class="carousel-item second">
        <img :src="books[1].fields.image.fields.file.url" class="book-image"/>
        <div class="book-content">
          <h2>{{books[1].fields.title}}</h2>
          <h5>{{books[1].fields.author}}</h5>
          <div class="book-detail">{{books[1].fields.detail}}</div>
          <a :href="books[1].fields.link">Amazonで開く</a>
        </div>
      </slide>
      <slide class="carousel-item second">
        <img :src="books[2].fields.image.fields.file.url" class="book-image"/>
        <div class="book-content">
          <h2>{{books[2].fields.title}}</h2>
          <h5>{{books[2].fields.author}}</h5>
          <div class="book-detail">{{books[2].fields.detail}}</div>
          <a :href="books[2].fields.link">Amazonで開く</a>
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
  background-color: rgba(0,0,0,0.8);
  width: 100%;
  min-height: 300px;
  max-height: 400px;
  padding: 40px 80px;
  display: flex;
}

.book-image {
  height: 100%;
  max-height: 400px;
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
  .banner {

  }
}

@media screen and (max-width: 480px) {
  .banner {
    display: none;
  }
}
</style>

