<template>
  <div class="book-modal">
    <div class="modal-mask" @click="$emit('close')">
      <div class="modal-body" @click.stop>
        <button @click="$emit('close')" class="modal-close-button">×</button>
        <div class="modal-content-wrapper">
          <div class="modal-book-info-small">
              <h2 class="modal-book-title-small">{{item.fields.title}}</h2>
              <h5 class="modal-book-author-small">{{item.fields.author}}</h5>
          </div>
          <div class="modal-image-wrapper">
            <img :src="item.fields.image.fields.file.url" class="modal-book-image"/>
            <a :href="item.fields.link">Amazonで開く</a>
          </div>
          <div class="modal-book-content">
            <div class="modal-book-info-big">
              <h2 class="modal-book-title-big">{{item.fields.title}}</h2>
              <h5 class="modal-book-author-big">{{item.fields.author}}</h5>
            </div>
            <div class="modal-book-detail">{{item.fields.detail}}</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    item: Object,
  }
}
</script>

<style>
.modal-mask {
  width: 100%;
  height: 100%;
  position: fixed;
  top: 0;
  left: 0;
  z-index: 2;
  background-color: rgba(0,0,0,0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px;
}

.book-modal .modal-body {
  background-color: #fff;
  width: 800px;
  padding: 40px;
  position: relative;
}

.book-modal .modal-close-button {
  background-color: #fff;
  border: none;
  font-size: 30px;
  outline: 0;
  position: absolute;
  top: 5px;
  right: 5px;
}

.book-modal .modal-content-wrapper {
  height: 100%;
  display: flex;
}

.book-modal .modal-image-wrapper {
  text-align: center;
}

.book-modal .modal-book-image {
  max-height: 300px;
  margin: 20px;
}

.modal-book-content {
  margin-left: 20px;
}

.modal-book-author-big {
  color: #000;
  margin-top: 10px;
  padding-bottom: 10px;
  border-bottom: 1px solid gray;
}

.modal-book-title-big {
  color: #000;
}

.modal-book-info-small {
    display: none;
}

.modal-book-title-small {
    color: #000;
    font-size: 16px;
}

.modal-book-author-small {
  color: #000;
  margin-top: 4px;
  font-size: 12px;
}

.modal-book-detail {
  margin-top: 30px;
}

@media screen and (max-width: 1024px) {

}

@media screen and (max-width: 896px) {
  .book-modal .modal-body {
    width: 100%;
  }

  .book-modal .modal-book-image {
    max-height: 180px;
    margin: 10px;
  }

  .book-modal .modal-book-info-big {
    display: block;
  }

  .book-modal .modal-book-info-small {
    display: none;
  }


}

@media screen and (max-width: 480px) {
  .book-modal .modal-mask {
    padding: 10px;
  }

  .book-modal .modal-content-wrapper {
    flex-direction: column;
    justify-content: center;
  }
  .book-modal .modal-book-info-big {
    display: none;
  }

  .modal-book-info-small {
    display: block;
  }

  .modal-book-content {
    margin-left: 0;
    font-size: 10px;
  }

  .modal-book-detail {
    margin-top: 12px;
  }

  .book-modal .modal-image-wrapper > a {
    display: block;
  }
}
</style>
