<template>
  <div class="container">
    <BookModal :item="clickedItem" v-if="showModal" @close="closeModal()"/>
    <TheHeader/>
    <div class="main">
      <div class="book-list">
        <div v-for="book in books" :key="book.sys.id" class="book" >
          <img :src="book.fields.image.fields.file.url" @click="openModal(book)" class="book-image"/>
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
  width: 960px;
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  margin: 0 auto;
  padding: 0;
}

.book {
  width: 26%;
  margin: 30px;
}

.book::after{
  content:"";
  display: block;
  width: 26%;
}

.book-image {
  width: 100%;
  padding: 0px;
}

@media screen and (max-width: 960px) {
  .book-list {
    width: 100%;
    max-width: 960px;
  }

  .book {
    margin: 30px 15px;
  }
}

@media screen and (max-width: 560px) {
  .book {
    margin: 15px 10px;
  }
}
</style>

