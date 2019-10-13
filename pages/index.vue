<template>
  <section class="container">
    <ImageModal :image="clickedImage" v-if="showModal" @close="closeModal()"/>
    <TheHeader/>
    <div class="main">
      <div class="main-content">
        <TheBanner :books="banner"/>
        <div class="blog-content">
          <div class="articles">
            <div v-for="article in articles" :key="article.sys.id" class="article">
              <div class="article-header">
                <h2 class="article-title">{{article.fields.title}}</h2>
                <h5 class="article-date">{{article.sys.createdAt}}</h5>
              </div>
              <hr/>
              <div v-html="article.fields.body" class="article-body"></div>
              <img :src="article.fields.images[0].fields.file.url" class="article-image" @click="openModal(article.fields.images[0].fields.file.url)"/>
            </div>
          </div>
          <div class="sidebar">
            <TheAuthor :author="author"/>
            <!-- <div class="fb-page" data-href="https://www.facebook.com/facebook" data-tabs="timeline" data-width="300" data-height="500" data-small-header="true" data-adapt-container-width="true" data-hide-cover="false" data-show-facepile="false"><blockquote cite="https://www.facebook.com/facebook" class="fb-xfbml-parse-ignore"><a href="https://www.facebook.com/facebook">Facebook</a></blockquote></div> -->
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
import ImageModal from '~/components/ImageModal'
import { documentToHtmlString } from '@contentful/rich-text-html-renderer'
import client from '~/plugins/contentful'

// const script = document.createElement("script");
// script.src = "https://connect.facebook.net/ja_JP/sdk.js#xfbml=1&version=v4.0&appId=772558586494040&autoLogAppEvents=1";
// script.async = false;
// script.defer = true;
// script.crossorigin = "anonymous";
// document.body.insertBefore(script, document.body.firstChild);

const formatDate = function (date) {
  const date_array = date.toString().split(/[-T.]/)
  return date_array[0] + '年' + Number(date_array[1]).toString() + '月' + Number(date_array[2]).toString() + '日'
}

export default {
  components: {
    TheHeader,
    TheBanner,
    TheAuthor,
    ImageModal,
  },
  async asyncData() {
    return await client.getEntries({ order: '-sys.createdAt' })
      .then(entries => {
        let author
        let banner
        let articles = []
        let books = []

        entries.items.forEach(item => {
          const id = item.sys.contentType.sys.id

          if (id === 'article') {
            item.fields.body = documentToHtmlString(item.fields.body)
            item.sys.createdAt = formatDate(item.sys.createdAt)
            articles.push(item)
          }
          else if (id === 'book') {
            books.push(item)
          }
          else if (id === 'author') {
            author = item
          }
          else if (id === 'banner') {
            banner = item.fields.book
          }
        })

        return {
          author: author,
          banner: banner,
          articles: articles,
          books: books,
        }
      })
  },
  data() {
    return {
      showModal: false,
      clickedImage: '',
    }
  },
  methods: {
    openModal(item) {
      this.clickedImage = item
      this.showModal = true
    },
    closeModal() {
      this.showModal = false
    },
  },
  mounted () {
    // FB.XFBML.parse()
  }
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
  max-width: 960px;
  box-sizing: border-box;
  height: calc(100vh - 80px);
  margin: 0 auto;
  padding: 20px 20px;
  overflow: scroll;
}

.main-content {
  width: 100%;

}

.blog-content {
  display: flex;
  justify-content: center;
  margin-top: 20px;
}

.articles {
  width: 100%;
  margin-right: 40px;
  padding: 0;
}
.article {
  background-color: white;
  margin-bottom: 30px;
  padding: 20px;
}

.article-header {
  height: 40px;
  padding: 0 10px;
  display: flex;
  justify-content: space-between;
}

.article-date {
  color: black;
  margin-top: auto;
  padding-bottom: 10px;
}

.article-body > p {
  color: #000;
}

.article-image {
  width: 100%;
  max-height: 300px;
  margin-top: 20px;
  object-fit: cover;
}

.article-body {
  margin-top: 20px;
}

.sidebar {
  position: relative;
}

.author {
  margin-bottom: 20px;
  position: sticky;
  top: 0;
}

@media screen and (max-width: 960px) {
  .main-content {
    width: 100%;
  }

  .blog-content {
    flex-direction: column-reverse;
  }

  .articles {
    margin: 0 auto;
    margin-top: 20px;
  }

  .author {
    margin-bottom: 0;
  }
}

@media screen and (max-width: 560px) {
  .container {
    padding-top: 60px;
  }

  .main {
    padding: 10px;
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

  h2 {
    font-size: 16px;
  }
  h4 {
    font-size: 12px;
  }
  p {
    font-size: 11px;
  }
}
</style>

