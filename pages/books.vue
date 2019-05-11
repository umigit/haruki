<template>
  <div class="container">
    <BookModal :item="clickedItem" v-if="showModal" @close="closeModal()"/>
    <TheHeader/>
    <div class="main">
      <div class="book-list">
        <div v-for="book in books" :key="book.sys.id" class="book" @click="openModal(book)">
          <img :src="book.fields.image.fields.file.url" class="book-image"/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import TheHeader from '~/components/TheHeader'
import BookModal from '~/components/BookModal'
import client from '~/plugins/contentful'

export default {
  components: {
    TheHeader,
    BookModal,
  },
  async asyncData() {
    return await client.getEntries({'content_type': 'book' })
      .then(entries => {
        return {
          books: entries.items
        }
      })
  },
  data() {
    return {
      showModal: false,
      clickedItem: '',
    }
  },
  methods: {
    openModal(item) {
      this.clickedItem = item;
      this.showModal = true;
    },
    closeModal() {
      this.showModal = false;
    },
  },
}
</script>

<style>
.book-list {
  width: 1020px;
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  margin: 0 auto;
  padding: 0;
}

.book {
  width: 200px;
  margin: 30px;
}

.book-image {
  width: 100%;
}

@media screen and (max-width: 1024px) {
 .book-list {
   width: 800px;
 }
}

@media screen and (max-width: 896px) {
  .book-list {
    width: 100%;
  }

  .book {
    width: 150px;
  }
}

@media screen and (max-width: 480px) {
  .book {
    width: 26%;
    max-width: 100px;
    min-width: 80px;
    margin: 10px;
  }
}
</style>

