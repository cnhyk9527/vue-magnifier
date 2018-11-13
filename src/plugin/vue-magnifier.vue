<template>
  <div class="magnifier">
    <div
      class="magnifier-box" @mouseenter="showImgs" @mouseleave="hideImgs"
      @mousemove="moveImgs">
      <div class="magnifier-box-move" v-show="showMove" :style="{left:moveLeft+'px',top:moveTop+'px'}"></div>
      <img :src="smallImg" alt="" class="magnifier-box-img">
    </div>
    <div class="magnifier-big" v-show="showBig">
      <img :src="bigImg" alt="" class="magnifier-big-img" :style="{left:bigLeft+'px',top:bigTop+'px'}">
    </div>
  </div>
</template>
<script>
  export default {
    data () {
      return {
        showMove: false,
        showBig: false,
        moveLeft: 0,
        moveTop: 0,
        bigLeft: 0,
        bigTop: 0
      }
    },
    props: {
      smallImg: {
        type: String
      },
      bigImg: {
        type: String
      }
    },
    methods: {
      showImgs () {
        this.showMove = true
        this.showBig = true
      },
      hideImgs () {
        this.showMove = false
        this.showBig = false
      },
      moveImgs (value) {
        let box = document.getElementsByClassName('magnifier')
        let move = document.getElementsByClassName('magnifier-box-move')
        if (move[0].offsetWidth !== 0) {
          this.moveLeft = value.clientX + box[0].scrollLeft - box[0].offsetLeft - (move[0].offsetWidth / 2) + window.scrollX
          this.moveTop = value.clientY + box[0].scrollTop - box[0].offsetTop - (move[0].offsetHeight / 2) + window.scrollY
          // 限制x
          if (this.moveLeft < 0) {
            this.moveLeft = 0
          } else if (this.moveLeft > box[0].clientWidth - move[0].offsetWidth) {
            this.moveLeft = box[0].clientWidth - move[0].offsetWidth
          } else if (move[0].offsetWidth === 0) {
            if (this.moveLeft !== 0 && this.moveLeft < box[0].clientWidth) {
            }
          }
          // 限制Y
          if (this.moveTop < 0) {
            this.moveTop = 0
          } else if (this.moveTop > box[0].clientHeight - move[0].offsetHeight) {
            this.moveTop = box[0].clientHeight - move[0].offsetHeight
          }
          // 右侧大图坐标
          let scope = 800 / 450
          this.bigLeft = -(this.moveLeft * scope)
          this.bigTop = -(this.moveTop * scope)
          // console.log('left', this.moveLeft, 'box', box[0].clientHeight, 'move', move[0].offsetHeight)
        }
      }
    }
  }
</script>
<style scoped>
  .magnifier {
    position: relative;
    width: 450px;
    height: 450px;
  }

  .magnifier-box {
    position: relative;
    width: 100%;
    height: 100%;
  }

  .magnifier-box-move {
    position: absolute;
    height: 300px;
    width: 300px;
    background-color: red;
    opacity: 0.2;
    top: 0;
    left: 0;
    cursor: move;
  }

  .magnifier-box-img {
    width: 100%;
  }

  .magnifier-big {
    position: absolute;
    left: 460px;
    top: 0;
    height: 550px;
    width: 550px;
    overflow: hidden;
  }

  .magnifier-big-img {
    position: relative;
    width: 800px;
    object-fit: cover;
  }
</style>
<style>
  * {
    margin: 0 auto;
  }
</style>
