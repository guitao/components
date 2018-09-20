<template>
  <div class="hello">
    <Carousel :slides='slides' :inv='inv' :style='styleObject' :name='transitionName1' :target='target'></Carousel>
  </div>
</template>

<script>
import Carousel from "@/components/Carousel";

export default {
  name: 'HelloWorld',
  components: {Carousel},
  data () {
    return {
      slides: [
          {
            src: 'http://i3.mifile.cn/a4/xmad_14913974588712_tsRvc.jpg',
            href: ''
          },
          {
            src: 'http://i3.mifile.cn/a4/xmad_14915894814419_zNYsr.jpg',
            href: ''
          },
          {
            src: 'http://i3.mifile.cn/a4/xmad_14913784864515_mkpqH.jpg',
            href: ''
          },
          {
            src: 'http://i3.mifile.cn/a4/xmad_14908694250786_fObqa.jpg',
            href: ''
          },
          {
            src: 'http://i3.mifile.cn/a4/xmad_14913755624659_gRtNH.jpg',
            href: ''
          }
        ],
        inv: 3000,
        styleObject: {
          width: '1226px',
          height: '460px'
        },
        transitionName1: 'move',
        transitionName2: 'fade',
        target: '_blank'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
