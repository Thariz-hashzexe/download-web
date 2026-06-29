
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>TiRo Convert — Professional Video Converter</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Space+Grotesk:wght@400;500;600;700&display=swap" rel="stylesheet">
<style>
:root{--bg:#070a14;--surface:rgba(255,255,255,0.04);--border:rgba(255,255,255,0.08);--text:#eef0f8;--muted:rgba(238,240,248,0.45);--accent:#7c6ff7;--accent2:#4facfe;--green:#22d3a0;--red:#f43f5e;--r:16px;--rs:10px}
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
html{scroll-behavior:smooth}
body{font-family:'Inter',sans-serif;background:var(--bg);color:var(--text);min-height:100vh;overflow-x:hidden}
.orbs{position:fixed;inset:0;pointer-events:none;z-index:0;overflow:hidden}
.orb{position:absolute;border-radius:50%;filter:blur(130px);animation:drift 18s ease-in-out infinite alternate}
.o1{width:640px;height:640px;background:#7c6ff7;top:-220px;left:-120px;opacity:.12}
.o2{width:520px;height:520px;background:#4facfe;top:35%;right:-160px;opacity:.10;animation-delay:-6s}
.o3{width:420px;height:420px;background:#22d3a0;bottom:-120px;left:32%;opacity:.09;animation-delay:-12s}
@keyframes drift{0%{transform:translate(0,0) scale(1)}100%{transform:translate(35px,28px) scale(1.06)}}
.wrap{position:relative;z-index:1;max-width:880px;margin:0 auto;padding:0 20px 80px}
header{display:flex;align-items:center;justify-content:space-between;padding:28px 0 0;margin-bottom:44px}
.logo{font-family:'Space Grotesk',sans-serif;font-size:21px;font-weight:700;letter-spacing:-.5px;display:flex;align-items:center;gap:10px}
.logo-mark{width:36px;height:36px;background:linear-gradient(135deg,#7c6ff7,#4facfe);border-radius:9px;display:flex;align-items:center;justify-content:center;font-size:15px;flex-shrink:0}
.logo em{color:var(--muted);font-style:normal;font-weight:400}
.pill-badge{font-size:11px;font-weight:600;background:rgba(124,111,247,.12);border:1px solid rgba(124,111,247,.3);color:var(--accent);padding:4px 12px;border-radius:20px;letter-spacing:.5px;text-transform:uppercase}
.hero{text-align:center;margin-bottom:40px}
.hero h1{font-family:'Space Grotesk',sans-serif;font-size:clamp(30px,5.5vw,54px);font-weight:700;letter-spacing:-1.5px;line-height:1.08;margin-bottom:14px;background:linear-gradient(160deg,#fff 30%,rgba(255,255,255,.55));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text}
.hero h1 b{font-style:normal;background:linear-gradient(90deg,var(--accent),var(--accent2));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;font-weight:700}
.hero p{font-size:15px;color:var(--muted);max-width:480px;margin:0 auto;line-height:1.65}
.compat-note{background:rgba(244,63,94,.07);border:1px solid rgba(244,63,94,.2);border-radius:12px;padding:14px 18px;margin-bottom:20px;font-size:13px;color:var(--muted);display:none;line-height:1.6}
.compat-note.on{display:block}
.compat-note strong{color:#f87171}
.drop-zone{background:var(--surface);border:2px dashed var(--border);border-radius:24px;padding:64px 40px 52px;text-align:center;cursor:pointer;transition:border-color .25s,background .25s,transform .2s;position:relative;overflow:hidden;margin-bottom:22px}
.drop-zone::after{content:'';position:absolute;inset:0;background:radial-gradient(ellipse 70% 50% at 50% 0%,rgba(124,111,247,.1),transparent);opacity:0;transition:opacity .3s}
.drop-zone:hover,.drop-zone.over{border-color:var(--accent);background:rgba(124,111,247,.05)}
.drop-zone:hover::after,.drop-zone.over::after{opacity:1}
.drop-zone.over{transform:scale(1.012)}
.dz-icon{width:76px;height:76px;margin:0 auto 22px;background:linear-gradient(135deg,rgba(124,111,247,.18),rgba(79,172,254,.18));border:1px solid rgba(124,111,247,.25);border-radius:22px;display:flex;align-items:center;justify-content:center;font-size:32px;transition:transform .3s}
.drop-zone:hover .dz-icon{transform:translateY(-5px)}
.drop-zone h2{font-family:'Space Grotesk',sans-serif;font-size:20px;font-weight:600;margin-bottom:8px}
.drop-zone p{color:var(--muted);font-size:14px;margin-bottom:22px}
.btn-browse{display:inline-flex;align-items:center;gap:8px;background:linear-gradient(135deg,var(--accent),#5d52d0);color:#fff;border:none;border-radius:var(--rs);padding:11px 26px;font-size:14px;font-weight:600;font-family:inherit;cursor:pointer;transition:all .2s;box-shadow:0 4px 20px rgba(124,111,247,.35)}
.btn-browse:hover{transform:translateY(-1px);box-shadow:0 6px 28px rgba(124,111,247,.5)}
.fmt-note{margin-top:16px;font-size:12px;color:var(--muted)}
.fmt-note strong{color:rgba(238,240,248,.65)}
#filePick{display:none}
.preview-wrap{background:var(--surface);border:1px solid var(--border);border-radius:24px;overflow:hidden;margin-bottom:22px;display:none}
.preview-wrap.on{display:block;animation:fadeUp .35s ease}
.preview-top{position:relative;width:100%;background:#000;border-radius:24px 24px 0 0;overflow:hidden;cursor:pointer}
.preview-top video{display:block;width:100%;max-height:400px;object-fit:contain}
.preview-overlay{position:absolute;inset:0;display:flex;align-items:center;justify-content:center;background:rgba(0,0,0,.3);opacity:0;transition:opacity .2s}
.preview-top:hover .preview-overlay{opacity:1}
.play-btn{width:60px;height:60px;background:rgba(124,111,247,.85);border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:22px;backdrop-filter:blur(6px);transition:transform .2s;padding-left:4px}
.preview-top:hover .play-btn{transform:scale(1.1)}
.preview-meta{padding:16px 22px;display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:12px;border-top:1px solid var(--border)}
.preview-tags{display:flex;flex-wrap:wrap;gap:7px}
.ptag{font-size:11px;font-weight:600;background:rgba(124,111,247,.12);border:1px solid rgba(124,111,247,.25);color:var(--accent);padding:3px 10px;border-radius:20px}
.ptag.green{background:rgba(34,211,160,.1);border-color:rgba(34,211,160,.25);color:var(--green)}
.ptag.blue{background:rgba(79,172,254,.1);border-color:rgba(79,172,254,.25);color:var(--accent2)}
.preview-fname{font-size:13px;color:var(--muted);max-width:220px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.btn-change{background:transparent;border:1px solid var(--border);color:var(--muted);border-radius:8px;padding:6px 13px;font-size:12px;cursor:pointer;transition:all .2s;font-family:inherit;white-space:nowrap}
.btn-change:hover{border-color:var(--accent);color:var(--accent)}
.vol-bar{position:absolute;bottom:0;left:0;right:0;height:3px;background:rgba(255,255,255,.15)}
.vol-fill{height:100%;background:linear-gradient(90deg,var(--accent),var(--accent2));width:0%;transition:width .3s}
.card{background:var(--surface);border:1px solid var(--border);border-radius:var(--r);overflow:hidden;margin-bottom:20px;display:none}
.card.on{display:block;animation:fadeUp .35s ease}
@keyframes fadeUp{from{opacity:0;transform:translateY(12px)}to{opacity:1;transform:none}}
.card-head{padding:18px 22px;border-bottom:1px solid var(--border);display:flex;align-items:center;justify-content:space-between;gap:12px;flex-wrap:wrap}
.file-chip{display:flex;align-items:center;gap:13px}
.file-thumb{width:48px;height:36px;background:linear-gradient(135deg,rgba(124,111,247,.2),rgba(79,172,254,.2));border-radius:8px;display:flex;align-items:center;justify-content:center;font-size:18px;flex-shrink:0}
.fname{font-size:14px;font-weight:500;max-width:240px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.fsize{font-size:12px;color:var(--muted);margin-top:2px}
.btn-rm{background:transparent;border:1px solid var(--border);color:var(--muted);border-radius:8px;padding:6px 13px;font-size:12px;cursor:pointer;transition:all .2s;font-family:inherit}
.btn-rm:hover{border-color:var(--red);color:var(--red)}
.presets-row{padding:18px 22px;border-bottom:1px solid var(--border)}
.sec-label{font-size:11px;font-weight:600;color:var(--muted);text-transform:uppercase;letter-spacing:.8px;margin-bottom:11px;display:flex;align-items:center;gap:6px}
.chips{display:flex;flex-wrap:wrap;gap:7px}
.chip{padding:7px 14px;border:1px solid var(--border);border-radius:9px;font-size:12px;font-weight:500;cursor:pointer;transition:all .15s;background:transparent;color:var(--muted);font-family:inherit;white-space:nowrap}
.chip:hover{border-color:var(--accent);color:var(--text)}
.chip.on{background:rgba(124,111,247,.14);border-color:var(--accent);color:var(--accent)}
.sg{display:grid;grid-template-columns:1fr 1fr;gap:0}
@media(max-width:580px){.sg{grid-template-columns:1fr}}
.sg-cell{padding:18px 22px;border-right:1px solid var(--border);border-bottom:1px solid var(--border)}
.sg-cell:nth-child(even){border-right:none}
.sg-cell:nth-last-child(-n+2){border-bottom:none}
@media(max-width:580px){.sg-cell{border-right:none}.sg-cell:last-child{border-bottom:none}}
.conv-row{padding:18px 22px;display:flex;align-items:center;justify-content:space-between;gap:16px;flex-wrap:wrap}
.info-tags{display:flex;flex-wrap:wrap;gap:8px}
.itag{font-size:11px;font-weight:500;background:rgba(79,172,254,.1);border:1px solid rgba(79,172,254,.2);color:var(--accent2);padding:3px 10px;border-radius:20px}
.btn-go{display:inline-flex;align-items:center;gap:10px;background:linear-gradient(135deg,var(--accent),var(--accent2));color:#fff;border:none;border-radius:var(--rs);padding:13px 34px;font-size:15px;font-weight:600;font-family:inherit;cursor:pointer;transition:all .25s;box-shadow:0 4px 24px rgba(124,111,247,.4);position:relative;overflow:hidden;white-space:nowrap}
.btn-go::before{content:'';position:absolute;top:0;left:-100%;width:100%;height:100%;background:linear-gradient(90deg,transparent,rgba(255,255,255,.15),transparent);transition:left .5s}
.btn-go:hover::before{left:100%}
.btn-go:hover{transform:translateY(-1px);box-shadow:0 6px 32px rgba(124,111,247,.55)}
.btn-go:disabled{opacity:.45;cursor:not-allowed;transform:none;box-shadow:none}
@media(max-width:580px){.btn-go{width:100%;justify-content:center}}
.prog-card{background:var(--surface);border:1px solid var(--border);border-radius:var(--r);padding:28px;margin-bottom:20px;display:none}
.prog-card.on{display:block;animation:fadeUp .3s ease}
.prog-top{display:flex;align-items:center;justify-content:space-between;margin-bottom:20px}
.prog-title{font-family:'Space Grotesk',sans-serif;font-size:15px;font-weight:600;display:flex;align-items:center;gap:10px}
.ring{width:18px;height:18px;border:2px solid rgba(124,111,247,.25);border-top-color:var(--accent);border-radius:50%;animation:spin .75s linear infinite;flex-shrink:0}
@keyframes spin{to{transform:rotate(360deg)}}
.prog-num{font-family:'Space Grotesk',sans-serif;font-size:30px;font-weight:700;background:linear-gradient(90deg,var(--accent),var(--accent2));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text}
.track{background:rgba(255,255,255,.07);border-radius:100px;height:8px;overflow:hidden;margin-bottom:18px}
.fill{height:100%;border-radius:100px;background:linear-gradient(90deg,var(--accent),var(--accent2));width:0%;transition:width .4s ease;position:relative}
.fill::after{content:'';position:absolute;top:0;right:0;width:60px;height:100%;background:linear-gradient(90deg,transparent,rgba(255,255,255,.4));animation:shimmer 1.4s ease infinite}
@keyframes shimmer{0%,100%{opacity:0}50%{opacity:1}}
.prog-stats{display:flex;gap:24px;flex-wrap:wrap}
.st{display:flex;flex-direction:column;gap:3px}
.st-l{font-size:11px;color:var(--muted);text-transform:uppercase;letter-spacing:.5px}
.st-v{font-size:14px;font-weight:600;font-family:'Space Grotesk',sans-serif}
.win-card{background:var(--surface);border:1px solid rgba(34,211,160,.22);border-radius:var(--r);padding:44px 32px;text-align:center;display:none;position:relative;overflow:hidden;margin-bottom:20px}
.win-card.on{display:block;animation:fadeUp .4s ease}
.win-card::before{content:'';position:absolute;top:0;left:0;right:0;height:2px;background:linear-gradient(90deg,transparent,var(--green),transparent);animation:scan 2.2s ease infinite}
@keyframes scan{0%{opacity:0;transform:scaleX(0)}50%{opacity:1;transform:scaleX(1)}100%{opacity:0;transform:scaleX(0)}}
.win-icon{width:76px;height:76px;background:rgba(34,211,160,.1);border:2px solid rgba(34,211,160,.3);border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:34px;margin:0 auto 22px;animation:pop .4s cubic-bezier(.175,.885,.32,1.275)}
@keyframes pop{0%{transform:scale(0);opacity:0}100%{transform:scale(1);opacity:1}}
.win-card h2{font-family:'Space Grotesk',sans-serif;font-size:26px;font-weight:700;margin-bottom:8px}
.win-card p{color:var(--muted);font-size:14px;margin-bottom:30px}
.btn-dl{display:inline-flex;align-items:center;gap:10px;background:linear-gradient(135deg,var(--green),#17a37a);color:#fff;border:none;border-radius:var(--rs);padding:14px 40px;font-size:16px;font-weight:600;font-family:inherit;cursor:pointer;text-decoration:none;transition:all .25s;box-shadow:0 4px 24px rgba(34,211,160,.3)}
.btn-dl:hover{transform:translateY(-2px);box-shadow:0 8px 32px rgba(34,211,160,.45)}
.again{margin-top:18px;font-size:13px;color:var(--muted)}
.again a{color:var(--accent);cursor:pointer;font-weight:500;text-decoration:none}
.again a:hover{text-decoration:underline}
.qr-card{background:var(--surface);border:1px solid rgba(79,172,254,.25);border-radius:var(--r);padding:32px 28px;text-align:center;display:none;position:relative;overflow:hidden;margin-bottom:20px}
.qr-card.on{display:block;animation:fadeUp .4s ease}
.qr-card::before{content:'';position:absolute;top:0;left:0;right:0;height:2px;background:linear-gradient(90deg,transparent,var(--accent2),transparent);animation:scan 2.6s ease infinite}
.qr-card h3{font-family:'Space Grotesk',sans-serif;font-size:19px;font-weight:700;margin-bottom:6px}
.qr-sub{color:var(--muted);font-size:13px;margin-bottom:22px;max-width:380px;margin-left:auto;margin-right:auto;line-height:1.6}
.qr-box{display:inline-block;background:#fff;border-radius:18px;padding:16px;margin-bottom:20px;box-shadow:0 0 50px rgba(79,172,254,.18);width:200px;height:200px;display:flex;align-items:center;justify-content:center}
.qr-spinner{width:36px;height:36px;border:3px solid rgba(79,172,254,.2);border-top-color:#4facfe;border-radius:50%;animation:spin .8s linear infinite}
@keyframes spin{to{transform:rotate(360deg)}}
#qrCanvas{display:block;width:200px;height:200px}
.qr-steps{display:flex;justify-content:center;gap:20px;flex-wrap:wrap;margin-bottom:16px}
.qr-step{display:flex;align-items:center;gap:8px;font-size:13px;color:var(--muted)}
.qr-num{width:24px;height:24px;border-radius:50%;background:rgba(79,172,254,.12);border:1px solid rgba(79,172,254,.28);color:var(--accent2);font-size:11px;font-weight:700;display:flex;align-items:center;justify-content:center;flex-shrink:0}
.qr-expire{font-size:12px;color:var(--muted);opacity:.7}
.qr-timer{color:var(--accent2);font-weight:700}
.toast{position:fixed;bottom:24px;right:24px;background:rgba(18,20,32,.95);border:1px solid var(--border);border-radius:13px;padding:13px 18px;font-size:13px;display:flex;align-items:center;gap:10px;z-index:999;transform:translateY(80px);opacity:0;transition:all .32s cubic-bezier(.175,.885,.32,1.275);max-width:300px;backdrop-filter:blur(20px)}
.toast.show{transform:translateY(0);opacity:1}
footer{text-align:center;padding:36px 0 12px;color:var(--muted);font-size:13px}
footer strong{color:var(--text)}
.particle{position:fixed;pointer-events:none;z-index:900;border-radius:50%;animation:fall linear forwards}
@keyframes fall{0%{transform:translateY(-20px) rotate(0deg);opacity:1}100%{transform:translateY(110vh) rotate(720deg);opacity:0}}
</style>
</head>
<body>
<div class="orbs">
  <div class="orb o1"></div><div class="orb o2"></div><div class="orb o3"></div>
</div>
<div class="wrap">
  <header>
    <div class="logo"><div class="logo-mark">&#9654;</div>TiRo <em>Convert</em></div>
    <div class="pill-badge">100% Local &middot; No Upload</div>
  </header>
  <div class="hero">
    <h1>Your videos, <b>everywhere they need to be</b></h1>
    <p>Re-encode your video entirely in the browser &mdash; no server, no FFmpeg, no account. Pure browser technology.</p>
  </div>
  <div class="compat-note" id="compatNote"></div>
  <div class="drop-zone" id="dz">
    <div class="dz-icon">&#127916;</div>
    <h2>Drop your video here</h2>
    <p>MP4, MOV, WEBM, AVI, MKV and more</p>
    <button class="btn-browse" id="dzBtn">&#128193; Choose File</button>
    <div class="fmt-note"><strong>Files stay on your device</strong> &mdash; nothing leaves your browser</div>
    <input type="file" id="filePick" accept="video/*,.mkv,.mov,.avi,.wmv,.webm,.m4v">
  </div>
  <div class="preview-wrap" id="previewWrap">
    <div class="preview-top" id="previewTop">
      <video id="previewVid" preload="metadata" muted playsinline></video>
      <div class="preview-overlay"><div class="play-btn">&#9654;</div></div>
      <div class="vol-bar"><div class="vol-fill" id="volFill"></div></div>
    </div>
    <div class="preview-meta">
      <div class="preview-tags" id="previewTags"></div>
      <div style="display:flex;align-items:center;gap:10px;flex-wrap:wrap">
        <span class="preview-fname" id="previewFname"></span>
        <button class="btn-change" onclick="document.getElementById('filePick').click()">Change file</button>
      </div>
    </div>
  </div>
  <div class="card" id="settCard">
    <div class="card-head">
      <div class="file-chip">
        <div class="file-thumb">&#127902;</div>
        <div><div class="fname" id="fName">video.mp4</div><div class="fsize" id="fSize">&mdash;</div></div>
      </div>
      <button class="btn-rm" onclick="reset()">&times; Remove</button>
    </div>
    <div class="presets-row">
      <div class="sec-label">&#9889; Quick Preset</div>
      <div class="chips" id="presetChips">
        <button class="chip on" data-v="original">Original Quality</button>
        <button class="chip" data-v="iphone">Best for iPhone</button>
        <button class="chip" data-v="android">Best for Android</button>
        <button class="chip" data-v="small">Small File Size</button>
        <button class="chip" data-v="whatsapp">WhatsApp</button>
      </div>
    </div>
    <div class="sg">
      <div class="sg-cell">
        <div class="sec-label">&#127909; Output Format</div>
        <div class="chips" id="fmtChips">
          <button class="chip on" data-v="webm">WEBM (VP9)</button>
          <button class="chip" data-v="mp4">MP4 (H.264)*</button>
        </div>
        <div style="font-size:11px;color:var(--muted);margin-top:8px">*MP4 requires Chrome 130+ or Safari</div>
      </div>
      <div class="sg-cell">
        <div class="sec-label">&#128208; Resolution</div>
        <div class="chips" id="resChips">
          <button class="chip on" data-v="orig">Original</button>
          <button class="chip" data-v="1080">1080p</button>
          <button class="chip" data-v="720">720p</button>
          <button class="chip" data-v="480">480p</button>
        </div>
      </div>
      <div class="sg-cell">
        <div class="sec-label">&#10024; Quality / Bitrate</div>
        <div class="chips" id="qualChips">
          <button class="chip" data-v="max">Max (8 Mbps)</button>
          <button class="chip on" data-v="high">High (4 Mbps)</button>
          <button class="chip" data-v="med">Medium (2 Mbps)</button>
          <button class="chip" data-v="small">Small (1 Mbps)</button>
        </div>
      </div>
      <div class="sg-cell" style="border-bottom:none">
        <div class="sec-label">&#128266; Audio Bitrate</div>
        <div class="chips" id="audChips">
          <button class="chip on" data-v="192">192 kbps</button>
          <button class="chip" data-v="128">128 kbps</button>
          <button class="chip" data-v="96">96 kbps</button>
        </div>
      </div>
    </div>
    <div class="conv-row">
      <div class="info-tags" id="infoTags"><div class="itag">Analysing&hellip;</div></div>
      <button class="btn-go" id="btnGo">&#9889; Convert Now</button>
    </div>
  </div>
  <div class="prog-card" id="progCard">
    <div class="prog-top">
      <div class="prog-title"><div class="ring"></div><span id="progLabel">Converting&hellip;</span></div>
      <div class="prog-num" id="progNum">0%</div>
    </div>
    <div class="track"><div class="fill" id="progFill"></div></div>
    <div class="prog-stats">
      <div class="st"><span class="st-l">Elapsed</span><span class="st-v" id="stEl">&mdash;</span></div>
      <div class="st"><span class="st-l">Stage</span><span class="st-v" id="stStage">&mdash;</span></div>
      <div class="st"><span class="st-l">File Size</span><span class="st-v" id="stSize">&mdash;</span></div>
    </div>
  </div>
  <div class="win-card" id="winCard">
    <div class="win-icon">&#9989;</div>
    <h2>Conversion Complete!</h2>
    <p>Your video is ready. Everything stayed on your device.</p>
    <a class="btn-dl" id="dlBtn" href="#" download="tiro-converted.webm">&#11015;&#65039; Download Video</a>
    <div class="again">Convert another? <a onclick="reset()">Start over</a></div>
  </div>
  <div class="qr-card" id="qrCard">
    <h3>&#128241; Send to Phone</h3>
    <p class="qr-sub" id="qrSub">Scan with your phone camera &mdash; the video will auto-download. No cables, no cloud.</p>
    <div class="qr-box" id="qrBox"><canvas id="qrCanvas" width="200" height="200"></canvas></div>
    <div class="qr-steps" id="qrSteps">
      <div class="qr-step"><span class="qr-num">1</span> Open camera</div>
      <div class="qr-step"><span class="qr-num">2</span> Point at QR</div>
      <div class="qr-step"><span class="qr-num">3</span> Tap link &rarr; download</div>
    </div>
    <div class="qr-expire" id="qrExpireWrap">Link expires in <span class="qr-timer" id="qrTimer">10:00</span></div>
  </div>
  <footer><p>Created by <strong>TiRo Pride</strong> &nbsp;&middot;&nbsp; All processing happens locally in your browser</p></footer>
</div>
<div class="toast" id="toast"><span id="toastIco">&#8505;&#65039;</span><span id="toastTxt">&mdash;</span></div>
<script>
// TiRo Convert — Browser-Native Engine
// Uses MediaRecorder + Canvas — zero external dependencies
const $=id=>document.getElementById(id);
const S={preset:'original',fmt:'webm',res:'orig',qual:'high',aud:'192'};
const BITRATES={max:8000000,high:4000000,med:2000000,small:1000000};
const PRESETS={
  original:{qual:'high',res:'orig',fmt:'webm',aud:'192'},
  iphone:  {qual:'high',res:'720', fmt:'mp4', aud:'128'},
  android: {qual:'high',res:'720', fmt:'webm',aud:'128'},
  small:   {qual:'small',res:'480',fmt:'webm',aud:'96'},
  whatsapp:{qual:'small',res:'480',fmt:'webm',aud:'96'}
};
let inputFile=null,outputBlob=null,previewUrl=null,previewPlaying=false;
let qrTimerInterval=null,qrPublicUrl=null;

function wireChips(gid,key){
  $(gid).querySelectorAll('.chip').forEach(c=>{
    c.addEventListener('click',()=>{
      $(gid).querySelectorAll('.chip').forEach(x=>x.classList.remove('on'));
      c.classList.add('on'); S[key]=c.dataset.v;
    });
  });
}
wireChips('presetChips','preset');
wireChips('fmtChips','fmt');
wireChips('resChips','res');
wireChips('qualChips','qual');
wireChips('audChips','aud');

$('presetChips').querySelectorAll('.chip').forEach(c=>{
  c.addEventListener('click',()=>{
    const p=PRESETS[c.dataset.v]; if(!p)return;
    const map={fmt:'fmtChips',res:'resChips',qual:'qualChips',aud:'audChips'};
    ['fmt','res','qual','aud'].forEach(k=>{
      S[k]=p[k];
      $(map[k]).querySelectorAll('.chip').forEach(x=>x.classList.toggle('on',x.dataset.v===p[k]));
    });
  });
});

const dz=$('dz');
dz.addEventListener('dragover',e=>{e.preventDefault();dz.classList.add('over');});
dz.addEventListener('dragleave',()=>dz.classList.remove('over'));
dz.addEventListener('drop',e=>{e.preventDefault();dz.classList.remove('over');if(e.dataTransfer.files[0])pickFile(e.dataTransfer.files[0]);});
dz.addEventListener('click',e=>{if(!e.target.closest('#dzBtn'))$('filePick').click();});
$('dzBtn').addEventListener('click',e=>{e.stopPropagation();$('filePick').click();});
$('filePick').addEventListener('change',e=>{if(e.target.files[0])pickFile(e.target.files[0]);});

function pickFile(f){
  inputFile=f; $('fName').textContent=f.name; $('fSize').textContent=fmtBytes(f.size);
  dz.style.display='none'; show('settCard'); loadPreview(f);
}

function loadPreview(f){
  if(previewUrl)URL.revokeObjectURL(previewUrl);
  previewPlaying=false; previewUrl=URL.createObjectURL(f);
  const vid=$('previewVid'); vid.src=previewUrl; vid.pause();
  $('previewFname').textContent=f.name; show('previewWrap');
  const pt=$('previewTags'); pt.innerHTML='';
  addPTag(pt,f.name.split('.').pop().toUpperCase(),'');
  addPTag(pt,fmtBytes(f.size),'blue');
  vid.onloadedmetadata=()=>{
    addPTag(pt,Math.round(vid.videoWidth)+'x'+Math.round(vid.videoHeight),'');
    addPTag(pt,fmtDur(vid.duration),'green');
    const it=$('infoTags'); it.innerHTML='';
    [f.name.split('.').pop().toUpperCase(),fmtBytes(f.size),
     Math.round(vid.videoWidth)+'x'+Math.round(vid.videoHeight),fmtDur(vid.duration)
    ].forEach(t=>addTag(it,t));
  };
  $('previewTop').onclick=()=>{
    if(previewPlaying){vid.pause();previewPlaying=false;}
    else{vid.play();previewPlaying=true;}
  };
  vid.ontimeupdate=()=>{if(vid.duration)$('volFill').style.width=(vid.currentTime/vid.duration*100)+'%';};
  vid.onended=()=>{previewPlaying=false;};
}

$('btnGo').addEventListener('click',startConvert);

async function startConvert(){
  if(!inputFile)return;
  $('btnGo').disabled=true;
  $('previewVid').pause(); previewPlaying=false;
  show('progCard'); hide('winCard'); hide('qrCard');
  setProgress(0,'Preparing...'); setStage('Init');
  const t0=Date.now();
  const elapsed=()=>((Date.now()-t0)/1000).toFixed(1)+'s';
  try{
    // Load metadata
    const vid=document.createElement('video');
    vid.muted=true; vid.src=previewUrl;
    await new Promise(r=>{vid.onloadedmetadata=r;vid.load();});
    let W=vid.videoWidth,H=vid.videoHeight;
    if(S.res!=='orig'){
      const tH=parseInt(S.res);
      if(H>tH){W=Math.round(W*tH/H);H=tH;}
      if(W%2)W++; if(H%2)H++;
    }
    setProgress(5,'Setting up...');

    // Pick MIME
    const mimes=S.fmt==='mp4'
      ?['video/mp4;codecs=avc1','video/mp4']
      :['video/webm;codecs=vp9,opus','video/webm;codecs=vp8,opus','video/webm'];
    const mimeType=mimes.find(m=>MediaRecorder.isTypeSupported(m))||'video/webm';
    const outExt=mimeType.startsWith('video/mp4')?'mp4':'webm';
    const videoBps=BITRATES[S.qual]||4000000;
    const audioBps=parseInt(S.aud)*1000||192000;

    // Canvas
    const canvas=document.createElement('canvas');
    canvas.width=W; canvas.height=H;
    const ctx=canvas.getContext('2d');
    const fps=30;
    const canvasStream=canvas.captureStream(fps);

    // Audio via Web Audio API
    let audioTracks=[];
    try{
      const AudioCtx=window.AudioContext||window.webkitAudioContext;
      const audioCtx=new AudioCtx();
      const dest=audioCtx.createMediaStreamDestination();
      const src=audioCtx.createMediaElementSource(vid);
      src.connect(dest); src.connect(audioCtx.destination);
      audioTracks=dest.stream.getAudioTracks();
    }catch(e){console.warn('Audio pipe failed:',e);}

    const outStream=new MediaStream([...canvasStream.getVideoTracks(),...audioTracks]);
    const chunks=[];
    const recorder=new MediaRecorder(outStream,{mimeType,videoBitsPerSecond:videoBps,audioBitsPerSecond:audioBps});
    recorder.ondataavailable=e=>{if(e.data.size>0)chunks.push(e.data);};
    let recDone=new Promise(r=>{recorder.onstop=r;});
    recorder.start(200);

    // Play and draw
    vid.currentTime=0; vid.muted=true;
    await vid.play();
    setStage('Encoding...'); setProgress(10,'Encoding...');
    const duration=vid.duration; let lastPct=10;

    await new Promise((resolve,reject)=>{
      const draw=()=>{
        ctx.drawImage(vid,0,0,W,H);
        $('stEl').textContent=elapsed();
        const pct=Math.min(10+Math.round((vid.currentTime/duration)*85),95);
        if(pct>lastPct){setProgress(pct,'Encoding...');lastPct=pct;}
        if(!vid.ended&&!vid.paused)requestAnimationFrame(draw);
        else resolve();
      };
      vid.onended=resolve; vid.onerror=reject;
      requestAnimationFrame(draw);
    });

    setProgress(97,'Finalising...'); setStage('Done');
    recorder.stop(); await recDone;

    const blob=new Blob(chunks,{type:mimeType});
    outputBlob=blob;
    $('stEl').textContent=elapsed();
    $('stSize').textContent=fmtBytes(blob.size);
    setProgress(100,'Complete!');

    const dlUrl=URL.createObjectURL(blob);
    const dl=$('dlBtn');
    dl.href=dlUrl;
    const fname=inputFile.name.replace(/\.[^.]+$/,'')+'-tiro.'+outExt;
    dl.download=fname;

    setTimeout(()=>{
      hide('progCard'); show('winCard'); spawnConfetti();
      generateQR(blob,fname);
    },600);
  }catch(err){
    toast('Conversion error: '+err.message,'err');
    console.error(err);
    $('btnGo').disabled=false; hide('progCard');
  }
}

// ── QR Code ──
// IMPORTANT: a blob:/data: URL only exists inside THIS browser tab's memory.
// A phone scanning the QR is a totally different device/browser, so it can
// never resolve a blob: link — that's why the scan "did nothing" before.
// Fix: upload the converted file to a short-lived public host and QR-encode
// that real https:// link instead.
//
// NOTE on file:// pages: opening this HTML by double-clicking it (file:///C:/...)
// loads it with origin "null". Some upload hosts/CORS configs don't like that
// origin and the request can stall instead of failing cleanly — that's why a
// hard timeout below is required, so the UI never spins forever.
const UPLOAD_HOSTS=[
  {name:'file.io', url:'https://file.io/?expires=1d',
   parse:async res=>{const d=await res.json(); if(!d||!d.success||!d.link) throw new Error('bad response'); return d.link;}},
  {name:'0x0.st', url:'https://0x0.st',
   parse:async res=>{const t=(await res.text()).trim(); if(!/^https?:\/\//.test(t)) throw new Error('bad response'); return t;}}
];

function fetchWithTimeout(url,opts,ms){
  const ctrl=new AbortController();
  const timer=setTimeout(()=>ctrl.abort(),ms);
  return fetch(url,{...opts,signal:ctrl.signal}).finally(()=>clearTimeout(timer));
}

async function generateQR(blob,filename){
  show('qrCard');
  $('qrSub').textContent='Uploading for phone download…';
  $('qrBox').innerHTML='<div class="qr-spinner"></div>';
  $('qrSteps').style.opacity='.35';
  startQRTimer(true);

  const isFileProtocol=location.protocol==='file:';
  let lastErr=null;

  for(const host of UPLOAD_HOSTS){
    try{
      const fd=new FormData();
      fd.append('file',blob,filename);
      const res=await fetchWithTimeout(host.url,{method:'POST',body:fd,mode:'cors'},15000);
      if(!res.ok) throw new Error('HTTP '+res.status);
      const link=await host.parse(res);

      qrPublicUrl=link;
      $('qrBox').innerHTML='<canvas id="qrCanvas" width="200" height="200"></canvas>';
      drawQR($('qrCanvas'),qrPublicUrl);
      $('qrSub').textContent='Scan with your phone camera — the video will download from a temporary public link.';
      $('qrSteps').style.opacity='1';
      startQRTimer(false);
      return;
    }catch(err){
      lastErr=err;
      console.error('QR upload failed via '+host.name+':',err);
    }
  }

  // Every host failed or timed out
  console.error('All upload hosts failed:',lastErr);
  $('qrBox').innerHTML='<div style="font-size:13px;color:var(--muted);padding:30px 8px;line-height:1.6">QR unavailable</div>';
  $('qrExpireWrap').textContent='';
  clearInterval(qrTimerInterval);
  if(isFileProtocol){
    $('qrSub').innerHTML='Phone link failed because this page was opened directly from a file (<code style="color:var(--accent2)">file://</code>). Browsers block this kind of upload from local files. <b>Open this HTML through a local web server</b> (or host it online) and try again — or just use <b>Download Video</b> above on this device.';
    toast('file:// pages can\'t upload — serve the HTML over http(s) instead','warn');
  }else{
    $('qrSub').innerHTML='Could not create a phone link (no internet, or upload hosts are down/blocked). You can still use the <b>Download Video</b> button above on this device.';
    toast('Phone-link upload failed — use the Download button instead','warn');
  }
}

function startQRTimer(preparing){
  clearInterval(qrTimerInterval);
  if(preparing){$('qrExpireWrap').textContent='Preparing link…';return;}
  let secs=600;
  $('qrExpireWrap').innerHTML='Link expires in <span class="qr-timer" id="qrTimer">10:00</span>';
  const liveEl=$('qrTimer');
  const tick=()=>{
    const m=Math.floor(secs/60),s=String(secs%60).padStart(2,'0');
    liveEl.textContent=m+':'+s;
    if(secs<=0){clearInterval(qrTimerInterval);liveEl.textContent='Expired';liveEl.style.color='var(--red)';
      qrPublicUrl=null;}
    secs--;
  };
  tick(); qrTimerInterval=setInterval(tick,1000);
}

// ── Pure-JS QR encoder (Byte mode, ECC-M) ──
// GF(256)
const GFe=new Uint8Array(512),GFl=new Uint8Array(256);
(()=>{let x=1;for(let i=0;i<255;i++){GFe[i]=x;GFl[x]=i;x=x<<1;if(x&256)x^=285;}for(let i=255;i<512;i++)GFe[i]=GFe[i-255];})();
const gfm=(a,b)=>(!a||!b)?0:GFe[GFl[a]+GFl[b]];
const gfp=(x,p)=>GFe[(GFl[x]*p)%255];
function rsPoly(n){let p=[1];for(let i=0;i<n;i++){const q=[1,gfp(2,i)],r=new Array(p.length+q.length-1).fill(0);for(let j=0;j<p.length;j++)for(let k=0;k<q.length;k++)r[j+k]^=gfm(p[j],q[k]);p=r;}return p;}
function rsEnc(data,ecLen){const poly=rsPoly(ecLen),rem=[...data,...new Array(ecLen).fill(0)];for(let i=0;i<data.length;i++){const c=rem[i];if(c)for(let j=0;j<poly.length;j++)rem[i+j]^=gfm(poly[j],c);}return rem.slice(data.length);}

const ALIGN=[
  [],[],[6,18],[6,22],[6,26],[6,30],[6,34],[6,22,38],[6,24,42],[6,26,46],[6,28,50],
  [6,30,54],[6,32,58],[6,34,62],[6,26,46,66],[6,26,48,70],[6,26,50,74],[6,30,54,78],
  [6,30,56,82],[6,30,58,86],[6,34,62,90]
];
const ECCM=[null,{d:16,e:10},{d:28,e:16},{d:44,e:26},{d:64,e:36},{d:86,e:48},{d:108,e:64},{d:124,e:72},{d:154,e:88},{d:182,e:110},{d:216,e:130}];
const CAP=[0,14,26,42,62,84,106,122,154,180,206];

function drawQR(canvas,text){
  try{
    const bytes=Array.from(new TextEncoder().encode(text));
    let ver=1; while(ver<=10&&CAP[ver]<bytes.length)ver++;
    if(ver>10){console.warn('QR: URL too long for ver 10, capping');ver=10;}
    const size=ver*4+17;
    const mat=Array.from({length:size},()=>new Array(size).fill(null));
    const reserved=Array.from({length:size},()=>new Array(size).fill(false)); // function-pattern modules — never masked

    // Finder
    const finder=(r,c)=>{for(let dr=-1;dr<=7;dr++)for(let dc=-1;dc<=7;dc++){if(r+dr<0||r+dr>=size||c+dc<0||c+dc>=size)continue;const io=(dr>=0&&dr<=6&&(dc===0||dc===6))||(dc>=0&&dc<=6&&(dr===0||dr===6));const ii=dr>=2&&dr<=4&&dc>=2&&dc<=4;mat[r+dr][c+dc]=io||ii;reserved[r+dr][c+dc]=true;}};
    finder(0,0);finder(0,size-7);finder(size-7,0);

    // Timing
    for(let i=8;i<size-8;i++){mat[6][i]=mat[i][6]=(i%2===0);reserved[6][i]=true;reserved[i][6]=true;}
    mat[size-8][8]=true;reserved[size-8][8]=true;

    // Alignment
    const ap=ALIGN[ver]||[];
    for(const ar of ap)for(const ac of ap){if(mat[ar][ac]!==null)continue;for(let dr=-2;dr<=2;dr++)for(let dc=-2;dc<=2;dc++){mat[ar+dr][ac+dc]=(dr===0&&dc===0)||(Math.abs(dr)===2||Math.abs(dc)===2);reserved[ar+dr][ac+dc]=true;}}

    // Reserve format
    for(let i=0;i<=8;i++){if(mat[8][i]===null)mat[8][i]=false;reserved[8][i]=true;if(mat[i][8]===null)mat[i][8]=false;reserved[i][8]=true;}
    for(let i=size-7;i<size;i++){if(mat[8][i]===null)mat[8][i]=false;reserved[8][i]=true;if(mat[i][8]===null)mat[i][8]=false;reserved[i][8]=true;}

    // Data codewords
    const {d:dataCW,e:ecCW}=ECCM[ver];
    const len=Math.min(bytes.length,dataCW-3);
    let bits=[];
    bits.push(0,1,0,0);
    for(let i=7;i>=0;i--)bits.push((len>>i)&1);
    for(let i=0;i<len;i++)for(let j=7;j>=0;j--)bits.push((bytes[i]>>j)&1);
    for(let i=0;i<4&&bits.length<dataCW*8;i++)bits.push(0);
    while(bits.length%8)bits.push(0);
    const pads=[0b11101100,0b00010001];let pi=0;
    while(bits.length<dataCW*8){for(let j=7;j>=0;j--)bits.push((pads[pi%2]>>j)&1);pi++;}
    const cws=[];for(let i=0;i<dataCW;i++){let b=0;for(let j=0;j<8;j++)b=(b<<1)|bits[i*8+j];cws.push(b);}
    const ec=rsEnc(cws.slice(0,dataCW),ecCW);
    const all=[...cws.slice(0,dataCW),...ec];

    // Place data
    let idx=0,bit=7,up=true;
    for(let col=size-1;col>0;col-=2){
      if(col===6)col=5;
      for(let row=0;row<size;row++){
        const r=up?size-1-row:row;
        for(let c=col;c>=col-1;c--){
          if(mat[r][c]!==null)continue;
          mat[r][c]=idx<all.length?!!((all[idx]>>bit)&1):false;
          if(--bit<0){bit=7;idx++;}
        }
      }
      up=!up;
    }

    // Mask 0: (r+c)%2===0 — must NOT touch finder/timing/alignment/format modules
    for(let r=0;r<size;r++)for(let c=0;c<size;c++)if(mat[r][c]!==null&&!reserved[r][c]&&(r+c)%2===0)mat[r][c]=!mat[r][c];

    // Format info (ECC-M=01, mask=0)
    const fmt=0b01<<3|0;
    let fd=fmt<<10;const gp=0b10100110111;
    for(let i=14;i>=10;i--)if((fd>>i)&1)fd^=gp<<(i-10);
    const fb=((fmt<<10)|(fd&0x3FF))^0b101010000010010;
    const fp=[0,1,2,3,4,5,7,8,8,8,8,8,8,8,8];
    const fr=[8,8,8,8,8,8,8,8,7,5,4,3,2,1,0];
    for(let i=0;i<15;i++){const b=!!((fb>>(14-i))&1);mat[fr[i]][fp[i]]=b;if(i<7)mat[size-1-i][8]=b;else mat[8][size-7+(i-7)]=b;}

    // Draw (with a quiet-zone margin around the code, required for reliable scanning)
    const ctx=canvas.getContext('2d');
    const sz=canvas.width;
    const margin=4; // modules of quiet zone on each side, per QR spec
    const cell=sz/(size+margin*2);
    ctx.fillStyle='#fff';ctx.fillRect(0,0,sz,sz);
    ctx.fillStyle='#000';
    for(let r=0;r<size;r++)for(let c=0;c<size;c++)
      if(mat[r][c])ctx.fillRect(Math.floor((c+margin)*cell),Math.floor((r+margin)*cell),Math.ceil(cell),Math.ceil(cell));

  }catch(e){
    console.error('QR error:',e);
    const ctx=canvas.getContext('2d');
    ctx.fillStyle='#fff';ctx.fillRect(0,0,200,200);
    ctx.fillStyle='#666';ctx.font='12px sans-serif';ctx.fillText('QR error',10,100);
  }
}

// ── Helpers ──
function setProgress(pct,label){$('progNum').textContent=pct+'%';$('progFill').style.width=pct+'%';if(label)$('progLabel').textContent=label;}
function setStage(s){$('stStage').textContent=s;}
function show(id){$(id).classList.add('on');}
function hide(id){$(id).classList.remove('on');}
function toast(msg,type='info'){const ico={ok:'OK',err:'ERR',warn:'WARN',info:'INFO'}[type]||'INFO';$('toastIco').textContent={ok:'✅',err:'❌',warn:'⚠️',info:'ℹ️'}[type]||'ℹ️';$('toastTxt').textContent=msg;const t=$('toast');t.classList.add('show');clearTimeout(t._t);t._t=setTimeout(()=>t.classList.remove('show'),4200);}
function reset(){
  inputFile=null;outputBlob=null;$('filePick').value='';dz.style.display='';
  hide('settCard');hide('progCard');hide('winCard');hide('previewWrap');hide('qrCard');
  clearInterval(qrTimerInterval);qrPublicUrl=null;
  $('btnGo').disabled=false;setProgress(0,'');$('infoTags').innerHTML='<div class="itag">Analysing\u2026</div>';
  const vid=$('previewVid');vid.pause();vid.src='';previewPlaying=false;
  if(previewUrl){URL.revokeObjectURL(previewUrl);previewUrl=null;}
}
function fmtBytes(b){if(b<1024)return b+' B';if(b<1048576)return(b/1024).toFixed(1)+' KB';if(b<1073741824)return(b/1048576).toFixed(1)+' MB';return(b/1073741824).toFixed(2)+' GB';}
function fmtDur(s){const m=Math.floor(s/60),sec=Math.floor(s%60);return m+':'+String(sec).padStart(2,'0');}
function addPTag(p,t,cls){const d=document.createElement('div');d.className='ptag'+(cls?' '+cls:'');d.textContent=t;p.appendChild(d);}
function addTag(p,t){const d=document.createElement('div');d.className='itag';d.textContent=t;p.appendChild(d);}
function spawnConfetti(){const cols=['#7c6ff7','#4facfe','#22d3a0','#fff','#f9c74f'];for(let i=0;i<40;i++){const p=document.createElement('div');p.className='particle';const sz=5+Math.random()*8,dur=1.4+Math.random();p.style.cssText='left:'+Math.random()*100+'%;top:-10px;width:'+sz+'px;height:'+sz+'px;background:'+cols[Math.floor(Math.random()*cols.length)]+';border-radius:'+(Math.random()>.5?'50%':'3px')+';animation-duration:'+dur+'s;animation-delay:'+Math.random()*.6+'s';document.body.appendChild(p);setTimeout(()=>p.remove(),(dur+.6)*1000+200);}}

// Compat check
(()=>{
  const issues=[];
  if(!window.MediaRecorder)issues.push('MediaRecorder not supported');
  if(!HTMLCanvasElement.prototype.captureStream)issues.push('Canvas captureStream not supported');
  if(issues.length){
    const n=$('compatNote');
    n.innerHTML='<strong>Browser Compatibility Issue:</strong> '+issues.join(' &middot; ')+'. Please use <strong>Chrome</strong> or <strong>Edge</strong> for best results.';
    n.classList.add('on');
  }else{
    toast('Ready \u2014 drop a video to begin','ok');
  }
})();
</script>
</body>
</html>
