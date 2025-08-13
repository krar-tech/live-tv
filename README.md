<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="utf-8" />
  <title>لايف سبورت — نسخة محسنة</title>
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <meta name="theme-color" content="#26A69A" />
  <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@400;700;800&display=swap" rel="stylesheet">
  <style>
    :root{
      --accent:#26A69A;
      --accent-2:#4DB6AC;
      --bg1:#071021;
      --bg2:#0F1B2B;
      --glass: rgba(255,255,255,0.04);
      --text:#E8FFF9;
      --muted:#BFECE4;
      --max-width:980px;
      --card-radius:12px;
      --transition: 180ms cubic-bezier(.2,.9,.3,1);
      --iframe-shift: -120px;
      --news-cut: 120px;
      --news-shift: calc(-1 * var(--news-cut));
    }
    *{box-sizing:border-box}
    html,body{height:100%;margin:0;padding:0;background:linear-gradient(120deg,var(--bg1),var(--bg2));font-family:'Tajawal',sans-serif;color:var(--text);-webkit-font-smoothing:antialiased;overflow-x:hidden}
    a{color:var(--accent-2);text-decoration:none}
    body::before{content:"";position:fixed;inset:0;z-index:0;pointer-events:none;background:radial-gradient(600px 400px at 10% 10%, rgba(77,182,172,0.06), transparent),radial-gradient(400px 300px at 90% 80%, rgba(38,166,154,0.04), transparent);animation: bgMove 18s linear infinite;mix-blend-mode:screen;opacity:0.95}
    @keyframes bgMove{ from{transform:translateY(0)}50%{transform:translateY(-20px)}to{transform:translateY(0)} }

    header{position:sticky;top:0;z-index:140;padding:10px 16px;display:flex;align-items:center;gap:12px;justify-content:space-between;background: linear-gradient(90deg, rgba(3,6,9,0.88), rgba(3,6,9,0.45));border-bottom:1px solid rgba(255,255,255,0.03);backdrop-filter: blur(6px);}
    .brand{display:flex;align-items:center;gap:12px}
    header img{max-width:86px;border-radius:10px;cursor:pointer;box-shadow:0 6px 18px rgba(2,6,8,0.6)}
    header h1{font-size:20px;color:var(--accent-2);margin:0;font-weight:800;letter-spacing:0.6px}

    .controls{display:flex;align-items:center;gap:10px}
    .icon-btn{display:inline-flex;align-items:center;gap:8px;background: linear-gradient(180deg, var(--glass), rgba(255,255,255,0.02));border:1px solid rgba(255,255,255,0.04);padding:8px 10px;border-radius:10px;color:var(--muted);cursor:pointer;font-weight:700;transition:all var(--transition);box-shadow: 0 6px 22px rgba(0,0,0,0.45)}
    .icon-btn:hover{ transform:translateY(-3px); color:#071014; background:linear-gradient(90deg,var(--accent-2),var(--accent)) }

    .top-tabs{max-width:var(--max-width);margin:10px auto 6px;display:flex;gap:8px;align-items:center;justify-content:flex-start;padding:8px 6px;position:sticky;top:64px;z-index:135;background:transparent;border-radius:12px}
    .top-tab{padding:8px 14px;border-radius:10px;cursor:pointer;font-weight:800;background:transparent;color:var(--muted);border:1px solid rgba(255,255,255,0.03);transition:all var(--transition)}
    .top-tab.active{background:linear-gradient(90deg,var(--accent-2),var(--accent));color:#071014;box-shadow:0 14px 36px rgba(38,166,154,0.06);transform:translateY(-2px)}

    .search-bar{padding:8px 12px;max-width:var(--max-width);margin:8px auto 0 auto;text-align:center;position:relative;z-index:120}
    .search-bar input{padding:10px 12px;width:100%;max-width:520px;border-radius:10px;border:1px solid rgba(255,255,255,0.04);background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));color:var(--text);font-size:14px;outline:none;transition:box-shadow .18s}
    .search-bar input:focus{ box-shadow:0 8px 24px rgba(38,166,154,0.06); border-color: rgba(77,182,172,0.9) }

    .channel-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(160px,1fr));gap:10px;padding:10px;max-width:var(--max-width);margin:12px auto 80px;position:relative;z-index:20}
    .channel-card{background:linear-gradient(180deg, rgba(255,255,255,0.012), rgba(255,255,255,0.006));border:1px solid rgba(255,255,255,0.03);border-radius:12px;padding:8px;text-align:center;position:relative;transition:transform .18s cubic-bezier(.2,.9,.3,1), box-shadow .18s;overflow:visible;cursor:default;box-shadow: 0 8px 20px rgba(8,12,16,0.45)}
    .channel-card:hover{ transform:translateY(-6px); box-shadow: 0 14px 36px rgba(8,12,16,0.5) }
    .logo{width:88px;height:56px;object-fit:contain;border-radius:8px;margin:4px auto 6px;padding:4px;background:rgba(255,255,255,0.01)}
    .logo.spanish{width:132px;height:84px}
    @media (max-width:820px){ .logo.spanish{width:112px;height:72px} }
    @media (max-width:480px){ .logo.spanish{width:92px;height:60px} }

    .channel-card h3{font-size:15px;margin:4px 0;color:var(--text);font-weight:800}
    .channel-card p{font-size:12px;color:var(--muted);margin:2px 0}
    .play{background:linear-gradient(90deg,var(--accent-2),var(--accent));color:#071014;border:none;padding:10px 12px;border-radius:10px;cursor:pointer;font-size:14px;font-weight:900;width:100%;box-shadow:0 8px 22px rgba(38,166,154,0.06);transition:transform var(--transition)}
    .play:active{ transform:scale(.98) }
    .play[disabled]{ opacity:0.6; cursor:not-allowed; transform:none; box-shadow:none; background: linear-gradient(90deg, rgba(77,182,172,0.14), rgba(38,166,154,0.12)); color:var(--muted) }
    .fav-btn{position:absolute;top:8px;right:8px;background:transparent;border:none;font-size:18px;color:rgba(255,255,255,0.36);cursor:pointer;transition:transform var(--transition)}
    .fav-btn.is-fav{color:gold;transform:scale(1.06)}
    .live-tag{position:absolute;top:8px;left:8px;background:var(--accent);color:#071014;font-size:11px;padding:4px 7px;border-radius:8px;font-weight:800}

    #iframeContainer{width:100%;max-width:var(--max-width);height:calc(66vh + 40px);margin:18px auto 60px;border-radius:12px;overflow:hidden;position:relative;background:linear-gradient(180deg, rgba(4,6,8,0.5), rgba(7,10,12,0.25));border:1px solid rgba(255,255,255,0.03);z-index:30;box-shadow:0 18px 54px rgba(2,6,8,0.6)}
    #iframePlaceholder{width:100%;height:100%;display:flex;align-items:center;justify-content:center;color:var(--muted);cursor:pointer}
    #matchesFrame{width:100%;height:100%;border:0;display:block;background:transparent;position:relative;transform:translateY(var(--iframe-shift));filter:contrast(1) saturate(1);z-index:1}
    .frame-badge{ position:absolute; top:12px; right:12px; z-index:9999; display:flex; align-items:center; gap:8px; pointer-events:none; background:transparent; padding:6px 8px; border-radius:8px; }
    .frame-badge img{ height:36px; width:auto; border-radius:6px; display:block; }
    .frame-badge .wm-text{ font-weight:900; color:var(--accent-2); font-size:15px; text-shadow:0 2px 6px rgba(0,0,0,0.6) }

    #newsContainer{width:100%;max-width:var(--max-width);height:calc(60vh + 40px);margin:18px auto 60px;border-radius:12px;overflow:hidden;position:relative;background:linear-gradient(180deg, rgba(4,6,8,0.5), rgba(7,10,12,0.25));border:1px solid rgba(255,255,255,0.03);z-index:30;box-shadow:0 18px 54px rgba(2,6,8,0.6);display:none}
    #newsFrame{ width:100%; height:calc(100% + var(--news-cut)) !important; border:0; display:block; background:transparent; position:relative; transform:translateY(var(--news-shift)) !important; will-change:transform; z-index:1; }
    #highlightsContainer{width:100%;max-width:var(--max-width);height:calc(60vh + 40px);margin:18px auto 60px;border-radius:12px;overflow:hidden;position:relative;background:linear-gradient(180deg, rgba(4,6,8,0.5), rgba(7,10,12,0.25));border:1px solid rgba(255,255,255,0.03);z-index:30;box-shadow:0 18px 54px rgba(2,6,8,0.6);display:none}
    #highlightsFrame{ width:100%; height:calc(100% + var(--news-cut)) !important; border:0; display:block; background:transparent; position:relative; transform:translateY(var(--news-shift)) !important; will-change:transform; z-index:1; }

    #playerModal{position:fixed;inset:0;display:none;align-items:center;justify-content:center;background:linear-gradient(180deg, rgba(2,6,8,0.78), rgba(2,6,8,0.9));z-index:13000;padding:12px}
    #playerInner{width:100%;max-width:980px;height:56vh;background:#000;border-radius:12px;overflow:hidden;position:relative;box-shadow:0 20px 60px rgba(0,0,0,0.6);border:1px solid rgba(255,255,255,0.03);display:flex;flex-direction:column;align-items:stretch}
    #playerInner iframe,#playerInner video{width:100%;height:100%;border:0;display:block;background:#000;object-fit:contain}

    .controls-row{position:absolute;left:12px;top:12px;z-index:12111;display:flex;gap:8px}
    .player-control{background:rgba(255,255,255,0.03);border:none;padding:8px 10px;border-radius:10px;color:var(--muted);font-weight:700;cursor:pointer;transition:all var(--transition)}
    .share-channel{background:rgba(255,255,255,0.04);border:none;padding:8px 10px;border-radius:10px;color:var(--muted);font-weight:700;cursor:pointer}
    .btn-close{position:absolute; top:12px; right:12px; z-index:13010;background:rgba(229,57,53,0.95); color:#fff; border:none; padding:8px 10px; border-radius:10px; font-weight:800; cursor:pointer}

    .spinner-wrap{position:absolute;inset:0;display:none;align-items:center;justify-content:center;z-index:12102;background:linear-gradient(180deg, rgba(0,0,0,0.18), rgba(0,0,0,0.28));pointer-events:none}
    .spinner-circle{width:46px;height:46px;border-radius:50%;border:5px solid rgba(255,255,255,0.06);border-top-color:var(--accent);animation:spin 1s linear infinite;margin-bottom:8px}
    @keyframes spin{from{transform:rotate(0)}to{transform:rotate(360deg)}}

    .play-overlay{
      position:absolute;
      inset:0;
      display:flex;
      align-items:center;
      justify-content:center;
      z-index:13005;
      background: linear-gradient(180deg, rgba(0,0,0,0.4), rgba(0,0,0,0.6));
      cursor:pointer;
      -webkit-tap-highlight-color: transparent;
    }
    .play-overlay .btn{
      background:linear-gradient(90deg,var(--accent-2),var(--accent));
      color:#071014;
      padding:12px 18px;
      border-radius:10px;
      font-weight:900;
      box-shadow:0 10px 30px rgba(38,166,154,0.12);
    }

    #toast { position:fixed; left:50%; transform:translateX(-50%); bottom:26px; z-index:14000; background:rgba(0,0,0,0.6); color:#fff; padding:10px 14px; border-radius:10px; font-weight:700; display:none }
    @media (max-width:480px){ .logo{width:72px;height:48px} }
  </style>
</head>
<body>
  <header>
    <div class="brand">
      <img id="brandLogo" src="https://livetvali.neocities.org/1754740387347.jpg" alt="لوغو لايف سبورت" />
      <h1>لايف سبورت ⚽</h1>
    </div>
    <div class="controls">
      <button id="shareSite" class="icon-btn ripple" title="مشاركة الموقع">مشاركة</button>
      <button id="refreshBtn" class="icon-btn ripple" title="تحديث">🔄</button>
      <button id="settingsBtn" class="icon-btn ripple" title="إعدادات">⚙️</button>
    </div>
  </header>

  <div class="top-tabs" role="tablist" aria-label="تبديل العرض">
    <button id="tabChannels" class="top-tab active">القنوات</button>
    <button id="tabMatches" class="top-tab">جدول المباريات</button>
    <button id="tabNews" class="top-tab">أخبار لايف سبورت</button>
    <button id="tabHighlights" class="top-tab">ملخصات واهداف</button>
  </div>

  <div class="search-bar" id="searchBar"><input id="searchInput" type="text" placeholder="🔍 ابحث عن قناة... (اضغط / للتركيز السريع)" aria-label="ابحث عن قناة" /></div>
  <section id="channelGrid" class="channel-grid" aria-live="polite"></section>

  <div id="iframeContainer" role="region" aria-label="جدول المباريات" style="display:none">
    <div id="iframePlaceholder">اضغط لعرض جدول المباريات</div>
    <div id="matchesWatermark" class="frame-badge" style="display:none" aria-hidden="true">
      <img src="https://livetvali.neocities.org/1754740387347.jpg" alt="لوغو">
      <div class="wm-text">جدول لايف سبورت</div>
    </div>
  </div>

  <div id="newsContainer" style="display:none">
    <div id="newsPlaceholder" class="iframe-placeholder">اضغط لعرض الأخبار</div>
    <div id="newsWatermark" class="frame-badge" style="display:none" aria-hidden="true">
      <img src="https://livetvali.neocities.org/1754740387347.jpg" alt="لوغو">
      <div class="wm-text">أخبار لايف سبورت</div>
    </div>
  </div>

  <div id="highlightsContainer" style="display:none">
    <div id="highlightsPlaceholder" class="iframe-placeholder">اضغط لعرض الملخصات والأهداف</div>
    <div id="highlightsWatermark" class="frame-badge" style="display:none" aria-hidden="true">
      <img src="https://livetvali.neocities.org/1754740387347.jpg" alt="لوغو">
      <div class="wm-text">ملخصات لايف سبورت</div>
    </div>
  </div>

  <div id="playerModal" aria-hidden="true">
    <div id="playerInner" role="dialog" aria-modal="true" aria-label="مشغل القناة">
      <div class="controls-row">
        <button id="shareChannelBtn" class="share-channel" title="مشاركة هذه القناة">مشاركة القناة</button>
        <button id="fullscreenBtn" class="player-control ripple" title="ملء الشاشة">ملء الشاشة</button>
      </div>
      <button id="btnClose" class="btn-close" title="إغلاق">إغلاق</button>

      <div class="spinner-wrap" id="playerSpinner" aria-hidden="false">
        <div style="display:flex;flex-direction:column;align-items:center;justify-content:center;color:#e6fff8">
          <div class="spinner-circle" role="status" aria-label="جار التحميل"></div>
          <div id="spinnerText">جارِ تحميل القناة...</div>
        </div>
      </div>

      <div id="playOverlay" class="play-overlay" style="display:none" aria-hidden="true">
        <div class="btn">اضغط لتشغيل بالصوت</div>
      </div>

      <!-- نحتفظ بعنصر الفيديو كاحتياطي لكن الآن روابط m3u8 ستفتح داخل iframe كما طلبت -->
      <video id="playerVideo" playsinline controls style="display:none;pointer-events:auto;background:#000"></video>
      <iframe id="playerFrame" allow="autoplay; fullscreen" style="display:none;pointer-events:auto"></iframe>
    </div>
  </div>

  <div id="toast" role="status" aria-live="polite"></div>

<script>
  const SPORT360_URL = "https://www.btolat.com/news?p=1";
  const HIGHLIGHTS_URL = "https://www.btolat.com/video/type/10/home";
  const BTOLAT_URL = 'https://www.btolat.com/matches-center';

  let channels = [
    { name: 'English 1', quality: '', url: '', type: '', logo: 'https://upload.wikimedia.org/wikipedia/en/f/f2/Premier_League_Logo.svg' },
    { name: 'English 2', quality: '', url: '', type: '', logo: 'https://upload.wikimedia.org/wikipedia/en/f/f2/Premier_League_Logo.svg' },
    { name: 'Spanish 1', quality: '', url: '', type: '', logo: 'https://livetvali.neocities.org/large.jpg' },
    { name: 'Spanish 2', quality: '', url: '', type: '', logo: 'https://livetvali.neocities.org/large.jpg' },

    { name: 'live tv 1', quality: 'HD', url: 'https://stream.veo.buzz:6072/sport/ch1/adaptive.m3u8', type: 'hls', logo: 'https://livetvali.neocities.org/1754740387347.jpg' },
    /* رابطك الجديد تم إضافته هنا (live tv 2) */
    { name: 'live tv 2', quality: 'HD', url: 'https://stream.supertv.gg:3002/supertv/sport/stv2/ch2/ch2_1080.m3u8', type: 'hls', logo: 'https://livetvali.neocities.org/1754740387347.jpg' },
    { name: 'live tv 3', quality: 'HD', url: 'https://stream.sainaertebat.com/hls2/tv3test.m3u8', type: 'hls', logo: 'https://livetvali.neocities.org/1754740387347.jpg' },
    { name: 'live tv 4', quality: 'HD', url: 'https://cdn.karwan.tv/nrt-sport/tracks-v1a1/mono.m3u8', type: 'hls', logo: 'https://livetvali.neocities.org/1754740387347.jpg' },
    { name: 'live tv 5', quality: 'HD', url: 'https://solhtvhls.wns.live/hls/stream.m3u8', type: 'hls', logo: 'https://livetvali.neocities.org/1754740387347.jpg' }
  ];

  function loadJSON(key,fallback){ try{ const v=localStorage.getItem(key); return v?JSON.parse(v):fallback;}catch(e){return fallback;} }
  function saveJSON(key,val){ try{ localStorage.setItem(key,JSON.stringify(val)); }catch(e){} }

  const container = document.getElementById('channelGrid');
  const searchInput = document.getElementById('searchInput');
  const tabChannels = document.getElementById('tabChannels');
  const tabMatches = document.getElementById('tabMatches');
  const tabNews = document.getElementById('tabNews');
  const tabHighlights = document.getElementById('tabHighlights');

  const matchesFrameContainer = document.getElementById('iframeContainer');
  const newsContainer = document.getElementById('newsContainer');
  const highlightsContainer = document.getElementById('highlightsContainer');

  const playerModal = document.getElementById('playerModal');
  const playerInner = document.getElementById('playerInner');
  const playerVideo = document.getElementById('playerVideo');
  const playerFrame = document.getElementById('playerFrame');
  const spinnerWrap = document.getElementById('playerSpinner');
  const spinnerText = document.getElementById('spinnerText');
  const btnClose = document.getElementById('btnClose');
  const fullscreenBtn = document.getElementById('fullscreenBtn');
  const shareChannelBtn = document.getElementById('shareChannelBtn');
  const playOverlay = document.getElementById('playOverlay');

  const matchesWatermark = document.getElementById('matchesWatermark');
  const newsWatermark = document.getElementById('newsWatermark');
  const highlightsWatermark = document.getElementById('highlightsWatermark');

  const toastEl = document.getElementById('toast');

  let lastOpenedChannelUrl = null;
  let lastOpenedChannelType = null;

  let favorites = loadJSON('ls_favs', []);
  function isFav(url){ return url && favorites.indexOf(url)!==-1; }
  function addFav(url){ if(!isFav(url)){ favorites.unshift(url); saveJSON('ls_favs',favorites); } }
  function removeFav(url){ const i=favorites.indexOf(url); if(i!==-1){ favorites.splice(i,1); saveJSON('ls_favs',favorites); } }
  function toggleFavByUrl(url){ if(isFav(url)) removeFav(url); else addFav(url); renderChannels(); }

  function sortedChannelsForRender(originalList){
    const favOrdered = favorites.map(u => originalList.find(ch => ch.url === u)).filter(Boolean);
    const remaining = originalList.filter(ch => !favorites.includes(ch.url));
    return favOrdered.concat(remaining);
  }

  function escapeHtml(s){ return (s+'').replace(/[&<>"']/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":"&#39;"}[c])); }

  function renderChannels(list = channels){
    const toRender = sortedChannelsForRender(list);
    container.innerHTML = '';
    toRender.forEach((ch, idx) => {
      const card = document.createElement('div');
      card.className = 'channel-card';
      card.setAttribute('data-url', ch.url || '');
      const logoSrc = ch.logo || 'https://livetvali.neocities.org/1754740387347.jpg';
      const hasUrl = !!ch.url;
      const qualityText = ch.quality ? escapeHtml(ch.quality) : `<span style="color:rgba(191,236,228,0.6)">فارغ</span>`;
      const actionBtn = hasUrl
        ? `<div style="margin-top:8px"><button class="play ripple" data-url="${encodeURIComponent(ch.url)}" data-type="${ch.type}">مشاهدة</button></div>`
        : `<div style="margin-top:8px"><button class="play" disabled>رابط غير مضاف</button></div>`;

      const logoClass = (/large\.jpg/i.test(logoSrc) || /spanish/i.test(ch.name)) ? 'logo spanish' : 'logo';

      card.innerHTML = `
        <button class="fav-btn ${hasUrl && isFav(ch.url)?'is-fav':''}" aria-label="إضافة للمفضلة">★</button>
        <div class="live-tag">${idx+1}</div>
        <img loading="lazy" class="${logoClass}" src="${logoSrc}" alt="logo">
        <h3>${escapeHtml(ch.name)}</h3>
        <p>${qualityText}</p>
        ${actionBtn}
      `;
      container.appendChild(card);
    });

    container.querySelectorAll('.play:not([disabled])').forEach(btn=>{
      btn.addEventListener('click',(e)=>{
        const url = decodeURIComponent(e.currentTarget.dataset.url);
        const type = e.currentTarget.dataset.type;
        openWithSpinner(url,type,false);
      });
    });

    container.querySelectorAll('.fav-btn').forEach(btn=>{
      btn.addEventListener('click',(e)=>{
        e.stopPropagation();
        const card = e.currentTarget.closest('.channel-card');
        const url = card.dataset.url;
        if(!url){
          showToast('لا يوجد رابط مضاف لهذه القناة.');
          return;
        }
        toggleFavByUrl(url);
      });
    });
  }

  function showToast(msg, ms=2000){
    toastEl.textContent = msg;
    toastEl.style.display = 'block';
    toastEl.style.opacity = '1';
    clearTimeout(toastEl._t);
    toastEl._t = setTimeout(()=>{ toastEl.style.opacity = '0'; setTimeout(()=> toastEl.style.display='none',300); }, ms);
  }

  function showSpinner(text='جارِ تحميل القناة...'){ spinnerText.textContent = text; if(spinnerWrap) spinnerWrap.style.display='flex'; }
  function hideSpinner(){ if(spinnerWrap) spinnerWrap.style.display='none'; }

  function openWithSpinner(url,type, fromShare=false){ showSpinner(); setTimeout(()=> openPlayer(url,type, fromShare),120); }

  /**
   * التغيير الرئيسي هنا: روابط .m3u8 (HLS) سيتم فتحها داخل الـ iframe (`playerFrame`)
   * بدلاً من استخدام عنصر <video> — كما طلبت أن تكون بنفس طريقة البقية (داخل نافذة القناة).
   */
  function openPlayer(url,type, fromShare=false){
    // تنظيف وضع التشغيل السابق
    try{ playerFrame.style.display='none'; playerFrame.src='about:blank'; }catch(e){}
    try{ playerVideo.style.display='none'; playerVideo.pause(); playerVideo.removeAttribute('src'); }catch(e){}
    playerVideo.muted = false;
    playOverlay.style.display = 'none';
    const maint = document.getElementById('maintMsg'); if(maint) maint.remove();

    playerModal.style.display='flex'; playerModal.setAttribute('aria-hidden','false');
    showSpinner();

    lastOpenedChannelUrl = url;
    lastOpenedChannelType = type;

    // زر المشاركة يشارك رابط داخل موقعك يؤدي لفتح القناة داخله
    if(shareChannelBtn){
      shareChannelBtn.style.display = 'inline-flex';
      shareChannelBtn.onclick = () => {
        const rawUrl = lastOpenedChannelUrl || url || '';
        if(!rawUrl){
          showToast('لا يوجد رابط لمشاركته.');
          return;
        }
        const pageUrl = location.origin + location.pathname + '?ch=' + encodeURIComponent(rawUrl);
        if(navigator.share){
          navigator.share({ url: pageUrl }).catch(()=> { copyToClipboard(pageUrl); showToast('تم نسخ رابط القناة'); });
        } else {
          copyToClipboard(pageUrl);
          showToast('تم نسخ رابط القناة');
        }
      };
    }

    const isYouTube = (type==='youtube' || /youtube\.com|youtu\.be/.test(url));
    if(isYouTube){
      // يظل سلوك الـ YouTube كما كان (embed)
      let embed = url;
      try{
        if(/watch\?v=/.test(url)) embed = `https://www.youtube.com/embed/${new URL(url).searchParams.get('v')}?rel=0&autoplay=1&controls=1`;
        else if(/youtu\.be\//.test(url)){ const m=url.match(/youtu\.be\/([^?&]+)/); if(m) embed=`https://www.youtube.com/embed/${m[1]}?rel=0&autoplay=1&controls=1`; }
      }catch(e){}
      playerFrame.src = embed;
      playerFrame.style.display='block';
      playerFrame.setAttribute('allow','autoplay; fullscreen');
      playerFrame.onload = ()=> hideSpinner();
      setTimeout(()=> hideSpinner(),9000);
      return;
    }

    // إذا الرابط ينتهي بـ .m3u8 — الآن نفتح داخل iframe كما طلبت
    if(/\.m3u8(\?|$)/i.test(url)){
      try{
        // ضع الرابط مباشرة في iframe (سيعمل إذا الخادم يدعم العرض داخل iframe أو توجد صفحة مشغّل)
        playerFrame.src = url;
        playerFrame.style.display='block';
        playerFrame.setAttribute('allow','autoplay; fullscreen');
        // عندما يحمل الإطار نغلق السبي ننر
        playerFrame.onload = ()=> { hideSpinner(); };
        // خطأ التحميل -> نظهر رسالة صيانة
        playerFrame.onerror = ()=> { hideSpinner(); showMaintenance('⚠️ تعذر تحميل القناة داخل النافذة.'); };
        // كاحتياط: بعد 9 ثواني نخفي المؤشر إن لم يصل حدث load
        setTimeout(()=> hideSpinner(),9000);
      }catch(err){
        hideSpinner();
        showMaintenance('⚠️ تعذر فتح الرابط داخل النافذة.');
      }
      return;
    }

    // الحالة الافتراضية: نفتح الرابط في iframe
    try{
      playerFrame.src = url;
      playerFrame.style.display='block';
      playerFrame.setAttribute('allow','autoplay; fullscreen');
      playerFrame.onload = ()=> hideSpinner();
      setTimeout(()=> hideSpinner(),9000);
    }catch(e){
      hideSpinner();
      showMaintenance('⚠️ تعذر فتح الرابط.');
    }
  }

  function showPlayOverlay(){
    playOverlay.style.display = 'flex';
    playOverlay.setAttribute('aria-hidden','false');
    const handler = async () => {
      try{
        playOverlay.style.display = 'none';
        playerVideo.muted = false;
        await playerVideo.play().catch(()=>{});
      }catch(e){}
      playOverlay.removeEventListener('click', handler);
    };
    playOverlay.addEventListener('click', handler);
  }

  function copyToClipboard(text){
    try{
      navigator.clipboard.writeText(text);
    }catch(e){
      const ta = document.createElement('textarea');
      ta.value = text;
      document.body.appendChild(ta);
      ta.select();
      try{ document.execCommand('copy'); }catch(_){}
      ta.remove();
    }
  }

  function showMaintenance(msg){
    hideSpinner();
    try{ playerVideo.style.display='none'; playerFrame.style.display='none'; }catch(e){}
    const existing = document.getElementById('maintMsg'); if(existing) existing.remove();
    const div = document.createElement('div');
    div.id = 'maintMsg';
    div.style.position = 'absolute';
    div.style.inset = '0';
    div.style.display = 'flex';
    div.style.alignItems = 'center';
    div.style.justifyContent = 'center';
    div.style.zIndex = '12900';
    div.style.color = '#fff';
    div.style.fontSize = '16px';
    div.style.padding = '16px';
    div.innerHTML = `<div style="background:rgba(0,0,0,0.6);padding:12px 16px;border-radius:10px;max-width:420px;text-align:center;">${msg}<br><span style="display:block;margin-top:8px;font-size:20px">🔧</span></div>`;
    playerInner.appendChild(div);
  }

  async function enterFullscreenAndLock(){
    try{ if(!document.fullscreenElement) await playerInner.requestFullscreen({ navigationUI: 'hide' }); if(screen.orientation && screen.orientation.lock){ try{ await screen.orientation.lock('landscape-primary'); }catch(e){ try{ await screen.orientation.lock('landscape'); }catch(_){} } } }catch(err){ console.warn(err); showToast('تعذّر الدخول بملء الشاشة.'); }
  }
  async function exitFullscreenAndUnlock(){ try{ if(document.fullscreenElement) await document.exitFullscreen(); if(screen.orientation && screen.orientation.unlock){ try{ screen.orientation.unlock(); }catch(e){} } }catch(err){ console.warn(err); } }
  function updateFullscreenButtonText(){ if(document.fullscreenElement) fullscreenBtn.textContent = 'خروج من ملء الشاشة'; else fullscreenBtn.textContent = 'ملء الشاشة'; }
  document.addEventListener('fullscreenchange', () => { updateFullscreenButtonText(); });
  fullscreenBtn.addEventListener('click', async ()=> { if(document.fullscreenElement) await exitFullscreenAndUnlock(); else await enterFullscreenAndLock(); updateFullscreenButtonText(); });

  function closePlayer(){
    try{ if(document.fullscreenElement) exitFullscreenAndUnlock(); }catch(e){}
    try{ playerFrame.src='about:blank'; playerFrame.style.display='none'; }catch(e){}
    try{ playerVideo.pause(); playerVideo.removeAttribute('src'); playerVideo.style.display='none'; }catch(e){}
    const m = document.getElementById('maintMsg'); if(m) m.remove();
    playOverlay.style.display = 'none';
    playerModal.style.display='none'; playerModal.setAttribute('aria-hidden','true'); hideSpinner();
  }
  btnClose.addEventListener('click', closePlayer);
  playerModal.addEventListener('click', (ev)=>{ if(ev.target===playerModal) closePlayer(); });
  window.addEventListener('keydown', (e)=>{ if(e.key==='Escape') closePlayer(); });

  function createMatchesIframe(){
    if(document.getElementById('matchesFrame')) return;
    matchesFrameContainer.style.position='relative';
    const f = document.createElement('iframe');
    f.id='matchesFrame';
    f.src=BTOLAT_URL;
    f.allowFullscreen=true; f.referrerPolicy='no-referrer';
    f.style.width='100%'; f.style.height='100%'; f.style.border='0'; f.style.background='transparent'; f.style.zIndex='1';
    matchesFrameContainer.innerHTML='';
    matchesFrameContainer.appendChild(f);
    if(matchesWatermark){ matchesWatermark.style.display='flex'; matchesFrameContainer.appendChild(matchesWatermark); }
    f.onload = ()=> { const el = document.getElementById('matchesLoadMsg'); if(el) el.remove(); };
    f.onerror = ()=> { const el = document.getElementById('matchesLoadMsg'); if(el) el.textContent = 'تعذر تحميل الجدول.'; setTimeout(()=>{ if(el) el.remove(); },3000); };
  }

  function createNewsIframe(){
    if(document.getElementById('newsFrame')) return;
    newsContainer.style.position='relative';
    const f = document.createElement('iframe');
    f.id='newsFrame';
    f.src=SPORT360_URL;
    f.allowFullscreen=true; f.referrerPolicy='no-referrer';
    f.style.width='100%'; f.style.height='100%'; f.style.border='0'; f.style.background='transparent'; f.style.zIndex='1';
    newsContainer.innerHTML='';
    newsContainer.appendChild(f);
    if(newsWatermark){ newsWatermark.style.display='flex'; newsContainer.appendChild(newsWatermark); }
    let timedOut=false;
    const t=setTimeout(()=>{ if(document.getElementById('newsFrame')){ } else { timedOut=true; newsContainer.innerHTML=''; const msg=document.createElement('div'); msg.style.padding='18px'; msg.style.textAlign='center'; msg.style.color='var(--muted)'; msg.innerHTML = `<div>يبدو أن الموقع يمنع التضمين داخل الإطار.</div><div style="margin-top:8px"><button id="openNewsNew" class="icon-btn">افتح الأخبار في نافذة جديدة</button></div>`; newsContainer.appendChild(msg); document.getElementById('openNewsNew').addEventListener('click', ()=> window.open(SPORT360_URL,'_blank','noopener')); } }, 3500);
    f.onload = ()=>{ clearTimeout(t); };
    f.onerror = ()=>{ clearTimeout(t); newsContainer.innerHTML=''; const msg=document.createElement('div'); msg.style.padding='18px'; msg.style.textAlign='center'; msg.style.color='var(--muted)'; msg.innerHTML=`<div>تعذر تحميل الأخبار داخل الإطار.</div><div style="margin-top:8px"><button id="openNewsNew2" class="icon-btn">افتح الأخبار في نافذة جديدة</button></div>`; newsContainer.appendChild(msg); document.getElementById('openNewsNew2').addEventListener('click', ()=> window.open(SPORT360_URL,'_blank','noopener')); };
  }

  function createHighlightsIframe(){
    if(document.getElementById('highlightsFrame')) return;
    highlightsContainer.style.position='relative';
    const f = document.createElement('iframe');
    f.id='highlightsFrame';
    f.src=HIGHLIGHTS_URL;
    f.allowFullscreen=true; f.referrerPolicy='no-referrer';
    f.style.width='100%'; f.style.height='100%'; f.style.border='0'; f.style.background='transparent'; f.style.zIndex='1';
    highlightsContainer.innerHTML='';
    highlightsContainer.appendChild(f);
    if(highlightsWatermark){ highlightsWatermark.style.display='flex'; highlightsContainer.appendChild(highlightsWatermark); }
    let timedOut=false;
    const t=setTimeout(()=>{ if(document.getElementById('highlightsFrame')){ } else { timedOut=true; highlightsContainer.innerHTML=''; const msg=document.createElement('div'); msg.style.padding='18px'; msg.style.textAlign='center'; msg.style.color='var(--muted)'; msg.innerHTML = `<div>يبدو أن الموقع يمنع التضمين داخل الإطار.</div><div style="margin-top:8px"><button id="openHighNew" class="icon-btn">افتح الملخصات في نافذة جديدة</button></div>`; highlightsContainer.appendChild(msg); document.getElementById('openHighNew').addEventListener('click', ()=> window.open(HIGHLIGHTS_URL,'_blank','noopener')); } }, 3500);
    f.onload = ()=>{ clearTimeout(t); };
    f.onerror = ()=>{ clearTimeout(t); highlightsContainer.innerHTML=''; const msg=document.createElement('div'); msg.style.padding='18px'; msg.style.textAlign='center'; msg.style.color='var(--muted)'; msg.innerHTML=`<div>تعذر تحميل الملخصات داخل الإطار.</div><div style="margin-top:8px"><button id="openHighNew2" class="icon-btn">افتح الملخصات في نافذة جديدة</button></div>`; highlightsContainer.appendChild(msg); document.getElementById('openHighNew2').addEventListener('click', ()=> window.open(HIGHLIGHTS_URL,'_blank','noopener')); };
  }

  tabChannels.addEventListener('click', ()=>{ tabChannels.classList.add('active'); tabMatches.classList.remove('active'); tabNews.classList.remove('active'); tabHighlights.classList.remove('active'); container.style.display='grid'; matchesFrameContainer.style.display='none'; newsContainer.style.display='none'; highlightsContainer.style.display='none'; document.getElementById('searchBar').style.display='block'; });
  tabMatches.addEventListener('click', ()=>{ tabMatches.classList.add('active'); tabChannels.classList.remove('active'); tabNews.classList.remove('active'); tabHighlights.classList.remove('active'); container.style.display='none'; matchesFrameContainer.style.display='block'; newsContainer.style.display='none'; highlightsContainer.style.display='none'; document.getElementById('searchBar').style.display='none'; createMatchesIframe(); });
  tabNews.addEventListener('click', ()=>{ tabNews.classList.add('active'); tabChannels.classList.remove('active'); tabMatches.classList.remove('active'); tabHighlights.classList.remove('active'); container.style.display='none'; matchesFrameContainer.style.display='none'; newsContainer.style.display='block'; highlightsContainer.style.display='none'; document.getElementById('searchBar').style.display='none'; createNewsIframe(); });
  tabHighlights.addEventListener('click', ()=>{ tabHighlights.classList.add('active'); tabChannels.classList.remove('active'); tabMatches.classList.remove('active'); tabNews.classList.remove('active'); container.style.display='none'; matchesFrameContainer.style.display='none'; newsContainer.style.display='none'; highlightsContainer.style.display='block'; document.getElementById('searchBar').style.display='none'; createHighlightsIframe(); });

  document.getElementById('iframePlaceholder').addEventListener('click', ()=> tabMatches.click());
  document.getElementById('newsPlaceholder').addEventListener('click', ()=> tabNews.click());
  document.getElementById('highlightsPlaceholder').addEventListener('click', ()=> tabHighlights.click());

  function debounce(fn, wait=180){ let t=null; return (...a)=>{ clearTimeout(t); t=setTimeout(()=> fn(...a), wait); }; }
  const doSearch = debounce(()=>{ const q=(searchInput.value||'').toLowerCase().trim(); renderChannels(channels.filter(c=> c.name.toLowerCase().includes(q))); }, 180);
  searchInput.addEventListener('input', doSearch);
  window.addEventListener('keydown', (e)=>{ if(e.key === '/') { e.preventDefault(); searchInput.focus(); searchInput.select(); } });

  document.getElementById('shareSite')?.addEventListener('click', async ()=>{
    const url = location.href;
    try{ if(navigator.share){ await navigator.share({ title:'لايف سبورت', url }); } else { await navigator.clipboard.writeText(url); showToast('تم نسخ الرابط'); } }catch(e){ try{ await navigator.clipboard.writeText(url); showToast('تم نسخ الرابط'); }catch(_){ showToast('تعذر المشاركة'); } }
  });

  document.getElementById('refreshBtn')?.addEventListener('click', ()=>{
    if(tabChannels.classList.contains('active')){
      renderChannels();
      try{ navigator.vibrate && navigator.vibrate(30); }catch(e){}
    } else if(tabMatches.classList.contains('active')){
      const mf = document.getElementById('matchesFrame');
      if(mf){ mf.src = mf.src; const overlay = document.createElement('div'); overlay.id='matchesReloadMsg'; overlay.style.position='absolute'; overlay.style.inset='0'; overlay.style.display='flex'; overlay.style.alignItems='center'; overlay.style.justifyContent='center'; overlay.style.color='var(--muted)'; overlay.style.zIndex=195; overlay.textContent='جارِ إعادة تحميل الجدول...'; matchesFrameContainer.appendChild(overlay); mf.onload = ()=> overlay.remove(); mf.onerror = ()=> { overlay.textContent='تعذر إعادة التحميل.'; setTimeout(()=> overlay.remove(),2500); }; } else { createMatchesIframe(); }
    } else if(tabNews.classList.contains('active')){
      const nf = document.getElementById('newsFrame');
      if(nf){ nf.src = nf.src; const overlay = document.createElement('div'); overlay.id='newsReloadMsg'; overlay.style.position='absolute'; overlay.style.inset='0'; overlay.style.display='flex'; overlay.style.alignItems='center'; overlay.style.justifyContent='center'; overlay.style.color='var(--muted)'; overlay.style.zIndex=195; overlay.textContent='جارِ إعادة تحميل الأخبار...'; newsContainer.appendChild(overlay); nf.onload = ()=> overlay.remove(); nf.onerror = ()=> { overlay.textContent='تعذر إعادة التحميل.'; setTimeout(()=> overlay.remove(),2500); }; } else { createNewsIframe(); }
    } else if(tabHighlights.classList.contains('active')){
      const hf = document.getElementById('highlightsFrame');
      if(hf){ hf.src = hf.src; const overlay = document.createElement('div'); overlay.id='highlightsReloadMsg'; overlay.style.position='absolute'; overlay.style.inset='0'; overlay.style.display='flex'; overlay.style.alignItems='center'; overlay.style.justifyContent='center'; overlay.style.color='var(--muted)'; overlay.style.zIndex=195; overlay.textContent='جارِ إعادة تحميل الملخصات...'; highlightsContainer.appendChild(overlay); hf.onload = ()=> overlay.remove(); hf.onerror = ()=> { overlay.textContent='تعذر إعادة التحميل.'; setTimeout(()=> overlay.remove(),2500); }; } else { createHighlightsIframe(); }
    }
  });

  function openChannelFromQuery(){
    const params = new URLSearchParams(location.search);
    const ch = params.get('ch');
    if(ch){
      try{
        const url = decodeURIComponent(ch);
        const found = channels.find(c => c.url === url);
        const type = found ? found.type : ( /\.m3u8(\?|$)/i.test(url) ? 'hls' : ( /youtube\.com|youtu\.be/.test(url) ? 'youtube' : '' ) );
        setTimeout(()=> openWithSpinner(url,type,true), 400);
      }catch(e){}
    }
  }

  const SPANISH_LOGO = 'https://livetvali.neocities.org/large.jpg';
  (new Image()).src = SPANISH_LOGO;
  channels.forEach(ch => { if(/spanish/i.test(ch.name)) ch.logo = SPANISH_LOGO; });

  document.addEventListener('DOMContentLoaded', ()=>{
    renderChannels();
    container.style.display='grid';
    matchesFrameContainer.style.display='none';
    newsContainer.style.display='none';
    highlightsContainer.style.display='none';
    tabChannels.classList.add('active');
    if(matchesWatermark) matchesWatermark.style.display='none';
    if(newsWatermark) newsWatermark.style.display='none';
    if(highlightsWatermark) highlightsWatermark.style.display='none';
    openChannelFromQuery();
  });
</script>

<!-- Default Statcounter code for live-tv-sport -->
<script type="text/javascript">
var sc_project=13158795; 
var sc_invisible=1; 
var sc_security="169ba464"; 
</script>
<script type="text/javascript" src="https://www.statcounter.com/counter/counter.js" async></script>
<noscript><div class="statcounter"><a title="Web Analytics Made Easy - Statcounter" href="https://statcounter.com/" target="_blank"><img class="statcounter" src="https://c.statcounter.com/13158795/0/169ba464/1/" alt="Web Analytics Made Easy - Statcounter" referrerPolicy="no-referrer-when-downgrade"></a></div></noscript>

</body>
</html>
