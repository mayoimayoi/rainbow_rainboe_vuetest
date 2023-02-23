<script setup>
import { ref } from "vue";
import TheFooter from "./components/TheFooter.vue";
import TheHeader from "./components/TheHeader.vue";
import ConcentrateImage from "./assets/ConcentrateImage.png";
import HarmonyImage from "./assets/HarmonyImage.png";
import ImaginationImage from "./assets/ImaginationImage.png";
import ImpulsivityImage from "./assets/ImpulsivityImage.png";
import InstantaneousImage from "./assets/InstantaneousImage.png";
import ObsessionImage from "./assets/ObsessionImage.png";
import TalkImage from "./assets/TalkImage.png";

// 変数へ初期値を代入
const questionBox = [
  ["スタートボタンを押してください"],
  [
    "約束の時間に遅れることが多い",
    "一度決めた方法は変えたくない",
    "人が話し終わるのを待てないことがある",
    "変わっているねとよく言われるやばへき"
  ],
  [
    "物事の要点をつかむのが得意だ",
    "子どもの頃から整理整頓が苦手",
    "いつも探し物をしている",
    "大人数での雑談、集団行動を避けてしまう、"
  ],
  [
    "転職や引越しで、心機一転することが好き",
    "頭の中はいつもアイデアであふれている",
    "新しく物を買っても、あまり説明書は読まない。",
    "周りから考えすぎ、やりすぎと言われることが多い。"
  ],
  [
    "数時間から数日の間で気分に波がある。",
    "何から手をつけて良いか分からない時がある",
    "やりすぎてしまい、あとで落ち込むことがある",
    "一日が終わると、ぐったりしてしまう"
  ],
  [
    "音に敏感で、作業に集中できなくなることが多い。",
    "何を取りに来たのか、何を言おうとしたのかなどをよく忘れる。",
    "頭の中にモヤがかかったような感じがすることが多い。",
    "自他共に認めるマイペース"
  ],
  [
    "ささいなことで怒ってしまうことがある",
    "ちょっとした物でも、簡単に捨てることができない。",
    "作業の途中で、他のことを考えてしまったりする",
    "勢いで、つい正論をふりかざしてしまうことがある"
  ],
  [
    "長時間じっと座っていることが苦手だ",
    "子どもの頃からよく転んだりぶつかったりする",
    "人が自分の話の要点を飲み込めないときなど、心の中で爆発しそうになる。",
    "子どもの頃から感受性が強く、感覚が鋭敏だった。"
  ]
];
let questionNumber = 0;
let questionKind = 6;
let questionCount = 1;
let playerStatus = [0, 0, 0, 0, 0, 0, 0, 0];
let questionNeedCount = 1;
const titleContent = ref("あなたの得意を分析してみましょう");
const quesitonContent = ref(questionBox[0][0]);
const selectBtn = ref(false);
const startBtn = ref(true);
const retryBtn = ref(false);
const titleBox = ref(true);
const charengeResultShow = ref(false);
const keepResultShow = ref(false);
const changeShowCharacter = ref(false);
const harmonyImageShow = ref(false);
const imaginationImageShow = ref(false);
const impulsivityImageShow = ref(false);
const instantaneousImageShow = ref(false);
const obsessionImageShow = ref(false);
const talkImageShow = ref(false);

// 問題を20個のうちからランダム持ってくるための関数
function GetRandomInt(min, max) {
  min = Math.ceil(min);
  max = Math.floor(max);
  return Math.floor(Math.random() * (max - min) + min); //The maximum is exclusive and the minimum is inclusive
}

// 質問をランダムで返す関数
const ChangeQuestion = () => {
  questionKind = GetRandomInt(1, 7);
  questionNumber = GetRandomInt(0, 3);
  return questionBox[questionKind][questionNumber];
};

// スタートボタンを押した時の動作
const startDiagnosis = () => {
  // 質問に答える数を指定する
  questionNeedCount = document.getElementById("questionNeedNumber").value;
  quesitonContent.value = ChangeQuestion();
  ChangeShowCharacter();
  startBtn.value = !startBtn.value;
  selectBtn.value = !selectBtn.value;
  titleBox.value = !titleBox.value;
};

// リトライボタンを押した時の操作
const retryDiagnosis = () => {
  quesitonContent.value = questionBox[0][0];
  titleContent.value = "あなたの得意を分析してみましょう";
  document.getElementById("titleContentId").style.color = "black";
  document.getElementById("titleContentId").style.fontWeight = "normal";
  startBtn.value = !startBtn.value;
  retryBtn.value = !retryBtn.value;
  charengeResultShow.value = false;
  keepResultShow.value = false;
  questionCount = 1;
};

// 結果を表示する
const ResultDiagnosis = () => {
  ChangeShowCharacter();
  selectBtn.value = !selectBtn.value;
  retryBtn.value = !retryBtn.value;
  titleBox.value = !titleBox.value;
  document.getElementById("titleContentId").style.color = "red";
  document.getElementById("titleContentId").style.fontWeight = "bold";
  titleContent.value = "あなたの診断結果です";
  quesitonContent.value = "あなたはライオンさんタイプです";
  charengeResultShow.value = !charengeResultShow.value;
};

// はいかいいえを押した時の操作
const NextQestion = (selectAnswer) => {
  if (selectAnswer == "Yes") {
    playerStatus[questionKind] += 1;
  }
  ChangeShowCharacter();
  quesitonContent.value = ChangeQuestion();
  ChangeShowCharacter();
  if (questionCount == questionNeedCount) {
    ResultDiagnosis();
  } else {
    questionCount = questionCount + 1;
  }
};

// 該当の番号のキャラクター画像の表示を切り替える関数（非表示にもする）
const ChangeShowCharacter = () => {
  switch (questionKind) {
    case 1:
      changeShowCharacter.value = !changeShowCharacter.value;
      break;
    case 2:
      harmonyImageShow.value = !harmonyImageShow.value;
      break;
    case 3:
      imaginationImageShow.value = !imaginationImageShow.value;
      break;
    case 4:
      impulsivityImageShow.value = !impulsivityImageShow.value;
      break;
    case 5:
      instantaneousImageShow.value = !instantaneousImageShow.value;
      break;
    case 6:
      obsessionImageShow.value = !obsessionImageShow.value;
      break;
    case 7:
      talkImageShow.value = !talkImageShow.value;
      break;
  }
};
</script>
<template>
  <TheHeader />
  <div class="container-fluid">
    <div class="mainbox row">
      <div class="col-12">
        <!-- 画像画像 -->
        <div class="characterimg">
          <div v-show="changeShowCharacter">
            <img :src="ConcentrateImage" alt="集中力画像" />
          </div>
          <div v-show="harmonyImageShow">
            <img :src="HarmonyImage" alt="調和性画像" />
          </div>
          <div v-show="imaginationImageShow">
            <img :src="ImaginationImage" alt="想像力画像" />
          </div>
          <div v-show="impulsivityImageShow">
            <img :src="ImpulsivityImage" alt="衝動性画像" />
          </div>
          <div v-show="instantaneousImageShow">
            <img :src="InstantaneousImage" alt="瞬発力画像" />
          </div>
          <div v-show="obsessionImageShow">
            <img :src="ObsessionImage" alt="こだわり画像" />
          </div>
          <div v-show="talkImageShow">
            <img :src="TalkImage" alt="会話画像" />
          </div>
        </div>
        <!-- 質問画面 -->
        <div v-show="titleBox" class="mt-3">
          <h1 id="titleContentId">{{ titleContent }}</h1>
        </div>
        <div class="quesitonbox flexbox mt-3">
          <p>{{ quesitonContent }}</p>
        </div>
        <div class="mt-3">
          <div v-show="startBtn">
            <div class="my-3">
              <p>質問に答える数を指定してください</p>
              <input type="number" id="questionNeedNumber" value="1" />
            </div>
            <button class="startbtn blue" @click="startDiagnosis">
              スタート
            </button>
          </div>
          <div v-show="selectBtn">
            <div class="row">
              <div class="col-md-2"></div>
              <div class="col-md-4 mt-3">
                <button class="btn whiteblue" @click="NextQestion('Yes')">
                  はい
                </button>
              </div>
              <div class="col-md-4 mt-3">
                <button class="btn red" @click="NextQestion('No')">
                  いいえ
                </button>
              </div>
              <div class="col-md-2"></div>
            </div>
          </div>
        </div>
        <!-- 結果表示画面 -->
        <div v-show="charengeResultShow" class="mt-5">
          <div class="row">
            <div class="col-1"></div>
            <div id="bar-graph" class="content col-10">
              <div class="box15">
                <h2 class="c-title">あなたの虹色ステータス</h2>
                <div class="bar-graph-wrap">
                  <div class="graph red mt-3">
                    <span class="name">勉強</span>
                    <span class="number">65%</span>
                  </div>
                  <div class="graph orange mt-3">
                    <span class="name">お手伝い</span>
                    <span class="number">36%</span>
                  </div>
                  <div class="graph yellow mt-3">
                    <span class="name">お話</span>
                    <span class="number">76%</span>
                  </div>
                  <div class="graph green mt-3">
                    <span class="name">友達</span>
                    <span class="number">27%</span>
                  </div>
                  <div class="graph lightblue mt-3">
                    <span class="name">コツコツ</span>
                    <span class="number">40%</span>
                  </div>
                  <div class="graph blue mt-3">
                    <span class="name">遊び</span>
                    <span class="number">20%</span>
                  </div>
                  <div class="graph purple mt-3">
                    <span class="name">PC</span>
                    <span class="number">27%</span>
                  </div>
                </div>
              </div>
              <div class="box15 mt-3">
                <h3>ライオンさんタイプの個性</h3>
                <p>
                  友達思いなあなたはみんなの中心になって引っ張っていける存在です
                </p>
                <p>
                  ただたまに色んな事に興味を持ちすぎてしまったりするので注意
                </p>
              </div>
              <div class="my-3">
                <a href="#">あなたの才能をもっと伸ばす方法はこちらをクリック</a>
              </div>
            </div>
            <div class="col-1"></div>
          </div>
          <button class="startbtn red mt-5" @click="retryDiagnosis">
            リトライ
          </button>
        </div>
      </div>
    </div>
    <TheFooter />
  </div>
</template>
<style scoped>
.flexbox {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
.mainbox {
  width: 90%;
  margin: 0 auto;
  padding: 20px 30px;
  background: #f1ffe0;
  box-shadow: 0px 0px 0px 10px #e2e8cc;
  border: dashed 2px white;
}
.mainbox p {
  margin: 0;
  padding: 0;
}
.quesitonbox {
  height: 100px;
  background: #ffffee;
  box-shadow: 0px 0px 0px 5px #ffe00f;
  border: dashed 3px yellow;
  border-radius: 10px;
  font-size: 24px;
}
.quesitonbox p {
  margin: 0;
  padding: 0;
}
.btn {
  padding: 10px 20px;
  margin: 10px 0;
  font-size: 20px;
  width: 90%;
}
.startbtn {
  padding: 10px 20px;
  margin: 10px 0;
  font-size: 20px;
  width: 30%;
}
.blue {
  background-color: aqua;
}
.whiteblue {
  background-color: deepskyblue;
}
.red {
  background-color: indianred;
}
.characterimg {
  margin: 0 auto;
  width: 30%;
}
@media screen and (max-width: 639px) {
  /*スマホ用のcssを記述*/
  .characterimg {
    width: 100%;
  }
  .btn {
    /* スマホ用の時はwidth: 80%;にする */
    width: 70%;
  }
  .quesitonbox {
    height: 70px;
    font-size: 20px;
  }
  .startbtn {
    padding: 10px 20px;
    margin: 10px 0;
    font-size: 20px;
    width: 50%;
  }
}
.weblink {
  font-size: 24px;
}

.bar-graph-wrap {
  position: relative;
  height: 450px;
  -webkit-box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2);
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2);
  overflow: hidden;
}
.bar-graph-wrap .graph {
  height: 40px;
  position: absolute;
  left: 0;
  border-radius: 0 4px 4px 0;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-align: center;
  -ms-flex-align: center;
  align-items: center;
  -webkit-box-pack: justify;
  -ms-flex-pack: justify;
  justify-content: space-between;
  padding: 10px;
  -webkit-animation: graphAnim 2.5s forwards;
  animation: graphAnim 2.5s forwards;
}
.bar-graph-wrap .graph span {
  font-size: 14px;
  color: #ffffff;
}
@media screen and (max-width: 750px) {
  .bar-graph-wrap .graph span {
    font-size: 12px;
  }
}
.bar-graph-wrap .graph.red {
  top: 10px;
  background: #ff3051;
  width: 65%;
}
.bar-graph-wrap .graph.orange {
  top: 70px;
  background: #ffb030;
  width: 36%;
}
.bar-graph-wrap .graph.yellow {
  top: 130px;
  background: rgb(234, 234, 57);
  width: 40%;
}
.bar-graph-wrap .graph.green {
  top: 190px;
  background: greenyellow;
  width: 65%;
}
.bar-graph-wrap .graph.lightblue {
  top: 250px;
  background: rgb(0, 221, 255);
  width: 40%;
}
.bar-graph-wrap .graph.blue {
  top: 310px;
  background: blue;
  width: 20%;
}

.bar-graph-wrap .graph.purple {
  top: 370px;
  background: #c01fd2;
  width: 27%;
}

@-webkit-keyframes graphAnim {
  0% {
    -webkit-transform: translateX(-100%);
    transform: translateX(-100%);
  }
  100% {
    -webkit-transform: translateX(0);
    transform: translateX(0);
  }
}

@keyframes graphAnim {
  0% {
    -webkit-transform: translateX(-100%);
    transform: translateX(-100%);
  }
  100% {
    -webkit-transform: translateX(0);
    transform: translateX(0);
  }
}

.box15 {
  padding: 0.2em 0.5em;
  margin: 2em 0;
  color: #565656;
  background: #ffeaea;
  box-shadow: 0px 0px 0px 10px #ffeaea;
  border: dashed 2px #ffc3c3;
  border-radius: 8px;
}
.box15 p {
  margin: 0;
  padding: 0;
}
</style>
