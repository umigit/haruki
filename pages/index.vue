<template>
  <section class="container">
    <div class="main">
      <div class="articles">
        <div v-for="article in articles" :key="article.sys.id" class="article">
          <h2>{{article.fields.title}}</h2>
          <img :src="article.fields.images[0].fields.file.url" class="article-image"/>
          <div v-html="article.fields.body" class="article-body"></div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import { documentToHtmlString } from '@contentful/rich-text-html-renderer'
import client from '~/plugins/contentful'

export default {
  async asyncData() {
    return await client.getEntries()
      .then(entries => {
        let author
        let articles = []
        let books = []

        entries.items.forEach(item => {
          const id = item.sys.contentType.sys.id
          if (id === 'article') {
            item.fields.body = documentToHtmlString(item.fields.body)
            articles.push(item)
          }
          else if (id === 'book') {
            books.push(item)
          }
          else if (id === 'author') {
            author = item
          }
        })
        console.log(entries.items[0].sys.contentType.sys.id)
        return {
          author: author,
          articles: articles,
          books: books,
        }
      })
  },
}
</script>

<style>
.container {
  min-height: 100vh;
}

.article {
  width: 600px;
  border: 1px solid gray;
  padding: 20px;
}

.article-image {
  width: 100%;
}
</style>

