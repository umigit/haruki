<template>
  <section class="container">
    <TheHeader/>
    <div class="main">
      <div class="main-content">
        <TheBanner :books="books"/>
        <div class="blog-content">
          <div class="articles">
            <div v-for="article in articles" :key="article.sys.id" class="article">
              <h2>{{article.fields.title}}</h2>
              <img :src="article.fields.images[0].fields.file.url" class="article-image"/>
              <div v-html="article.fields.body" class="article-body"></div>
            </div>
          </div>
          <div class="sidebar">
            <TheAuthor :author="author"/>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import TheHeader from '~/components/TheHeader'
import TheBanner from '~/components/TheBanner'
import TheAuthor from '~/components/TheAuthor'
import { documentToHtmlString } from '@contentful/rich-text-html-renderer'
import client from '~/plugins/contentful'

export default {
  components: {
    TheHeader,
    TheBanner,
    TheAuthor,
  },
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
  height: 100vh;
  background-image: url('~assets/images/airship.jpg');
  background-size: cover;
  background-position: center center;
  background-attachment: fixed;
  padding-top: 80px;
}

.main {
  box-sizing: border-box;
  height: calc(100vh - 80px);

  padding: 20px 20px;
  overflow: scroll;
}

.main-content {
  width: 1020px;
  margin: 0 auto;
}

.blog-content {
  display: flex;
  margin-top: 20px;
}

.articles {
  width: 100%;
  margin-right: 40px;
  padding: 0;
}
.article {
  background-color: white;
  padding: 20px;
}

.article-image {
  width: 100%;
}

@media screen and (max-width: 1024px) {
  .main-content {
    width: 800px;
  }
}

@media screen and (max-width: 896px) {
  .main-content {
    width: 100%;
  }

  .blog-content {
    flex-direction: column-reverse;
  }

  .articles {
    margin-right: 0;
    margin-top: 20px;
  }
}

@media screen and (max-width: 480px) {
  .container {
    padding-top: 60px;
  }

  .main-content {
    width: 100%;
  }

  .blog-content {
    margin-top: 0;
  }

  .articles {
    margin-right: 0;
    margin-top: 20px;
  }
}
</style>

