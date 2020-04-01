<template>
  <div class="introduce">
    <pre class="typing"></pre>
    <div class="picture">
      <img :class="{'shixi':picture1}" src="/imgs/introduce/dalian1.png" alt />
      <img :class="{'shixi':picture1}" src="/imgs/introduce/dalian2.png" alt />
      <img :class="{'shixi':picture2}" src="/imgs/introduce/kaoyan.png" alt />
    </div>
    <router-link class="togame" to="/game" v-show="appear">一个拼图小游戏</router-link>
  </div>
</template>

<script>
export default {
  data() {
    return {
      texts: [
        "基本介绍",
        "我叫刘炳坤，山东人，2020届本科毕业于大连大学，酒店管理专业",
        "我知道自己与科班出生的人有很大差距，但我真的喜欢编程，有一颗学习新技术的好奇心",
        "在大三的时候自学了C语言、数据库、数据结构、计算机网络基础",
        "在2019.7到2020.1.22疫情爆发前在大连金石滩鲁能希尔顿酒店当礼宾实习生(专业硬性要求)",
        "在实习的情况下决定考研,但....考研数学教我做人,说这些只是想说我真的喜欢，愿意去学",
        "专业技能",
        "熟练掌握HTML5,CSS3,原生JS,ES6,jquery,Ajax,scss,了解http原理",
        "熟悉vue，这网页就是用vue写的",
        "热爱生活,积极向上,自学能力强"
      ],
      appear: false,
      typedata: {
        count: 0,
        index: 0,
        currentText: "",
        letter: "",
        flag: 1
      },
      go: true,
      picture1: false,
      picture2: false
    };
  },
  mounted() {
    this.type();
  },
  methods: {
    //打字
    type() {
      this.typedata.flag = 1;
      this.typedata.currentText = this.texts[this.typedata.count]; //数组里的值
      //如果一个值打印完毕
      if (this.typedata.index === this.typedata.currentText.length) {
        if (this.typedata.count === 4) {
          this.picture1 = true;
        }
        if (this.typedata.count === 5) {
          this.picture2 = true;
        }
        //判断是否整个数组循环完毕
        if (this.typedata.count + 1 === this.texts.length) {
          this.appear = true;
          clearTimeout(back);
          return;
        }
        document.querySelector(".typing").innerHTML += "&#10;";
        this.typedata.count++;
        this.typedata.index = 0;
        this.typedata.flag = 0;
      }
      if (this.typedata.flag) {
        //如果是打字状态
        this.typedata.letter = this.typedata.currentText.slice(
          this.typedata.index,
          ++this.typedata.index
        );
        document.querySelector(".typing").innerHTML += this.typedata.letter;
      }
      var back = setTimeout(this.type, parseInt(Math.random() * 150 + 50));
    }
  }
};
</script>

<style lang="scss" scoped>
.introduce {
  height: 100vh;
  background-color: #000000;
  .typing {
    position: fixed;
    top: 30%;
    left: 20%;
    color: green;
    font-size: 12px;
    line-height: 20px;
  }
  .picture {
    position: fixed;
    top: 0;
    right: 0;
    img {
      opacity: 0;
      transition: opacity 1s;
      &:nth-child(1) {
        top: 20px;
        right: 40px;
        position: absolute;
        height: 300px;
        width: 400px;
      }
      &:nth-child(2) {
        top: 250px;
        right: 150px;
        position: absolute;
        height: 300px;
        width: 240px;
        transform: rotateZ(30deg);
      }
      &:nth-child(3) {
        top: 100px;
        right: 20px;
        position: absolute;
        height: 500px;
        width: 240px;
      }
    }
    .shixi {
      opacity: 1;
    }
  }
  .togame {
    position: absolute;
    top: 70%;
    left: 40%;
    width: 200px;
    height: 60px;
    text-align: center;
    line-height: 60px;
    color: #fff;
    font-style: 24px;
    box-sizing: border-box;
    background: linear-gradient(90deg, #03a9f4, #f441a5, #ffeb3b, #03a9f4);
    background-size: 400%;
    border-radius: 30px;
    z-index: 1;
    &:hover {
      animation: animate 8s linear infinite;
    }
    @keyframes animate {
      0% {
        background-position: 0%;
      }
      100% {
        background-position: 400%;
      }
    }
    &::before {
      content: "";
      position: absolute;
      top: -7px;
      left: -7px;
      right: -7px;
      bottom: -7px;
      z-index: -1;
      background: linear-gradient(90deg, #03a9f4, #f441a5, #ffeb3b, #03a9f4);
      background-size: 400%;
      border-radius: 40px;
      filter: blur(20px);
    }
  }
}
</style>