<template>
  <div class="container">
    <TheHeader/>
    <div class="book-list">
      <div v-for="book in books" :key="book.sys.id" class="book">
        <img :src="book.fields.image.fields.file.url" class="book-image"/>
      </div>
    </div>
  </div>
</template>

<script>
import TheHeader from '~/components/TheHeader'
import client from '~/plugins/contentful'

export default {
  components: {
    TheHeader,
  },
  async asyncData() {
    return await client.getEntries({'content_type': 'book' })
      .then(entries => {
        return {
          books: entries.items
        }
      })
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
}

.book {
  width: 200px;
  margin: 30px;
}

.book-image {
  width: 100%;
}
</style>

