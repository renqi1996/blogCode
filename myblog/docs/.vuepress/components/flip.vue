<template>
  <div>
    <!-- 翻牌的外沿 -->
    <div class="flip" :class="[flipType, {'go': isFlipping}]">
      <!-- 前面的纸牌 -->
      <div class="digital front" :class="_textClass(frontTextFromData)"></div>
      <!-- 后面的纸牌 -->
      <div class="digital back" :class="_textClass(backTextFromData)"></div>
    </div>
  </div>
</template>

<script>
export default {
    name: 'flipClock',
    data() {
        return {
          count: 0,
          isFlipping: false,
          flipType: 'down',
          frontTextFromData: 0,
          backTextFromData: 1
        }
    },
    props: {
      frontText: {
        type: [Number, String],
        default: 0
      },
      backText: {
        type: [Number, String],
        default: 0
      },
      duration: {
        type: Number,
        default: 600
      }
    },
    methods: {
      _textClass: function (TextFromData) {
        return 'number' + TextFromData
      },
      _flip: function (type, front, back) {
        // this.isFlipping = false表示当前正在翻转中,不执行
        if (this.isFlipping) {
          return false
        }
        this.frontTextFromData = front
        this.backTextFromData = back
        this.flipType = type
        this.isFlipping = true
        setTimeout(() => {
          this.isFlipping = false
          this.frontTextFromData  = back
        }, this.duration)
      },
      flipDown: function (front, back) {
        this._flip('down', front, back)
      },
      flipUp: function (front, back) {
        this._flip('up', front, back)
      },
      setFront: function (text) {
        this.frontTextFromData = text
      },
      setBack: function (text) {
        this.backTextFromData = text
      }
    },
    created () {
      this.frontTextFromData = this.frontText
      this.backTextFromData = this.backText
    }
}
</script>

<style scoped>
.flip {
  display: inline-block;
  position: relative;
  width: 60px;
  height: 100px;
  line-height: 100px;
  border: 1px solid #000;
  border-radius: 10px;
  background: #ffffff;
  font-size: 66px;
  color: #ffffff;
  box-shadow: 0 0 6px rgba(0, 0, 0, .5);
  text-align: center;
  font-family: "Helvetica Neue"
}
.flip .digital:before,
.flip .digital:after {
  content: '';
  position: absolute;
  left: 0;
  right: 0;
  background: #000;
  overflow: hidden;
  box-sizing: border-box; /*下边框不会影响到整个高度，兼容性有待考虑，详见MDN*/
}
.flip .digital:before {
  top: 0;
  bottom: 50%;
  border-radius: 10px 10px 0 0 ;
  border-bottom: 1px solid #666;
}
.flip .digital:after {
  top: 50%;
  bottom: 0;
  border-radius: 0 0 10px 10px;
  line-height: 0px;
}
.flip.down .front:before {
  z-index: 3;
}
.flip.down .back:after {
  z-index: 2;
  transform-origin: 50% 0%; /* 翻转基准点 */
  transform: perspective(160px) rotateX(180deg);
}
.flip.up .front:after {
  z-index: 3;
}
.flip.up .back:before {
  z-index: 2;
  transform-origin: 50% 100%;
  transform: perspective(160px) rotateX(-180deg);
}
.flip.up .front:before,
.flip.up .back:after {
  z-index: 1;
}
.flip.down .front:after,
.flip.down .back:before {
  z-index: 1;
}
/* css设置纸牌翻转动画 */
.flip.down.go .front:before {
  transform-origin: 50% 100%;
  animation: frontFlipDown 0.6s ease-in-out both;
  box-shadow: 0 -2px 6px rgba(255, 255, 255, 0.3);
  backface-visibility: hidden;
}
.flip.down.go .back:after {
    animation: backFlipDown 0.6s ease-in-out both;
}
/* keyframes 使其匀速运动 */
@keyframes frontFlipDown {
  0% {
    transform: perspective(160px) rotateX(0deg);
  }
  100% {
    transform: perspective(160px) rotateX(-180deg);
  }
}
@keyframes backFlipDown {
  0% {
    transform: perspective(160px) rotateX(180deg);
  }
  100% {
    transform: perspective(160px) rotateX(0deg);
  }
}
.flip.up.go .front:after {
  transform-origin: 50% 0;
  animation: frontFlipUp 0.6s ease-in-out both;
  box-shadow: 0 2px 6px rgba(255, 255, 255, 0.3);
  backface-visibility: hidden;
}

.flip.up.go .back:before {
  animation: backFlipUp 0.6s ease-in-out both;
}
@keyframes frontFlipUp {
  0% {
    transform: perspective(160px) rotateX(0deg);
  }

  100% {
    transform: perspective(160px) rotateX(180deg);
  }
}

@keyframes backFlipUp {
  0% {
    transform: perspective(160px) rotateX(-180deg);
  }

  100% {
    transform: perspective(160px) rotateX(0deg);
  }
}
/* css设置纸牌显示文字 */
.flip .number0:before,
.flip .number0:after {
  content: '0';
}
.flip .number1:before,
.flip .number1:after {
  content: '1';
}
.flip .number2:before,
.flip .number2:after {
  content: '2';
}
.flip .number3:before,
.flip .number3:after {
  content: '3';
}
.flip .number4:before,
.flip .number4:after {
  content: '4';
}
.flip .number5:before,
.flip .number5:after {
  content: '5';
}
.flip .number6:before,
.flip .number6:after {
  content: '6';
}
.flip .number7:before,
.flip .number7:after {
  content: '7';
}
.flip .number8:before,
.flip .number8:after {
  content: '8';
}
.flip .number9:before,
.flip .number9:after {
  content: '9';
}
</style>