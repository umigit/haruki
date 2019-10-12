<template>
  <section class="container">
    <TheHeader/>
    <div class="main">
      <!-- <script async defer crossorigin="anonymous" src="https://connect.facebook.net/ja_JP/sdk.js#xfbml=1&version=v4.0&appId=772558586494040&autoLogAppEvents=1"></script> -->
      <div class="main-content">
        <TheBanner :books="banner"/>
        <div class="blog-content">

          <div class="articles">
            <!-- <div class="fb-page" data-href="https://www.facebook.com/haruki.amanuma" data-tabs="timeline" data-width="500" data-height="200" data-small-header="false" data-adapt-container-width="true" data-hide-cover="false" data-show-facepile="true"></div> -->
          </div>
          <div class="sidebar">
            <TheAuthor :author="author"/>
            <div class="fb-page" data-href="https://www.facebook.com/facebook" data-tabs="timeline" data-width="300" data-height="500" data-small-header="true" data-adapt-container-width="true" data-hide-cover="false" data-show-facepile="true"><blockquote cite="https://www.facebook.com/facebook" class="fb-xfbml-parse-ignore"><a href="https://www.facebook.com/facebook">Facebook</a></blockquote></div>

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

const script = document.createElement("script");
script.src = "https://connect.facebook.net/ja_JP/sdk.js#xfbml=1&version=v4.0&appId=772558586494040&autoLogAppEvents=1";
script.async = true;
script .defer = true;
script.crossorigin = "anonymous";
document.body.insertBefore(script, document.body.firstChild);

export default {
  components: {
    TheHeader,
    TheBanner,
    TheAuthor,
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
  justify-content: center;
  margin-top: 20px;
}

.articles {
  width: 100%;
  /* max-width: 500px; */
  margin-right: 40px;
  padding: 0;
}
.article {
  background-color: white;
  margin-bottom: 30px;
  padding: 20px;
}

.article-body > p {
  color: #000;
}

.article-image {
  width: 100%;
  margin-top: 20px;
}

.article-body {
  margin-top: 20px;
}

.sidebar {
  position: relative;
}

.author {
  margin-bottom: 20px;
}

@media screen and (max-width: 1024px) {
  .main-content {
    width: 840px;
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
    margin: 0 auto;
    margin-top: 20px;
  }
}

@media screen and (max-width: 480px) {
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

