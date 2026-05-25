<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
<title>霊綴 - たまつづり</title>

<style>
*{
  margin:0;
  padding:0;
  box-sizing:border-box;
}

html,body{
  width:100%;
  height:100%;
  overflow:hidden;
  background:#0d0b08;
  font-family:"Yu Mincho","Hiragino Mincho ProN","Noto Serif JP",serif;
  user-select:none;
  -webkit-user-select:none;
  touch-action:none;
}

#viewport{
  position:fixed;
  inset:0;
  background:#0d0b08;
  overflow:hidden;
}

#stage{
  position:absolute;
  left:50%;
  top:50%;
  width:1366px;
  height:768px;
  transform-origin:center center;
  overflow:hidden;
  background:#14100c;
}

.screen{
  position:absolute;
  inset:0;
  opacity:0;
  pointer-events:none;
  transition:opacity .55s ease;
}

.screen.active{
  opacity:1;
  pointer-events:auto;
}

/* ================= TITLE ================= */

#titleScreen{
  background:
    radial-gradient(circle at 50% 35%, rgba(255,255,255,.35), transparent 36%),
    linear-gradient(180deg, #e9dfc8 0%, #c7b89b 55%, #342a22 100%);
  background-size:cover;
  background-position:center;
}

#titleScreen.hasImage{
  background-image:var(--title-bg);
  background-size:cover;
  background-position:center;
}

.titleShade{
  position:absolute;
  inset:0;
  background:
    radial-gradient(circle at 50% 42%, transparent 0 48%, rgba(0,0,0,.22) 100%),
    linear-gradient(180deg, rgba(0,0,0,.05), transparent 30%, rgba(0,0,0,.18));
  pointer-events:none;
}

.titleLogo{
  position:absolute;
  left:50%;
  top:38%;
  transform:translate(-50%,-50%);
  color:#120c08;
  text-align:center;
  z-index:3;
  text-shadow:
    0 2px 0 rgba(255,255,255,.35),
    0 10px 18px rgba(0,0,0,.22);
}

.hasImage .titleLogo{
  display:none;
}

.titleLogo .main{
  font-size:118px;
  font-weight:900;
  letter-spacing:.22em;
}

.titleLogo .sub{
  margin-top:8px;
  font-size:25px;
  letter-spacing:.5em;
  color:rgba(20,12,8,.72);
}

.startPrompt{
  position:absolute;
  left:50%;
  bottom:74px;
  transform:translateX(-50%);
  z-index:5;
  font-size:26px;
  font-weight:900;
  letter-spacing:.16em;
  color:rgba(45,28,18,.88);
  text-shadow:
    0 1px 0 rgba(255,255,255,.55),
    0 0 14px rgba(255,245,230,.6);
  animation:startBlink 2.4s ease-in-out infinite;
}

.startPrompt::before,
.startPrompt::after{
  content:"";
  display:inline-block;
  width:28px;
  height:2px;
  background:rgba(147,36,27,.65);
  vertical-align:middle;
  margin:0 18px;
}

@keyframes startBlink{
  0%,100%{opacity:.45;}
  50%{opacity:1;}
}

.inkRipple{
  position:absolute;
  width:20px;
  height:20px;
  border-radius:50%;
  border:2px solid rgba(145,28,22,.65);
  transform:translate(-50%,-50%);
  animation:inkRipple .9s ease-out forwards;
  pointer-events:none;
  z-index:20;
}

@keyframes inkRipple{
  to{
    width:560px;
    height:560px;
    opacity:0;
    border-width:18px;
  }
}

/* ================= LOADING ================= */

#loadingScreen{
  background:
    radial-gradient(circle at 24% 48%, rgba(255,235,210,.55), transparent 28%),
    linear-gradient(90deg, #ede3cf, #d8c8a9 58%, #2a2119);
  color:#1b120b;
}

#loadingScreen::before{
  content:"";
  position:absolute;
  inset:0;
  background:
    repeating-linear-gradient(12deg, rgba(45,30,18,.04) 0 1px, transparent 1px 8px),
    repeating-linear-gradient(-18deg, rgba(255,255,255,.09) 0 1px, transparent 1px 9px);
  pointer-events:none;
}

.loadingChar{
  position:absolute;
  left:118px;
  bottom:0;
  width:430px;
  height:690px;
  z-index:3;
}

.loadingChar::before{
  content:"";
  position:absolute;
  left:45px;
  top:110px;
  width:340px;
  height:470px;
  background:radial-gradient(circle, rgba(255,225,200,.45), transparent 65%);
  filter:blur(18px);
}

.loadingChar img{
  position:absolute;
  left:15px;
  bottom:0;
  max-width:390px;
  max-height:680px;
  object-fit:contain;
  filter:drop-shadow(0 14px 16px rgba(0,0,0,.35));
}

.loadingText{
  position:absolute;
  right:66px;
  bottom:48px;
  z-index:5;
  font-family:Georgia, "Times New Roman", serif;
  font-size:31px;
  letter-spacing:.08em;
  color:rgba(245,235,214,.92);
  text-shadow:0 3px 9px rgba(0,0,0,.75);
}

.loadingDots::after{
  content:"";
  animation:dots 1.4s steps(4,end) infinite;
}

@keyframes dots{
  0%{content:"";}
  25%{content:".";}
  50%{content:"..";}
  75%,100%{content:"...";}
}

/* ================= HOME ================= */

#homeScreen{
  background-image:var(--home-bg);
  background-size:cover;
  background-position:center;
}

#homeScreen::after{
  content:"";
  position:absolute;
  inset:0;
  pointer-events:none;
  background:
    radial-gradient(circle at 47% 43%, transparent 0 58%, rgba(0,0,0,.18) 100%),
    linear-gradient(180deg, rgba(0,0,0,.04), transparent 22%, transparent 76%, rgba(0,0,0,.12));
  z-index:2;
}

.panel{
  position:absolute;
  z-index:5;
  background-image:var(--panel-bg);
  background-size:100% 100%;
  background-repeat:no-repeat;
  color:#1a120d;
  font-weight:900;
  text-shadow:0 1px 0 rgba(255,255,255,.35);
}

/* top */

.playerPanel{
  left:126px;
  top:25px;
  width:330px;
  height:88px;
  padding:15px 26px;
  font-size:24px;
  line-height:1.35;
}

.playerPanel .level{
  margin-left:30px;
  font-size:22px;
}

.playerPanel .bar{
  position:absolute;
  left:55px;
  right:55px;
  bottom:22px;
  height:7px;
  background:rgba(30,20,15,.75);
  border-radius:999px;
  overflow:hidden;
}

.playerPanel .bar::before{
  content:"";
  display:block;
  width:38%;
  height:100%;
  background:linear-gradient(90deg,#9b2d24,#e78b73);
}

.playerPanel .next{
  position:absolute;
  right:56px;
  bottom:2px;
  font-size:16px;
}

.resource{
  top:25px;
  width:235px;
  height:88px;
  padding:15px 20px;
  text-align:center;
  font-size:27px;
  line-height:1.15;
}

.resource small{
  display:block;
  font-size:21px;
}

.res1{left:478px;}
.res2{left:733px;}
.res3{left:988px;}

.utility{
  top:22px;
  width:70px;
  height:95px;
  padding-top:17px;
  text-align:center;
  font-size:17px;
  line-height:1.4;
  opacity:.9;
  cursor:pointer;
}

.utility .icon{
  display:block;
  font-size:27px;
  margin-bottom:3px;
}

.u1{right:190px;}
.u2{right:108px;}
.u3{right:26px;}

/* hiyori */

.hiyori{
  position:absolute;
  left:80px;
  bottom:92px;
  width:420px;
  height:585px;
  z-index:4;
  cursor:pointer;
}

.hiyori::before{
  content:"";
  position:absolute;
  left:20px;
  top:60px;
  width:380px;
  height:470px;
  background:radial-gradient(circle, rgba(255,220,200,.45), transparent 68%);
  filter:blur(16px);
  opacity:.9;
}

.hiyori img{
  position:absolute;
  left:20px;
  bottom:0;
  max-width:390px;
  max-height:585px;
  object-fit:contain;
  filter:drop-shadow(0 12px 12px rgba(0,0,0,.35));
  transition:transform .25s ease, filter .25s ease;
}

.hiyori.active img{
  transform:translateY(-5px) scale(1.015);
  filter:
    drop-shadow(0 12px 12px rgba(0,0,0,.35))
    drop-shadow(0 0 20px rgba(210,80,55,.45));
}

.spiritFire{
  position:absolute;
  width:44px;
  height:60px;
  opacity:.7;
  z-index:6;
  animation:floatFire 3.2s ease-in-out infinite;
}

.spiritFire::before{
  content:"";
  position:absolute;
  inset:5px 9px;
  background:linear-gradient(180deg, rgba(255,230,210,.82), rgba(218,92,70,.7));
  clip-path:polygon(50% 0%,75% 27%,66% 48%,88% 63%,63% 100%,50% 78%,36% 100%,12% 63%,34% 48%,25% 28%);
}

.fireA{left:350px;top:140px;}
.fireB{left:82px;top:290px;animation-delay:.9s;transform:scale(.78);}
.fireC{left:310px;top:70px;animation-delay:1.7s;transform:scale(.58);}

@keyframes floatFire{
  0%,100%{transform:translateY(0);opacity:.48;}
  50%{transform:translateY(-14px);opacity:.9;}
}

.talk{
  left:56px;
  bottom:132px;
  width:315px;
  height:116px;
  padding:20px 28px;
  font-size:21px;
  line-height:1.55;
  z-index:8;
}

.talk .kana{
  font-size:15px;
  letter-spacing:.3em;
}

.talk .name{
  font-size:27px;
}

.talk .line{
  height:1px;
  background:rgba(40,25,18,.28);
  margin:6px 0 9px;
}

/* right panels */

.daily{
  left:530px;
  top:274px;
  width:295px;
  height:225px;
  padding:28px 34px;
  font-size:19px;
}

.daily h2{
  font-size:28px;
  margin-bottom:20px;
  letter-spacing:.12em;
}

.daily p{
  display:flex;
  justify-content:space-between;
  margin:17px 0;
  font-size:18px;
}

.storyCard{
  position:absolute;
  z-index:5;
  width:245px;
  height:142px;
  border:2px solid rgba(55,38,25,.7);
  box-shadow:0 6px 12px rgba(0,0,0,.28);
  background:
    linear-gradient(rgba(0,0,0,.25),rgba(0,0,0,.25)),
    var(--home-bg);
  background-size:900px auto;
  color:#f4ead5;
  padding:25px 26px;
  text-shadow:0 2px 3px rgba(0,0,0,.8);
  cursor:pointer;
}

.storyCard h2{
  font-size:28px;
  margin-bottom:8px;
}

.storyCard p{
  font-size:16px;
}

.memory{
  left:848px;
  top:284px;
  background-position:70% 52%;
}

.lost{
  left:1110px;
  top:284px;
  background-position:92% 54%;
}

.sortie{
  left:850px;
  bottom:150px;
  width:455px;
  height:150px;
  padding-top:34px;
  text-align:center;
  font-size:64px;
  color:#8f2b1d;
  letter-spacing:.18em;
  z-index:7;
  cursor:pointer;
  transition:transform .18s ease, filter .18s ease;
}

.sortie:hover{
  transform:translateY(-3px);
  filter:brightness(1.04);
}

.sortie small{
  display:block;
  margin-top:3px;
  font-size:24px;
  color:#2a1b13;
  letter-spacing:.12em;
}

/* nav */

.nav{
  position:absolute;
  left:34px;
  right:34px;
  bottom:22px;
  height:106px;
  z-index:10;
  display:flex;
  gap:22px;
}

.navItem{
  position:relative;
  flex:1;
  height:100%;
  background-image:var(--panel-bg);
  background-size:100% 100%;
  background-repeat:no-repeat;
  display:flex;
  align-items:center;
  justify-content:center;
  gap:18px;
  color:#1d130d;
  font-size:34px;
  font-weight:900;
  letter-spacing:.08em;
  cursor:pointer;
  transition:
    transform .18s ease,
    filter .18s ease,
    box-shadow .18s ease;
}

.navItem:hover{
  transform:translateY(-3px);
}

.navItem.active{
  color:#8e251b;
  filter:brightness(1.08) saturate(1.08);
  box-shadow:
    0 0 10px rgba(190,45,32,.35),
    0 0 22px rgba(190,45,32,.32),
    inset 0 0 24px rgba(190,45,32,.13);
}

.navItem.active::before{
  content:"";
  position:absolute;
  inset:7px;
  border:2px solid rgba(178,38,28,.48);
  border-radius:6px;
  pointer-events:none;
}

.navItem.active::after{
  content:"";
  position:absolute;
  inset:0;
  background:
    radial-gradient(circle at 50% 50%, rgba(196,52,39,.16), transparent 62%);
  pointer-events:none;
  mix-blend-mode:multiply;
}

.navIcon{
  position:relative;
  z-index:2;
  font-size:32px;
  opacity:.82;
}

.navLabel{
  position:relative;
  z-index:2;
}

/* sound button */

.soundBtn{
  position:absolute;
  left:34px;
  top:128px;
  width:126px;
  height:46px;
  z-index:30;
  border:1px solid rgba(55,35,22,.45);
  border-radius:999px;
  background:rgba(245,231,205,.62);
  color:#2b1c12;
  font-size:18px;
  font-weight:900;
  letter-spacing:.04em;
  cursor:pointer;
  box-shadow:0 4px 10px rgba(0,0,0,.18);
}

/* fade */

#fade{
  position:absolute;
  inset:0;
  background:#0c0907;
  opacity:0;
  pointer-events:none;
  z-index:100;
  transition:opacity .45s ease;
}

#fade.show{
  opacity:1;
}
</style>
</head>

<body>
<div id="viewport">
  <div id="stage">

    <!-- TITLE -->
    <section id="titleScreen" class="screen active">
      <div class="titleShade"></div>
      <div class="titleLogo">
        <div class="main">霊綴</div>
        <div class="sub">たまつづり</div>
      </div>
      <div class="startPrompt">画面をタップして物語を綴る</div>
    </section>

    <!-- LOADING -->
    <section id="loadingScreen" class="screen">
      <div class="loadingChar">
        <img id="loadingCharacter" src="https://i.imgur.com/vCd1ayg.png" alt="Loading Character">
      </div>
      <div class="loadingText">Loading<span class="loadingDots"></span></div>
    </section>

    <!-- HOME -->
    <section id="homeScreen" class="screen">

      <button class="soundBtn" id="soundBtn">音量 ON</button>

      <div class="panel playerPanel">
        綴師 <span class="level">Lv.23</span>
        <div class="bar"></div>
        <div class="next">あと 1,250</div>
      </div>

      <div class="panel resource res1">
        <small>霊片</small>
        1,580
      </div>

      <div class="panel resource res2">
        <small>銭</small>
        32,460
      </div>

      <div class="panel resource res3">
        <small>霊力</small>
        78/120
        <small>回復まで 01:34</small>
      </div>

      <div class="panel utility u1">
        <span class="icon">◇</span>
        贈物
      </div>

      <div class="panel utility u2">
        <span class="icon">⚙</span>
        設定
      </div>

      <div class="panel utility u3">
        <span class="icon">✦</span>
        お知らせ
      </div>

      <div class="hiyori" id="hiyori">
        <div class="spiritFire fireA"></div>
        <div class="spiritFire fireB"></div>
        <div class="spiritFire fireC"></div>
        <img src="https://i.imgur.com/vCd1ayg.png" alt="灯依">
      </div>

      <div class="panel talk">
        <div class="kana">ひより</div>
        <div class="name">灯依</div>
        <div class="line"></div>
        <div id="quote">……呼んでくれた？</div>
      </div>

      <div class="panel daily">
        <h2>✿ 本日の綴り</h2>
        <p><span>虚霊を5体討伐する</span><span>(3/5)</span></p>
        <p><span>記憶の欠片を集める</span><span>(0/8)</span></p>
        <p><span>霊力を1回受け取る</span><span>(1/1)</span></p>
      </div>

      <div class="storyCard memory">
        <h2>綴りの記憶</h2>
        <p>あなたが綴った記憶</p>
      </div>

      <div class="storyCard lost">
        <h2>失われた記録</h2>
        <p>名もなき物語を探す</p>
      </div>

      <div class="panel sortie" id="sortie">
        出陣
        <small>物語を綴る</small>
      </div>

      <div class="nav">
        <div class="navItem active" data-menu="ホーム">
          <span class="navIcon">⌂</span>
          <span class="navLabel">ホーム</span>
        </div>
        <div class="navItem" data-menu="編成">
          <span class="navIcon">◇</span>
          <span class="navLabel">編成</span>
        </div>
        <div class="navItem" data-menu="育成">
          <span class="navIcon">✿</span>
          <span class="navLabel">育成</span>
        </div>
        <div class="navItem" data-menu="霊録">
          <span class="navIcon">▣</span>
          <span class="navLabel">霊録</span>
        </div>
        <div class="navItem" data-menu="霊契">
          <span class="navIcon">◆</span>
          <span class="navLabel">霊契</span>
        </div>
      </div>

    </section>

    <div id="fade"></div>
  </div>
</div>

<script>
const TITLE_BG_URL = "https://i.imgur.com/8W04WLC.png";

const BGM_URL = "https://raw.githubusercontent.com/logicoolneoking-max/eldia-assets/main/%E8%8A%B1%E3%81%95%E3%81%9D%E3%81%B5.mp3";

const ASSETS = {
  homeBg: "https://i.imgur.com/cX4H0sC.png",
  panel: "https://i.imgur.com/NZSXeBT.png",
  hiyori: "https://i.imgur.com/vCd1ayg.png"
};

const BASE_W = 1366;
const BASE_H = 768;

const stage = document.getElementById("stage");
const titleScreen = document.getElementById("titleScreen");
const loadingScreen = document.getElementById("loadingScreen");
const homeScreen = document.getElementById("homeScreen");
const fade = document.getElementById("fade");
const quote = document.getElementById("quote");
const hiyori = document.getElementById("hiyori");
const sortie = document.getElementById("sortie");
const soundBtn = document.getElementById("soundBtn");

document.documentElement.style.setProperty("--home-bg", `url("${ASSETS.homeBg}")`);
document.documentElement.style.setProperty("--panel-bg", `url("${ASSETS.panel}")`);

if(TITLE_BG_URL.trim()){
  document.documentElement.style.setProperty("--title-bg", `url("${TITLE_BG_URL}")`);
  titleScreen.classList.add("hasImage");
}

function fitStage(){
  const scale = Math.min(window.innerWidth / BASE_W, window.innerHeight / BASE_H);
  stage.style.transform = `translate(-50%, -50%) scale(${scale})`;
}
window.addEventListener("resize", fitStage);
fitStage();

/* BGM */

let menuBgm = null;
let bgmStarted = false;
let bgmMuted = false;

function setupBgm(){
  if(!BGM_URL) return;
  menuBgm = new Audio(BGM_URL);
  menuBgm.loop = true;
  menuBgm.volume = 0.42;
  menuBgm.preload = "auto";
}

function startBgm(){
  if(!menuBgm || bgmStarted) return;

  bgmStarted = true;
  menuBgm.currentTime = 0;

  const promise = menuBgm.play();

  if(promise){
    promise.catch(() => {
      bgmStarted = false;
      soundBtn.textContent = "音量 OFF";
    });
  }
}

function toggleBgm(){
  if(!menuBgm) return;

  if(!bgmStarted){
    startBgm();
    bgmMuted = false;
    soundBtn.textContent = "音量 ON";
    return;
  }

  bgmMuted = !bgmMuted;
  menuBgm.muted = bgmMuted;
  soundBtn.textContent = bgmMuted ? "音量 OFF" : "音量 ON";
}

setupBgm();

soundBtn.addEventListener("click", (e) => {
  e.stopPropagation();
  toggleBgm();
});

/* screen transition */

function showScreen(target){
  document.querySelectorAll(".screen").forEach(s => s.classList.remove("active"));
  target.classList.add("active");
}

function showFade(callback){
  fade.classList.add("show");

  setTimeout(() => {
    callback();
    fade.classList.remove("show");
  }, 450);
}

titleScreen.addEventListener("click", (e) => {
  startBgm();

  const rect = stage.getBoundingClientRect();
  const x = (e.clientX - rect.left) / (rect.width / BASE_W);
  const y = (e.clientY - rect.top) / (rect.height / BASE_H);

  const ripple = document.createElement("div");
  ripple.className = "inkRipple";
  ripple.style.left = x + "px";
  ripple.style.top = y + "px";
  titleScreen.appendChild(ripple);

  setTimeout(() => {
    showFade(() => showScreen(loadingScreen));

    setTimeout(() => {
      showFade(() => showScreen(homeScreen));
    }, 1450);
  }, 520);

  setTimeout(() => ripple.remove(), 1000);
});

/* home interactions */

const quotes = [
  "……呼んでくれた？",
  "まだ、ここにいる",
  "灯は、まだ消えてない",
  "あなたが呼ぶなら……わたしは、ここにいられる"
];

let quoteIndex = 0;

hiyori.addEventListener("click", () => {
  hiyori.classList.add("active");

  quoteIndex = (quoteIndex + 1) % quotes.length;
  quote.textContent = quotes[quoteIndex];

  setTimeout(() => {
    hiyori.classList.remove("active");
  }, 650);
});

document.querySelectorAll(".navItem").forEach(item => {
  item.addEventListener("click", () => {
    document.querySelectorAll(".navItem").forEach(i => i.classList.remove("active"));
    item.classList.add("active");

    const menu = item.dataset.menu;

    if(menu === "ホーム") quote.textContent = "……呼んでくれた？";
    if(menu === "編成") quote.textContent = "みんなの灯も、守りたい";
    if(menu === "育成") quote.textContent = "強くなれたら……守れるかな";
    if(menu === "霊録") quote.textContent = "記憶は……少しずつ、戻るのかな";
    if(menu === "霊契") quote.textContent = "契りは、名前を呼ぶことから始まる";
  });
});

sortie.addEventListener("click", () => {
  quote.textContent = "物語を……綴りに行くんだね";
});
</script>

</body>
</html>
