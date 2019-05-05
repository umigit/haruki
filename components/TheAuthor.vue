<template>
  <div class="author">
    <img :src="author.fields.image.fields.file.url" class="author-image"/>
    <h2>{{author.fields.name}}</h2>
    <p>{{author.fields.summary}}</p>
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

.author > h2 {
  text-align: center;
}
.author-image {
  width: 100%;
}
</style>
