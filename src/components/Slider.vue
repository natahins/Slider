<template>
  <div class="slider">
      <div class="slider__container container">
          <p @click="goBack" class="container__arrow"><i class="left"></i></p>
          <div class="container__content">
           <transition :name="this.animateName">
           <div class="container__slide" :key="this.currentItem">
            <img :src="require('@/assets/'+ this.currentItem + '.jpg')">
           </div>
          </transition>
          </div>
          <p @click="goNext" class="container__arrow"><i class="right"></i></p>
      </div>
      <div class="slider__dots dots">
      <div v-for="(dot, index) in images" :key="index" class="dots__dot" @click="slideClickChange(index)" v-bind:class="{ active: currentItem === index + 1 ? true : false }">
      </div>
      </div>
  </div>
</template>

<script>
export default {
  name: 'Slider',
  data () {
    return {
      images: [1, 2, 3],
      currentItem: 1,
      animateName: 'slidenext',
      activeItem: null
    }
  },
  methods: {
    goNext () {
      this.animateName = 'slidenext'
      this.currentItem < this.images.length ? this.currentItem++ : this.currentItem = 1
    },
    goBack () {
      this.animateName = 'slideback'
      this.currentItem > 1 ? this.currentItem-- : this.currentItem = this.images.length
    },
    slideClickChange (value) {
      let oldItem = this.currentItem
      this.currentItem = value + 1
      oldItem > this.currentItem ? this.animateName = 'slideback' : this.animateName = 'slidenext'
    }
  }
}
</script>

<style lang="scss" scoped>
.slider {
    background-color: silver;
}
.container {
        display: flex;
        flex-flow: row nowrap;
        justify-content: center;
        align-items: center;
        &__content {
            overflow: hidden;
            position: relative;
            width: 400px;
            height: 400px;
        }
         &__slide{
                position: absolute;
            }
        &__arrow {
            padding: 25px;
        }
    }
.dots {
    display: flex;
    flex-flow: row nowrap;
    justify-content: center;
      &__dot {
        width: 10px;
        height: 10px;
        background-color: black;
        border-radius: 50%;
        margin: 10px 10px;
        &:hover {
            background-color: aliceblue;
        }
    }
}
.active {
          background-color: aliceblue;
        }
i {
  border: solid black;
  border-width: 0 10px 10px 0;
  display: inline-block;
  padding: 10px;
}
.right {
  transform: rotate(-45deg);
  -webkit-transform: rotate(-45deg);
  &:hover{
      border: solid aliceblue;
      border-width: 0 10px 10px 0;
      display: inline-block;
      padding: 10px;
  }
}
.left {
  transform: rotate(135deg);
  -webkit-transform: rotate(135deg);
   &:hover{
      border: solid aliceblue;
      border-width: 0 10px 10px 0;
      display: inline-block;
      padding: 10px;
  }
}

.slidenext-leave-active,
.slidenext-enter-active {
  transition: 1s;
}
.slidenext-enter {
  transform: translate(100%, 0);
}
.slidenext-leave-to {
  transform: translate(-100%, 0);
}

.slideback-leave-active,
.slideback-enter-active {
  transition: 1s;
}
.slideback-enter {
  transform: translateX(-100%);
}
.slideback-leave-to {
    transform: translateX(100%);
}
</style>
