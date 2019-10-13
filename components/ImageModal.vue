<template>
  <div class="image-modal">
    <div class="modal-mask" @click="$emit('close')">
      <div class="modal-body" @click.stop>
        <button @click="$emit('close')" class="modal-close-button">×</button>
        <div class="modal-content-wrapper">
          <div class="modal-image-wrapper">
            <img :src="image" class="modal-image"/>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script scope>
export default {
  props: {
    image: String,
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

.image-modal .modal-body {
  width: 800px;
  height: auto;
  max-height: 100%;
  max-width: 100%;
  max-height: 100%;
  background-color: #fff;
  padding: 40px;
  position: relative;
}

.image-modal .modal-close-button {
  background-color: #fff;
  border: none;
  font-size: 30px;
  outline: 0;
  position: absolute;
  top: 5px;
  right: 5px;
}

.image-modal .modal-content-wrapper {
  max-width: 100%;
  display: flex;
}

.image-modal .modal-image-wrapper {
  max-width: 100%;
}

.image-modal .modal-image {
  max-width: 100%;
  max-height: 100%;
  object-fit: contain;
}

@media screen and (max-width: 960px) {
  .image-modal .modal-body {
    width: 100%;
  }
}

@media screen and (max-width: 560px) {
  .image-modal .modal-mask {
    padding: 10px;
  }

  .image-modal .modal-content-wrapper {
    flex-direction: column;
    justify-content: center;
  }

  .image-modal .modal-image-wrapper > a {
    display: block;
  }
}
</style>
