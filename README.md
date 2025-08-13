<!doctype html>
<html lang="ja">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Instagram ID / PASS</title>
  <style>
    :root{
      --bg:#0f172a;
      --card:#111827;
      --text:#e5e7eb;
      --muted:#94a3b8;
      --accent:#22c55e;
      --danger:#ef4444;
    }
    html,body{height:100%;}
    body{
      margin:0; background:linear-gradient(180deg,#0b1220,#0f172a 30%,#0b1220);
      color:var(--text); font-family: system-ui, -apple-system, Segoe UI, Roboto, "Helvetica Neue", Inter, Arial, "Noto Sans JP", sans-serif;
      display:grid; place-items:center;
    }
    .wrap{ width:min(680px,92vw); padding:24px; }
    .card{
      background:rgba(17,24,39,.8); backdrop-filter: blur(8px);
      border-radius:20px; padding:28px; box-shadow: 0 10px 30px rgba(0,0,0,.35);
      border:1px solid rgba(255,255,255,.05);
    }
    h1{font-size:clamp(22px,3.2vw,28px); margin:0 0 8px}
    p{margin:0 0 18px; color:var(--muted)}
    .row{display:flex; gap:10px; align-items:center; margin:12px 0}
    .label{min-width:86px; opacity:.8}
    .secret{filter: blur(12px); transition: filter .25s ease, opacity .25s ease; user-select: none;}
    .secret.revealed{filter:none}
    .btns{display:flex; gap:10px; flex-wrap:wrap; margin-top:18px}
    button{
      appearance:none; border:1px solid rgba(255,255,255,.12); color:var(--text);
      background:transparent; padding:10px 14px; border-radius:12px; cursor:pointer; font-weight:600
    }
    .primary{ border-color:rgba(34,197,94,.6)}
    .danger{ border-color:rgba(239,68,68,.6)}
    .copy-tip{font-size:12px; color:var(--muted); margin-top:6px}
    .idpass{word-break: break-all; font-family: ui-monospace, SFMono-Regular, Menlo, Consolas, monospace;}
    .footer{margin-top:20px; font-size:12px; color:var(--muted)}
  </style>
</head>
<body>
  <div class="wrap">
    <div class="card">
      <h1>InstagramのIDとパスワード</h1>
      <p>下の「表示する」を押すと内容が見えます。必要が終わったら、非表示に戻すかパスワードを変更してください。</p>

      <div class="row">
        <div class="label">ID</div>
        <div id="idText" class="idpass secret">ka1013_</div>
        <button data-copy-target="#idText">コピー</button>
      </div>

      <div class="row">
        <div class="label">PASS</div>
        <div id="passText" class="idpass secret">kaay1013</div>
        <button data-copy-target="#passText">コピー</button>
      </div>

      <div class="btns">
        <button id="revealBtn" class="primary">表示する</button>
        <button id="hideBtn">非表示にする</button>
        <button id="changeBtn" class="danger">パスワードを変更する手順</button>
      </div>

      <div class="copy-tip">安全のため、共有後は2段階認証の有効化やパスワード変更をおすすめします。</div>

      <div class="footer">© あなたの名前 — このページのURLをQRコードにしてください（リンク期限なしの静的ホスティングでOK）</div>
    </div>
  </div>

  <script>
    const $ = s => document.querySelector(s);
    const idText = $('#idText');
    const passText = $('#passText');
    const revealBtn = $('#revealBtn');
    const hideBtn = $('#hideBtn');
    const changeBtn = $('#changeBtn');

    function reveal(){ idText.classList.add('revealed'); passText.classList.add('revealed'); }
    function hide(){ idText.classList.remove('revealed'); passText.classList.remove('revealed'); }

    revealBtn.addEventListener('click', reveal);
    hideBtn.addEventListener('click', hide);

    document.querySelectorAll('button[data-copy-target]').forEach(btn => {
      btn.addEventListener('click', async () => {
        const target = document.querySelector(btn.getAttribute('data-copy-target'));
        try { await navigator.clipboard.writeText(target.textContent.trim());
          btn.textContent = 'コピーしました'; setTimeout(()=>btn.textContent='コピー', 1200);
        } catch(e){ alert('コピーに失敗しました'); }
      });
    });

    changeBtn.addEventListener('click', () => {
      alert('Instagramアプリ → 設定とアクティビティ → アカウントセンター → パスワードとセキュリティ → パスワードを変更');
    });
  </script>
</body>
</html>
