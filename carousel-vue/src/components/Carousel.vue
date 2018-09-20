<template>
    <div class="slide-show" @mousemove="clearInv" @mouseout="runInv">
        <transition-group tag="ul" class="slide-ul" :name="name">
            <li v-for="(item, index) in slides" :key="index" v-show="index === nowIndex">
                <a :href="item.href" :target="target">
                    <img :src="item.src" alt="">
                </a>
            </li>
        </transition-group>
        <ul class="slide-pages">
            <li v-for="(item, index) in slides" :key="index"
                @click="goto(index)"
                class="slide-page-point"
            >
                <a :class="{'active': index === nowIndex}">{{index + 1}}</a>
            </li>
        </ul>
        <div class="control-wrapper">
            <a class="prev" @click="goto(preIndex)"></a>
            <a class="next" @click="goto(nextIndex)"></a>
        </div>
    </div>
</template>

<script>
export default {
  props: {
    slides: {
      type: Array,
      default: []
    },
    inv: {
      type: Number,
      default: 1000
    },
    name: {
      type: String,
      default: "move"
    },
    target: {
      type: String,
      default: "_blank"
    }
  },
  data() {
    return {
      nowIndex: 0
    };
  },
  computed: {
    preIndex() {
      if (this.nowIndex === 0) {
        return this.slides.length - 1;
      } else {
        this.nowIndex - 1;
      }
    },
    nextIndex() {
      if (this.nowIndex === this.slides.length - 1) {
        return 0;
      } else {
        return this.nowIndex + 1;
      }
    }
  },
  methods: {
    gotoInv(index) {
      this.nowIndex = index;
    },
    runInv() {
      this.invId = setInterval(() => {
        this.gotoInv(this.nextIndex);
      }, this.inv);
    },
    clearInv() {
      clearInterval(this.invId);
    }
  },
  mounted() {
    this.runInv();
  }
};
</script>

<style lang="scss" scoped>
.slide-show {
  position: relative;
  overflow: hidden;
}

.slide-ul {
  width: 100%;
  height: 100%;
  li {
    position: absolute;
    width: 100%;
    height: 100%;

    img {
      width: 100%;
      height: 100%;
      transition: all 1s;
    }
  }
}

.slide-page {
  position: absolute;
  bottom: 20px;
  right: 30px;
  li {
    display: inline-block;
    height: 18px;
    a {
      display: block;
      height: 6px;
      width: 6px;
      margin: 0 5px;
      border: 2px solid rgba(255, 255, 255, 0.3);
      border-radius: 10px;
      text-align: left;
      text-indent: -9999px;
      overflow: hidden;
      _zoom: 1;
      background: #f5f5f5;
      background: rgba(0, 0, 0, 0.4);
      -webkit-transition: all 0.2s;
      transition: all 0.2s;
      &.active {
        background: #fff;
        background: rgba(255, 255, 255, 0.4);
        border-color: #757575;
        border-color: rgba(0, 0, 0, 0.4);
      }
    }
  }
}

.move-enter-active {
  transition: all 0.5s ease;
  transform: translateX(0);
}

.move-leave-active {
  transition: all 0.5s ease;
  transform: translateX(-100%);
}

.move-enter {
  transform: translateX(100%);
}

.move-leave {
  transform: translateX(0);
}

</style>

