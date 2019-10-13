<template>
  <div class="author">
    <img :src="author.fields.image.fields.file.url" class="author-image"/>
    <div class="author-info">
      <h2>{{author.fields.name}}</h2>
      <p>{{author.fields.summary}}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    author: Object,
  }
}
</script>

<style>
.author {
  background-color: white;
  width: 300px;
  padding: 15px;
}

.author-info > h2 {
  text-align: center;
}

.author-info > p {
  color: #000;
}
.author-image {
  width: 100%;
}

@media screen and (max-width: 896px) {
  .author {
    width: 100%;
    display: flex;
    align-items: center;
    position: static;
  }

  .author-image {
    width: 200px;
    height: 200px;
    object-fit: contain;
    object-position: center center;
  }

  .author-info {
    margin-left: 20px;
    flex: 1;
  }
}

@media screen and (max-width: 480px) {
  .author-image {
    width: 100px;
    height: 100px;
    object-fit: contain;
    object-position: center center;
  }
}
</style>
