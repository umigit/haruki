<template>
  <div class="container">
    <TheHeader/>
    <div class="main">
      <div class="profile-container">
        <div class="profile">
          <div class="profile-body">
            <div class="profile-image-box">
              <img :src="author.fields.images[0].fields.file.url" class="profile-image"/>
            </div>
            <div class="profile-content">
              <h2>{{author.fields.name}}</h2>
              <h4>{{author.fields.summary}}</h4>
              <p>{{author.fields.detail}}</p>
            </div>
          </div>
        </div>
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
    return await client.getEntries({'content_type': 'author' })
      .then(entries => {
        return {
          author: entries.items[0]
        }
      })
  },
}
</script>

<style>
.profile-container {
  height: 100%;
}

.profile {
  width: 800px;
  background-color: rgba(0,0,0,0.5);
  margin: 0 auto;
}

.profile-body {
  display: flex;
  padding: 40px;
}

.profile-image-box {
  width: 300px;
  margin: 0 auto;
}

.profile-image {
  width: 100%;
  object-fit: contain;
  margin: 20px 0;
}

.profile-content {
  margin-left: 40px;
  flex: 1;
}

.profile-content > h4 {
  margin-top: 10px;
}

.profile-content > p {
  margin-top: 40px;
}

.profile-content > h2, h4 , h5, p {
  color: #fff;
}

@media screen and (max-width: 960px) {
  .profile {
    width: 100%;
  }

  .profile-image-box {
    max-width: 280px;
    width: 30%;
    min-width: 150px;
  }

  .profile-body {
    flex-direction: column;
  }

  .profile-content {
    margin-left: 0;
  }

  .profile-content > h2 {
    text-align: center;
  }
}

@media screen and (max-width: 560px) {
  .profile-body {
    padding: 20px 40px;
  }

  .profile-content > p {
    margin-top: 10px;
  }
}
</style>

