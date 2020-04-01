<template>
  <div class="home">
    <div class="page1" v-if="go">
      <!-- 打字 -->
      <div class="typewriting">
        <h1>
          <span class="typing"></span>
          <span class="mark"></span>
        </h1>
      </div>
      <div class="button" v-show="appear">
        <!-- 按钮 -->
        <router-link class="tointro" to="/introduce" @click="a">
          <span></span>
          <span></span>
          <span></span>
          <span></span>
          GO!
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "type",
  data() {
    return {
      texts: [
        "首先感谢您能点看这个网站",
        "我叫刘炳坤",
        "热爱前端和编程",
        "这是一份简历"
      ],
      appear: false,
      typedata: {
        count: 0,
        index: 0,
        currentText: "",
        letter: "",
        flag: 1
      },
      go: true
    };
  },
  mounted() {
    this.type();
  },
  methods: {
    //打字
    type() {
      this.typedata.currentText = this.texts[this.typedata.count]; //数组里的值
      if (this.typedata.letter.length === this.typedata.currentText.length) {
        //如果一个值打印完毕
        //判断是否整个数组循环完毕
        if (this.typedata.count + 1 === this.texts.length) {
          this.appear = true;
          clearTimeout(back);
          return;
        }
        this.typedata.flag = 0;
      }
      if (this.typedata.flag) {
        //如果是打字状态
        this.typedata.letter = this.typedata.currentText.slice(
          0,
          ++this.typedata.index
        );
        document.querySelector(".typing").innerHTML = this.typedata.letter;
      } else {
        //删除状态
        this.typedata.letter = this.typedata.currentText.slice(
          0,
          --this.typedata.index
        );
        document.querySelector(".typing").innerHTML = this.typedata.letter;
        if (!this.typedata.index) {
          this.typedata.count++;
          this.typedata.flag = 1;
        }
      }
      var back = setTimeout(this.type, parseInt(Math.random() * 200 + 100));
    },
    a() {
      this.go = false;
    }
  }
};
</script>

<style lang="scss" scoped>
@import "../assets/scss/mixin.scss";
.home {
  height: 100vh;
  background-color: #000000;
  .page1 {
    .typewriting {
      @include center(50%, 40%);
      h1 {
        margin-bottom: 40px;
        font-weight: 100;
        color: #b0b0b0;
        span.mark {
          border-right: 2px solid white;
          animation: blink 0.6s step-end infinite;
        }
      }
    }
    //文本闪烁
    @keyframes blink {
      from,
      to {
        border-color: transparent;
      }
      50% {
        border-color: white;
      }
    }
    .button {
      .tointro {
        @include center(50%, 55%);
        display: inline-block;
        padding: 12px 20px;
        color: #2196f3;
        text-transform: uppercase;
        letter-spacing: 4px;
        text-decoration: none;
        font-size: 24px;
        overflow: hidden;
        transition: 0.2s;
        &:hover {
          color: #255784;
          background-color: #2196f3;
          box-shadow: 0 0 10px #2196f3, 0 0 40px #2196f3, 0 0 80px #2196f3;
          transition-delay: 1s;
          span:nth-child(1) {
            left: 100%;
            transition: 1s;
          }

          span:nth-child(3) {
            right: 100%;
            transition: 1s;
            transition-delay: 0.5s;
          }

          span:nth-child(2) {
            top: 100%;
            transition: 1s;
            transition-delay: 0.25s;
          }

          span:nth-child(4) {
            bottom: 100%;
            transition: 1s;
            transition-delay: 0.75s;
          }
        }
        span {
          position: absolute;
          display: block;
          &:nth-child(1) {
            top: 0;
            left: -100%;
            width: 100%;
            height: 2px;
            background: linear-gradient(90deg, transparent, #2196f3);
          }
          &:nth-child(3) {
            bottom: 0;
            right: -100%;
            width: 100%;
            height: 2px;
            background: linear-gradient(270deg, transparent, #2196f3);
          }
          &:nth-child(2) {
            top: -100%;
            right: 0;
            width: 2px;
            height: 100%;
            background: linear-gradient(180deg, transparent, #2196f3);
          }
          &:nth-child(4) {
            bottom: -100%;
            left: 0;
            width: 2px;
            height: 100%;
            background: linear-gradient(360deg, transparent, #2196f3);
          }
        }
      }
    }
  }
}
// .come {

// }
@keyframes goo {
  from {
    background-color: #333333;
  }
  to {
    background: linear-gradient(90deg, #333333 30%, #b0b0b0 10%, #000000 100%);
  }
}
</style>