# my-mbti

<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>MBTI로 포켓몬 찾기</title>
  <style>
    :root {
      --cream: #fff9e9;
      --yellow: #ffdf78;
      --yellow-dark: #f2bf42;
      --brown: #55432f;
      --muted: #88765e;
      --white: #fffef9;
      --pink: #ffe8dc;
      --green: #e8f1d8;
    }

    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      min-height: 100vh;
      padding: 28px 16px 48px;
      background:
        radial-gradient(circle at 10% 8%, #fff0bd 0, transparent 25%),
        radial-gradient(circle at 95% 70%, #fbe9c5 0, transparent 25%),
        var(--cream);
      color: var(--brown);
      font-family: "Malgun Gothic", "Apple SD Gothic Neo",
        "Noto Sans KR", sans-serif;
      font-size: 17px;
      line-height: 1.7;
    }

    button {
      font: inherit;
    }

    .app {
      width: 100%;
      max-width: 820px;
      margin: 0 auto;
    }

    .header {
      text-align: center;
      margin: 10px 0 28px;
    }

    .eyebrow {
      display: inline-block;
      padding: 5px 15px;
      border: 1px solid #f0d991;
      border-radius: 999px;
      background: #fff5d4;
      color: #88651d;
      font-size: 14px;
      font-weight: 800;
      letter-spacing: 1px;
    }

    h1 {
      margin: 13px 0 8px;
      font-size: clamp(30px, 6vw, 45px);
      line-height: 1.25;
      letter-spacing: -1.5px;
    }

    .subtitle {
      margin: 0;
      color: var(--muted);
      font-size: 17px;
    }

    .panel {
      padding: clamp(20px, 5vw, 34px);
      border: 2px solid #f2e3bd;
      border-radius: 28px;
      background: rgba(255, 254, 249, 0.94);
      box-shadow: 0 12px 32px rgba(116, 88, 39, 0.08);
    }

    .section-title {
      margin: 0 0 5px;
      font-size: 24px;
      letter-spacing: -0.5px;
    }

    .section-desc {
      margin: 0 0 22px;
      color: var(--muted);
      font-size: 15px;
    }

    .mbti-grid {
      display: grid;
      grid-template-columns: repeat(4, minmax(0, 1fr));
      gap: 10px;
    }

    .mbti-btn {
      min-height: 58px;
      padding: 10px 4px;
      border: 2px solid #f0e4c9;
      border-radius: 15px;
      background: #fffaf0;
      color: var(--brown);
      font-size: 18px;
      font-weight: 800;
      cursor: pointer;
      transition: transform 0.15s, background 0.15s,
        border-color 0.15s, box-shadow 0.15s;
    }

    .mbti-btn:hover {
      transform: translateY(-3px);
      border-color: var(--yellow-dark);
      background: #fff0bd;
      box-shadow: 0 5px 12px #c9a44c24;
    }

    .mbti-btn:focus-visible,
    .primary-btn:focus-visible,
    .secondary-btn:focus-visible {
      outline: 3px solid #bd8c20;
      outline-offset: 3px;
    }

    .hint {
      margin: 20px 0 0;
      text-align: center;
      color: var(--muted);
      font-size: 14px;
    }

    .result {
      display: none;
      animation: appear 0.35s ease-out;
    }

    .result.show {
      display: block;
    }

    .result-top {
      text-align: center;
      padding: 5px 0 23px;
    }

    .type-badge {
      display: inline-block;
      padding: 5px 15px;
      border-radius: 999px;
      background: #ffedb3;
      color: #795719;
      font-weight: 900;
      font-size: 15px;
    }

    .pokemon-emoji {
      display: flex;
      align-items: center;
      justify-content: center;
      width: 170px;
      height: 170px;
      max-width: 48vw;
      max-height: 48vw;
      margin: 18px auto 15px;
      border: 3px solid #f6df9f;
      border-radius: 50%;
      background: linear-gradient(145deg, #fff6d9, #ffedb4);
      font-size: clamp(78px, 16vw, 112px);
      box-shadow: inset 0 0 0 9px #fff9e8;
    }

    .pokemon-name {
      margin: 0;
      font-size: clamp(30px, 6vw, 40px);
      line-height: 1.3;
      letter-spacing: -1px;
    }

    .pokemon-tagline {
      margin: 8px 0 0;
      color: var(--muted);
      font-size: 16px;
    }

    .info-card {
      margin-top: 13px;
      padding: 20px 22px;
      border-radius: 20px;
    }

    .reason-card {
      background: #fff5d8;
      border: 1px solid #f3e2ac;
    }

    .match-card {
      background: var(--green);
      border: 1px solid #d5e4c1;
    }

    .card-title {
      margin: 0 0 8px;
      font-size: 19px;
      font-weight: 900;
    }

    .reason-text {
      margin: 0;
      white-space: pre-line;
      font-size: 16px;
      line-height: 1.9;
      word-break: keep-all;
    }

    .match-row {
      display: flex;
      align-items: center;
      gap: 13px;
    }

    .match-emoji {
      display: flex;
      align-items: center;
      justify-content: center;
      flex: 0 0 53px;
      height: 53px;
      border-radius: 16px;
      background: #fffef8;
      font-size: 30px;
    }

    .match-type {
      font-size: 23px;
      font-weight: 900;
    }

    .match-desc {
      margin-top: 1px;
      color: #61734e;
      font-size: 14px;
    }

    .actions {
      display: flex;
      justify-content: center;
      margin-top: 25px;
    }

    .primary-btn,
    .secondary-btn {
      min-height: 54px;
      padding: 12px 25px;
      border-radius: 15px;
      font-size: 17px;
      font-weight: 900;
      cursor: pointer;
      transition: transform 0.15s, background 0.15s;
    }

    .primary-btn {
      width: 100%;
      border: 0;
      background: var(--yellow);
      color: #503b19;
    }

    .primary-btn:hover {
      background: #ffd45c;
      transform: translateY(-2px);
    }

    .secondary-btn {
      border: 2px solid #ead9b6;
      background: #fffaf0;
      color: var(--brown);
    }

    .secondary-btn:hover {
      background: #fff0c8;
    }

    .footer {
      margin: 22px 0 0;
      color: #9b896e;
      text-align: center;
      font-size: 13px;
    }

    .hidden {
      display: none !important;
    }

    @keyframes appear {
      from {
        opacity: 0;
        transform: translateY(10px);
      }
      to {
        opacity: 1;
        transform: translateY(0);
      }
    }

    @media (max-width: 480px) {
      body {
        padding: 17px 12px 30px;
      }

      .header {
        margin-bottom: 20px;
      }

      .mbti-grid {
        gap: 8px;
      }

      .mbti-btn {
        min-height: 53px;
        font-size: 16px;
        border-radius: 12px;
      }

      .panel {
        border-radius: 22px;
      }

      .info-card {
        padding: 17px;
      }
    }

    @media (prefers-reduced-motion: reduce) {
      *,
      *::before,
      *::after {
        animation-duration: 0.01ms !important;
        transition-duration: 0.01ms !important;
      }
    }
  </style>
</head>

<body>
  <main class="app">
    <header class="header">
      <span class="eyebrow">POKÉMON × MBTI</span>
      <h1>나와 닮은 포켓몬은? 🌼</h1>
      <p class="subtitle">
        내 MBTI를 고르고 운명의 포켓몬을 만나 보세요!
      </p>
    </header>

    <section class="panel" id="selection">
      <h2 class="section-title">✨ 내 MBTI를 선택해 주세요</h2>
      <p class="section-desc">
        16가지 유형 중 나의 성격 유형을 눌러 보세요.
      </p>

      <div class="mbti-grid" id="mbtiGrid" aria-label="MBTI 유형 선택">
        <button class="mbti-btn" data-type="INTJ">INTJ</button>
        <button class="mbti-btn" data-type="INTP">INTP</button>
        <button class="mbti-btn" data-type="ENTJ">ENTJ</button>
        <button class="mbti-btn" data-type="ENTP">ENTP</button>
        <button class="mbti-btn" data-type="INFJ">INFJ</button>
        <button class="mbti-btn" data-type="INFP">INFP</button>
        <button class="mbti-btn" data-type="ENFJ">ENFJ</button>
        <button class="mbti-btn" data-type="ENFP">ENFP</button>
        <button class="mbti-btn" data-type="ISTJ">ISTJ</button>
        <button class="mbti-btn" data-type="ISFJ">ISFJ</button>
        <button class="mbti-btn" data-type="ESTJ">ESTJ</button>
        <button class="mbti-btn" data-type="ESFJ">ESFJ</button>
        <button class="mbti-btn" data-type="ISTP">ISTP</button>
        <button class="mbti-btn" data-type="ISFP">ISFP</button>
        <button class="mbti-btn" data-type="ESTP">ESTP</button>
        <button class="mbti-btn" data-type="ESFP">ESFP</button>
      </div>

      <p class="hint">💛 정답은 없어요. 재미로 즐겨 주세요!</p>
    </section>

    <section class="panel result" id="result" aria-live="polite">
      <div class="result-top">
        <span class="type-badge" id="typeBadge">나의 MBTI</span>
        <div class="pokemon-image-wrap">
          <img
            class="pokemon-image"
            id="pokemonImage"
            src="https://img.pokemondb.net/artwork/large/gardevoir.jpg"
            alt="가디안 공식 일러스트"
          >
        </div>
        <h2 class="pokemon-name" id="pokemonName">피카츄</h2>
        <p class="pokemon-tagline" id="pokemonTagline">
          나와 꼭 닮은 특별한 파트너!
        </p>
      </div>

      <article class="info-card reason-card">
        <h3 class="card-title">💛 왜 나와 닮았을까?</h3>
        <p class="reason-text" id="pokemonReason"></p>
      </article>

      <article class="info-card match-card">
        <h3 class="card-title">🍀 잘 맞는 MBTI</h3>
        <div class="match-row">
          <div class="match-emoji" id="matchEmoji" aria-hidden="true">🌿</div>
          <div>
            <div class="match-type" id="matchType">INFJ</div>
            <div class="match-desc" id="matchDesc">
              서로의 다른 매력을 발견하는 조합!
            </div>
          </div>
        </div>
      </article>

      <div class="actions">
        <button class="secondary-btn" id="resetBtn">
          ↩ 다시 고르기
        </button>
      </div>
    </section>

    <footer class="footer">
      포켓몬과 MBTI의 성격 연결은 재미를 위한 창작 해석입니다. 🌷
    </footer>
  </main>

  <script>
    const pokemonData = {
      INTJ: {
        name: "뮤츠",
        emoji: "🧠",
        tagline: "차분한 전략가 타입",
        reason:
          "깊이 생각하고 자신만의 목표를 향해 나아가는 모습이 닮았어요.\n" +
          "뛰어난 분석력과 독립적인 분위기가 뮤츠를 떠올리게 해요.",
        match: "ENFP",
        matchEmoji: "🦊",
        matchDesc: "새로운 관점과 신선한 활력을 더해 주는 조합!"
      },
      INTP: {
        name: "메타몽",
        emoji: "🟣",
        tagline: "호기심 가득한 탐구자 타입",
        reason:
          "무엇이든 궁금해하고 자유롭게 가능성을 탐색하는 모습이 닮았어요.\n" +
          "틀에 얽매이지 않는 유연한 사고가 매력 포인트예요.",
        match: "ENTJ",
        matchEmoji: "👑",
        matchDesc: "아이디어를 멋진 계획으로 발전시키는 조합!"
      },
      ENTJ: {
        name: "리자몽",
        emoji: "🐉",
        tagline: "목표를 향해 돌진하는 리더 타입",
        reason:
          "큰 목표를 세우고 어려움에도 당당히 도전하는 모습이 닮았어요.\n" +
          "강한 추진력과 자신감으로 주변을 이끄는 타입이에요.",
        match: "INTP",
        matchEmoji: "🟣",
        matchDesc: "실행력과 창의적인 아이디어가 만나는 조합!"
      },
      ENTP: {
        name: "겐가",
        emoji: "👻",
        tagline: "재치 넘치는 아이디어 뱅크",
        reason:
          "장난기와 재치로 분위기를 바꾸고 새로운 시도를 즐기는 모습이 닮았어요.\n" +
          "남들이 생각하지 못한 방법을 찾아내는 데 능숙해요.",
        match: "INFJ",
        matchEmoji: "🌙",
        matchDesc: "톡톡 튀는 발상과 깊은 통찰이 만나는 조합!"
      },
      INFJ: {
        name: "루카리오",
        emoji: "🐺",
        tagline: "마음을 읽는 조용한 수호자",
        reason:
          "상대의 감정을 세심하게 살피고 소중한 가치를 지키려는 모습이 닮았어요.\n" +
          "조용하지만 깊은 신념과 따뜻한 배려를 가진 타입이에요.",
        match: "ENTP",
        matchEmoji: "👻",
        matchDesc: "서로 다른 시선으로 생각의 폭을 넓혀 주는 조합!"
      },
      INFP: {
        name: "이브이",
        emoji: "🦊",
        tagline: "가능성이 반짝이는 감성파",
        reason:
          "자신만의 세계와 소중한 가치관을 간직하는 모습이 닮았어요.\n" +
          "풍부한 상상력과 무한한 가능성이 이브이의 매력과 잘 어울려요.",
        match: "ENFJ",
        matchEmoji: "🦁",
        matchDesc: "따뜻한 응원으로 서로의 꿈을 키우는 조합!"
      },
      ENFJ: {
        name: "가디안",
        emoji: "✨",
        tagline: "마음을 따뜻하게 지켜 주는 리더",
        reason:
          "주변 사람들을 응원하고 소중한 사람을 지키려는 모습이 닮았어요.\n" +
          "공감 능력과 따뜻한 리더십으로 모두에게 힘이 되어 줘요.",
        match: "INFP",
        matchEmoji: "🦊",
        matchDesc: "따뜻한 배려와 섬세한 감성이 만나는 조합!"
      },
      ENFP: {
        name: "피카츄",
        emoji: "⚡",
        tagline: "어디서든 빛나는 에너지 메이커",
        reason:
          "새로운 만남과 모험을 좋아하고 주변에 활기를 불어넣는 모습이 닮았어요.\n" +
          "호기심과 긍정적인 에너지로 일상에 즐거움을 더해 줘요.",
        match: "INTJ",
        matchEmoji: "🧠",
        matchDesc: "상상력과 전략이 만나 멋진 가능성을 만드는 조합!"
      },
      ISTJ: {
        name: "잠만보",
        emoji: "😴",
        tagline: "믿음직하고 든든한 현실파",
        reason:
          "자신의 페이스를 지키며 맡은 일을 꾸준히 해내는 모습이 닮았어요.\n" +
          "안정감과 책임감이 강하고 믿고 의지할 수 있는 타입이에요.",
        match: "ESFP",
        matchEmoji: "🎉",
        matchDesc: "안정적인 일상에 즐거운 활력을 더하는 조합!"
      },
      ISFJ: {
        name: "해피너스",
        emoji: "🥚",
        tagline: "다정함으로 마음을 돌보는 수호자",
        reason:
          "다른 사람의 필요를 알아차리고 조용히 챙겨 주는 모습이 닮았어요.\n" +
          "꾸준한 배려와 따뜻한 마음으로 주변을 편안하게 해 줘요.",
        match: "ESFP",
        matchEmoji: "🎉",
        matchDesc: "세심한 배려와 밝은 에너지가 어우러지는 조합!"
      },
      ESTJ: {
        name: "윈디",
        emoji: "🐕",
        tagline: "책임감 강한 든든한 대장",
        reason:
          "상황을 빠르게 정리하고 목표를 향해 확실하게 움직이는 모습이 닮았어요.\n" +
          "책임감과 실행력이 뛰어나 믿음직한 존재가 되어 줘요.",
        match: "ISFP",
        matchEmoji: "🎨",
        matchDesc: "계획성과 유연함이 서로의 부족한 부분을 채우는 조합!"
      },
      ESFJ: {
        name: "푸린",
        emoji: "🎤",
        tagline: "모두를 웃게 하는 분위기 메이커",
        reason:
          "사람들과 어울리기를 좋아하고 주변의 기분을 살피는 모습이 닮았어요.\n" +
          "다정한 표현과 친근한 에너지로 모임에 온기를 더해 줘요.",
        match: "ISFP",
        matchEmoji: "🎨",
        matchDesc: "함께하는 즐거움과 섬세한 감성이 만나는 조합!"
      },
      ISTP: {
        name: "메타그로스",
        emoji: "🤖",
        tagline: "침착하고 실용적인 해결사",
        reason:
          "복잡한 상황에서도 침착하게 원인을 찾고 해결하는 모습이 닮았어요.\n" +
          "논리적인 판단과 실용적인 기술로 문제를 풀어 나가요.",
        match: "ESFJ",
        matchEmoji: "🎤",
        matchDesc: "차분한 문제 해결력에 따뜻한 소통을 더하는 조합!"
      },
      ISFP: {
        name: "이상해씨",
        emoji: "🌱",
        tagline: "부드럽고 자기만의 색이 있는 타입",
        reason:
          "자연스러운 분위기와 자신만의 감성을 소중히 여기는 모습이 닮았어요.\n" +
          "다정하고 유연하며, 가까운 사람에게 진심을 다하는 타입이에요.",
        match: "ESTJ",
        matchEmoji: "🐕",
        matchDesc: "자유로운 감성과 든든한 추진력이 만나는 조합!"
      },
      ESTP: {
        name: "갸라도스",
        emoji: "🐲",
        tagline: "망설임 없이 뛰어드는 모험가",
        reason:
          "생생한 경험을 즐기고 기회가 오면 과감하게 도전하는 모습이 닮았어요.\n" +
          "순발력과 대담함으로 예상치 못한 상황에서도 활약해요.",
        match: "ISFJ",
        matchEmoji: "🥚",
        matchDesc: "대담한 모험에 편안함과 세심함을 더하는 조합!"
      },
      ESFP: {
        name: "루차불",
        emoji: "🎭",
        tagline: "무대를 빛내는 열정적인 스타",
        reason:
          "지금 이 순간을 즐기고 사람들과 신나게 어울리는 모습이 닮았어요.\n" +
          "넘치는 표현력과 자신감으로 주변까지 즐겁게 만들어 줘요.",
        match: "ISTJ",
        matchEmoji: "📘",
        matchDesc: "즉흥적인 즐거움과 든든한 안정감이 만나는 조합!"
      }
    };

    const selection = document.getElementById("selection");
    const result = document.getElementById("result");

    const typeBadge = document.getElementById("typeBadge");
    const pokemonEmoji = document.getElementById("pokemonEmoji");
    const pokemonName = document.getElementById("pokemonName");
    const pokemonTagline = document.getElementById("pokemonTagline");
    const pokemonReason = document.getElementById("pokemonReason");
    const matchEmoji = document.getElementById("matchEmoji");
    const matchType = document.getElementById("matchType");
    const matchDesc = document.getElementById("matchDesc");
    const resetBtn = document.getElementById("resetBtn");

    function selectMBTI(type) {
      const data = pokemonData[type];

      if (!data) return;

      typeBadge.textContent = "나의 MBTI · " + type;
      pokemonEmoji.textContent = data.emoji;
      pokemonEmoji.setAttribute("aria-label", data.name);
      pokemonName.textContent = data.name;
      pokemonTagline.textContent = data.tagline;
      pokemonReason.textContent = data.reason;
      matchEmoji.textContent = data.matchEmoji;
      matchType.textContent = data.match;
      matchDesc.textContent = data.matchDesc;

      selection.classList.add("hidden");
      result.classList.remove("show");

      // 애니메이션을 다시 실행해 결과 화면을 보여 줍니다.
      void result.offsetWidth;
      result.classList.add("show");

      window.scrollTo({ top: 0, behavior: "smooth" });
    }

    document.getElementById("mbtiGrid").addEventListener("click", function(event) {
      const button = event.target.closest("button[data-type]");

      if (button) {
        selectMBTI(button.dataset.type);
      }
    });

    resetBtn.addEventListener("click", function() {
      result.classList.remove("show");
      selection.classList.remove("hidden");

      window.scrollTo({ top: 0, behavior: "smooth" });
      document.querySelector(".section-title").focus?.();
    });
  </script>
</body>
</html>
