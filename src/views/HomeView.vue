<template>
  <div id="galleryId" style="display: grid; grid-template-columns: repeat(2, minmax(0, 1fr)); gap: 2rem; width: 100%">
    <a
      style="width: 100%; display: block;"
      v-for="(image, key) in images"
      :key="key"
      :href="image.fullurl"
      :data-pswp-width="imageWidth(image.fullurl)"
      :data-pswp-height="imageHeight(image.fullurl)"
      target="_blank"
      rel="noreferrer"
    >
      <img :src="image.fullurl" alt="" style="width: 100%;" />
    </a>
  </div>
</template>

<script>
import PhotoSwipeLightbox from 'photoswipe/lightbox';
import 'photoswipe/style.css';

export default {
  data() {
    return {
      images: [
        {
          fullurl: 'https://cdn.photoswipe.com/photoswipe-demo-images/photos/1/img-2500.jpg',
        },
        {
          fullurl: 'https://cdn.photoswipe.com/photoswipe-demo-images/photos/2/img-2500.jpg',
        },
      ]
    }
  },
  methods: {
    imageWidth(url) {
      let image = new Image()
      image.src = url

      return image.width
    },
    imageHeight(url) {
      let image = new Image()
      image.src = url

      return image.height
    }
  },
  mounted() {
    if(!this.lightbox) {
      this.lightbox = new PhotoSwipeLightbox({
        gallery: '#galleryId',
        children: 'a',
        pswpModule: () => import('photoswipe'),
      })
      this.lightbox.init()
    }
  },
  unmounted() {
    if(this.lightbox) {
      this.lightbox.destroy()
      this.lightbox = null
    }
  }
}
</script>