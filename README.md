#my-mbti

<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>MBTI로 포켓몬 찾기 🌼</title>
<style>
:root {
  --cream:#fff9e9; --yellow:#ffdf78; --brown:#55432f;
  --muted:#88765e; --white:#fffef9;
}
* { box-sizing:border-box; }
body {
  margin:0; padding:26px 15px 40px; min-height:100vh;
  background:var(--cream); color:var(--brown);
  font-family:"Malgun Gothic","Apple SD Gothic Neo",sans-serif;
  font-size:17px; line-height:1.7;
}
.app { max-width:760px; margin:auto; }
header { text-align:center; margin:8px 0 26px; }
.eyebrow {
  display:inline-block; background:#ffedb3; border-radius:99px;
  padding:5px 15px; font-size:14px; font-weight:bold;
}
h1 { font-size:clamp(30px,6vw,43px); margin:12px 0 4px; }
.subtitle { color:var(--muted); margin:0; }
.panel {
  background:var(--white); border:2px solid #f2e3bd;
  border-radius:25px; padding:clamp(20px,5vw,32px);
  box-shadow:0 10px 28px #74582710;
}
h2 { margin:0 0 5px; font-size:24px; }
.description { color:var(--muted); font-size:15px; margin:0 0 20px; }
.grid { display:grid; grid-template-columns:repeat(4,1fr); gap:10px; }
.mbti {
  padding:12px 3px; border:2px solid #f0e4c9; border-radius:13px;
  background:#fffaf0; color:var(--brown); font-size:17px;
  font-weight:bold; cursor:pointer;
}
.mbti:hover,.mbti:focus-visible { background:#fff0bd; border-color:#e6bd50; }
.hint { text-align:center; color:var(--muted); font-size:14px; margin:20px 0 0; }
.hidden { display:none!important; }
.result { display:none; }
.result.show { display:block; animation:appear .3s ease-out; }
.center { text-align:center; }
.type {
  display:inline-block; padding:5px 15px; border-radius:99px;
  background:#ffedb3; font-weight:bold;
}
.art {
  width:200px; height:200px; max-width:60vw; max-height:60vw;
  margin:18px auto 14px; border:3px solid #f6df9f; border-radius:50%;
  background:linear-gradient(145deg,#fff6d9,#ffedb4);
  box-shadow:inset 0 0 0 8px #fff9e8;
  display:flex; align-items:center; justify-content:center; overflow:hidden;
}
.art img { width:100%; height:100%; object-fit:contain; padding:9px; }
.art .fallback { font-size:80px; display:none; }
.name { font-size:36px; line-height:1.3; margin:0; }
.tagline { color:var(--muted); margin:7px 0 20px; }
.info { margin-top:14px; padding:19px 21px; border-radius:18px; }
.reason { background:#fff5d8; border:1px solid #f3e2ac; }
.match { background:#e8f1d8; border:1px solid #d5e4c1; }
.info h3 { margin:0 0 8px; font-size:19px; }
.reason-text { white-space:pre-line; margin:0; line-height:1.9; }
.match-row { display:flex; align-items:center; gap:13px; }
.match-icon {
  display:flex; align-items:center; justify-content:center; flex:0 0 52px;
  height:52px; border-radius:15px; background:white; font-size:29px;
}
.match-type { font-size:23px; font-weight:bold; }
.match-desc { color:#61734e; font-size:14px; }
.actions { display:flex; justify-content:center; margin-top:23px; }
button.secondary {
  border:2px solid #ead9b6; background:#fffaf0; color:var(--brown);
  border-radius:14px; padding:12px 24px; font-size:17px;
  font-weight:bold; cursor:pointer;
}
button.secondary:hover { background:#fff0c8; }
footer { text-align:center; color:#9b896e; font-size:13px; margin-top:22px; }
@keyframes appear {
  from { opacity:0; transform:translateY(8px); }
  to { opacity:1; transform:translateY(0); }
}
@media(max-width:420px) {
  body { padding:18px 12px 30px; }
  .grid { gap:7px; }
  .mbti { font-size:15px; padding:10px 2px; }
  .info { padding:16px; }
}
</style>
</head>
<body>
<main class="app">
<header>
  <span class="eyebrow">POKÉMON × MBTI</span>
  <h1>나와 닮은 포켓몬은? 🌼</h1>
  <p class="subtitle">MBTI를 고르고 운명의 포켓몬을 만나 보세요!</p>
</header>

<section class="panel" id="selection">
  <h2>✨ 내 MBTI를 선택해 주세요</h2>
  <p class="description">16가지 유형 중 하나를 눌러 보세요.</p>
  <div class="grid" id="mbtiGrid">
    <button class="mbti" data-type="INTJ">INTJ</button>
    <button class="mbti" data-type="INTP">INTP</button>
    <button class="mbti" data-type="ENTJ">ENTJ</button>
    <button class="mbti" data-type="ENTP">ENTP</button>
    <button class="mbti" data-type="INFJ">INFJ</button>
    <button class="mbti" data-type="INFP">INFP</button>
    <button class="mbti" data-type="ENFJ">ENFJ</button>
    <button class="mbti" data-type="ENFP">ENFP</button>
    <button class="mbti" data-type="ISTJ">ISTJ</button>
    <button class="mbti" data-type="ISFJ">ISFJ</button>
    <button class="mbti" data-type="ESTJ">ESTJ</button>
    <button class="mbti" data-type="ESFJ">ESFJ</button>
    <button class="mbti" data-type="ISTP">ISTP</button>
    <button class="mbti" data-type="ISFP">ISFP</button>
    <button class="mbti" data-type="ESTP">ESTP</button>
    <button class="mbti" data-type="ESFP">ESFP</button>
  </div>
  <p class="hint">💛 정답은 없어요. 재미로 즐겨 주세요!</p>
</section>

<section class="panel result" id="result" aria-live="polite">
  <div class="center">
    <span class="type" id="typeBadge"></span>
    <div class="art">
      <img id="pokemonImage" src="" alt="">
      <span class="fallback" id="fallback" aria-hidden="true">🌟</span>
    </div>
    <h2 class="name" id="pokemonName"></h2>
    <p class="tagline" id="tagline"></p>
  </div>
  <article class="info reason">
    <h3>💛 왜 나와 닮았을까?</h3>
    <p class="reason-text" id="reason"></p>
  </article>
  <article class="info match">
    <h3>🍀 잘 맞는 MBTI</h3>
    <div class="match-row">
      <div class="match-icon" id="matchEmoji"></div>
      <div>
        <div class="match-type" id="matchType"></div>
        <div class="match-desc" id="matchDesc"></div>
      </div>
    </div>
  </article>
  <div class="actions">
    <button class="secondary" id="resetBtn">↩ 다시 고르기</button>
  </div>
</section>
<footer>포켓몬 이미지의 저작권은 해당 권리자에게 있습니다. 성격 연결은 재미를 위한 창작 해석입니다. 🌷</footer>
</main>

<script>
/*
  이미지 주소는 Pokémon Database의 공식 아트워크 파일을 사용합니다.
  이미지가 보이지 않는다면 인터넷 연결 또는 이미지 서버를 확인하세요.
*/
const pokemon = {
 INTJ:{name:"뮤츠",id:150,emoji:"🧠",tag:"차분한 전략가 타입",reason:"깊이 생각하고 자신만의 목표를 향해 나아가는 모습이 닮았어요.\n뛰어난 분석력과 독립적인 분위기가 뮤츠를 떠올리게 해요.",match:"ENFP",matchEmoji:"⚡",matchDesc:"새로운 관점과 신선한 활력을 더해 주는 조합!"},
 INTP:{name:"메타몽",id:132,emoji:"🟣",tag:"호기심 가득한 탐구자 타입",reason:"무엇이든 궁금해하고 자유롭게 가능성을 탐색하는 모습이 닮았어요.\n틀에 얽매이지 않는 유연한 사고가 매력 포인트예요.",match:"ENTJ",matchEmoji:"👑",matchDesc:"아이디어를 멋진 계획으로 발전시키는 조합!"},
 ENTJ:{name:"리자몽",id:6,emoji:"🐉",tag:"목표를 향해 돌진하는 리더 타입",reason:"큰 목표를 세우고 어려움에도 당당히 도전하는 모습이 닮았어요.\n강한 추진력과 자신감으로 주변을 이끄는 타입이에요.",match:"INTP",matchEmoji:"🟣",matchDesc:"실행력과 창의적인 아이디어가 만나는 조합!"},
 ENTP:{name:"팬텀",id:94,emoji:"👻",tag:"재치 넘치는 아이디어 뱅크",reason:"장난기와 재치로 분위기를 바꾸고 새로운 시도를 즐기는 모습이 닮았어요.\n남들이 생각하지 못한 방법을 찾아내는 데 능숙해요.",match:"INFJ",matchEmoji:"🌙",matchDesc:"톡톡 튀는 발상과 깊은 통찰이 만나는 조합!"},
 INFJ:{name:"루카리오",id:448,emoji:"🐺",tag:"마음을 읽는 조용한 수호자",reason:"상대의 감정을 세심하게 살피고 소중한 가치를 지키려는 모습이 닮았어요.\n조용하지만 깊은 신념과 따뜻한 배려를 가진 타입이에요.",match:"ENTP",matchEmoji:"👻",matchDesc:"서로 다른 시선으로 생각의 폭을 넓혀 주는 조합!"},
 INFP:{name:"이브이",id:133,emoji:"🦊",tag:"가능성이 반짝이는 감성파",reason:"자신만의 세계와 소중한 가치관을 간직하는 모습이 닮았어요.\n풍부한 상상력과 무한한 가능성이 이브이의 매력과 잘 어울려요.",match:"ENFJ",matchEmoji:"✨",matchDesc:"따뜻한 응원으로 서로의 꿈을 키우는 조합!"},
 ENFJ:{name:"가디안",id:282,emoji:"✨",tag:"마음을 따뜻하게 지켜 주는 리더",reason:"주변 사람들을 응원하고 소중한 사람을 지키려는 모습이 닮았어요.\n공감 능력과 따뜻한 리더십으로 모두에게 힘이 되어 줘요.",match:"INFP",matchEmoji:"🦊",matchDesc:"따뜻한 배려와 섬세한 감성이 만나는 조합!"},
 ENFP:{name:"피카츄",id:25,emoji:"⚡",tag:"어디서든 빛나는 에너지 메이커",reason:"새로운 만남과 모험을 좋아하고 주변에 활기를 불어넣는 모습이 닮았어요.\n호기심과 긍정적인 에너지로 일상에 즐거움을 더해 줘요.",match:"INTJ",matchEmoji:"🧠",matchDesc:"상상력과 전략이 만나 멋진 가능성을 만드는 조합!"},
 ISTJ:{name:"잠만보",id:143,emoji:"😴",tag:"믿음직하고 든든한 현실파",reason:"자신의 페이스를 지키며 맡은 일을 꾸준히 해내는 모습이 닮았어요.\n안정감과 책임감이 강하고 믿고 의지할 수 있는 타입이에요.",match:"ESFP",matchEmoji:"🎉",matchDesc:"안정적인 일상에 즐거운 활력을 더하는 조합!"},
 ISFJ:{name:"해피너스",id:242,emoji:"🥚",tag:"다정함으로 마음을 돌보는 수호자",reason:"다른 사람의 필요를 알아차리고 조용히 챙겨 주는 모습이 닮았어요.\n꾸준한 배려와 따뜻한 마음으로 주변을 편안하게 해 줘요.",match:"ESFP",matchEmoji:"🎉",matchDesc:"세심한 배려와 밝은 에너지가 어우러지는 조합!"},
 ESTJ:{name:"윈디",id:59,emoji:"🐕",tag:"책임감 강한 든든한 대장",reason:"상황을 빠르게 정리하고 목표를 향해 확실하게 움직이는 모습이 닮았어요.\n책임감과 실행력이 뛰어나 믿음직한 존재가 되어 줘요.",match:"ISFP",matchEmoji:"🎨",matchDesc:"계획성과 유연함이 서로의 부족한 부분을 채우는 조합!"},
 ESFJ:{name:"푸린",id:39,emoji:"🎤",tag:"모두를 웃게 하는 분위기 메이커",reason:"사람들과 어울리기를 좋아하고 주변의 기분을 살피는 모습이 닮았어요.\n다정한 표현과 친근한 에너지로 모임에 온기를 더해 줘요.",match:"ISFP",matchEmoji:"🎨",matchDesc:"함께하는 즐거움과 섬세한 감성이 만나는 조합!"},
 ISTP:{name:"메타그로스",id:376,emoji:"🤖",tag:"침착하고 실용적인 해결사",reason:"복잡한 상황에서도 침착하게 원인을 찾고 해결하는 모습이 닮았어요.\n논리적인 판단과 실용적인 기술로 문제를 풀어 나가요.",match:"ESFJ",matchEmoji:"🎤",matchDesc:"차분한 문제 해결력에 따뜻한 소통을 더하는 조합!"},
 ISFP:{name:"이상해씨",id:1,emoji:"🌱",tag:"부드럽고 자기만의 색이 있는 타입",reason:"자연스러운 분위기와 자신만의 감성을 소중히 여기는 모습이 닮았어요.\n다정하고 유연하며, 가까운 사람에게 진심을 다하는 타입이에요.",match:"ESTJ",matchEmoji:"🐕",matchDesc:"자유로운 감성과 든든한 추진력이 만나는 조합!"},
 ESTP:{name:"갸라도스",id:130,emoji:"🐲",tag:"망설임 없이 뛰어드는 모험가",reason:"생생한 경험을 즐기고 기회가 오면 과감하게 도전하는 모습이 닮았어요.\n순발력과 대담함으로 예상치 못한 상황에서도 활약해요.",match:"ISFJ",matchEmoji:"🥚",matchDesc:"대담한 모험에 편안함과 세심함을 더하는 조합!"},
 ESFP:{name:"루차불",id:701,emoji:"🎭",tag:"무대를 빛내는 열정적인 스타",reason:"지금 이 순간을 즐기고 사람들과 신나게 어울리는 모습이 닮았어요.\n넘치는 표현력과 자신감으로 주변까지 즐겁게 만들어 줘요.",match:"ISTJ",matchEmoji:"📘",matchDesc:"즉흥적인 즐거움과 든든한 안정감이 만나는 조합!"}
};

const selection = document.getElementById("selection");
const result = document.getElementById("result");
const img = document.getElementById("pokemonImage");
const fallback = document.getElementById("fallback");

function selectMBTI(type) {
  const p = pokemon[type];
  if (!p) return;

  document.getElementById("typeBadge").textContent = "나의 MBTI · " + type;
  document.getElementById("pokemonName").textContent = p.name;
  document.getElementById("tagline").textContent = p.tag;
  document.getElementById("reason").textContent = p.reason;
  document.getElementById("matchEmoji").textContent = p.matchEmoji;
  document.getElementById("matchType").textContent = p.match;
  document.getElementById("matchDesc").textContent = p.matchDesc;

  // Pokémon Database의 공식 아트워크 파일 경로
  img.style.display = "block";
  fallback.style.display = "none";
  img.alt = p.name + " 공식 아트워크";
  img.onerror = function() {
    img.style.display = "none";
    fallback.textContent = p.emoji;
    fallback.style.display = "block";
  };
  img.src = "https://img.pokemondb.net/artwork/large/" + ({
    6:"charizard", 25:"pikachu", 39:"jigglypuff",
    59:"arcanine", 94:"gengar", 130:"gyarados",
    132:"ditto", 133:"eevee", 143:"snorlax",
    150:"mewtwo", 242:"blissey", 282:"gardevoir",
    376:"metagross", 448:"lucario", 701:"hawlucha",
    1:"bulbasaur"
  }[p.id] || p.name.toLowerCase()) + ".jpg";

  selection.classList.add("hidden");
  result.classList.remove("show");
  void result.offsetWidth;
  result.classList.add("show");
  window.scrollTo({top:0,behavior:"smooth"});
}

document.getElementById("mbtiGrid").addEventListener("click", event => {
  const button = event.target.closest("button[data-type]");
  if (button) selectMBTI(button.dataset.type);
});

document.getElementById("resetBtn").addEventListener("click", () => {
  result.classList.remove("show");
  selection.classList.remove("hidden");
  window.scrollTo({top:0,behavior:"smooth"});
});
</script>
</body>
</html>
