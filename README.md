<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="utf-8" />
  <title>📺 لايف سبورت</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <meta name="theme-color" content="#26A69A" />
  <!-- خط تاجيول -->
  <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@400;700;800&display=swap" rel="stylesheet">
  <style>
    /*
     * متغيرات CSS لسهولة التعديل على الألوان والثيمات
     * CSS variables for easy theming and color adjustments
     */
    :root{
      --accent:#566471;
      --accent-2:#8a99a6;
      --bg1:#f3f4f6;
      --bg2:#eef1f4;
      --glass: rgba(0,0,0,0.03);
      --text:#0b1720;
      --muted:#57606a;
      --max-width:980px;
      --card-radius:12px;
      --transition: 180ms cubic-bezier(.2,.9,.3,1);
      --iframe-shift: -120px;
      --tg-height:56px;
      --bar-height:48px;
      --live-dot:#ff5a5a;
      --close-default: rgba(229,57,53,0.95);
      --close-card-open: #1e88e5;
      --telegram:#0088cc;
    }
    [data-theme="dark"]{
      --accent:#26a69a;
      --accent-2:#34c89a;
      --bg1:#0b0f12;
      --bg2:#071018;
      --glass: rgba(255,255,255,0.02);
      --text:#e6fff8;
      --muted:#9fb7b0;
      --live-dot:#ff6b6b;
    }
    
    /* Global Styles */
    *{box-sizing:border-box}
    html,body{
      height:100%;
      margin:0;
      padding:0;
      padding-bottom:var(--bar-height); 
      background:linear-gradient(120deg,var(--bg1),var(--bg2));
      font-family:'Tajawal',sans-serif;
      color:var(--text);
      -webkit-font-smoothing:antialiased;
      overflow-x:hidden
    }
    a{color:var(--accent-2);text-decoration:none}
    body::before{
      content:"";
      position:fixed;
      inset:0;
      z-index:0;
      pointer-events:none;
      background:radial-gradient(600px 400px at 10% 10%, rgba(0,0,0,0.02), transparent),radial-gradient(400px 300px at 90% 80%, rgba(0,0,0,0.01), transparent);
      animation: bgMove 18s linear infinite;
      mix-blend-mode:normal;
      opacity:1
    }
    @keyframes bgMove{ from{transform:translateY(0)}50%{transform:translateY(-20px)}to{transform:translateY(0)} }

    /* Telegram Bar and Header - Updated */
    .telegram-bar{
      position:sticky;
      top:0;
      z-index:170;
      padding:8px 14px;
      display:flex;
      align-items:center;
      justify-content:space-between;
      background: linear-gradient(90deg,#2ea99a,#1f8f7f);
      color:#fff;
      font-weight:800;
      border-bottom:1px solid rgba(0,0,0,0.06);
      box-shadow:0 6px 18px rgba(0,0,0,0.12)
    }
    .tg-left{display:flex;align-items:center;gap:12px}
    .tg-left img{height:20px;width:20px;display:block}
    .tg-text{font-size:15px}
    .tg-handle{opacity:0.95;font-weight:700}
    
    /* Removed .tg-actions as per user request */

    header{
      position:sticky;
      top:var(--tg-height);
      z-index:160;
      padding:10px 16px;
      display:flex;
      align-items:center;
      gap:12px;
      justify-content:space-between;
      background: linear-gradient(90deg, rgba(3,6,9,0.88), rgba(3,6,9,0.45));
      border-bottom:1px solid rgba(255,255,255,0.03);
      backdrop-filter: blur(6px);
    } 
    .brand{display:flex;align-items:center;gap:12px}
    header img{max-width:86px;border-radius:10px;cursor:pointer;box-shadow:0 6-px 18px rgba(2,6,8,0.6)}
    header h1{font-size:20px;color:var(--accent-2);margin:0;font-weight:800;letter-spacing:0.6px}

    /*
     * Improved Search Bar Styling
     * تم تحسين تنسيق شريط البحث
     */
    .search-bar {
      position: relative;
      z-index: 50;
      max-width: var(--max-width);
      margin: 12px auto;
      padding: 0 16px;
    }
    #searchInput {
      width: 100%;
      padding: 12px 16px;
      border-radius: 12px; /* Increased border-radius for consistency */
      background: linear-gradient(180deg, rgba(255, 255, 255, 0.02), rgba(255, 255, 255, 0.01));
      border: 1px solid rgba(255, 255, 255, 0.04);
      color: var(--text);
      font-size: 16px;
      font-family: 'Tajawal', sans-serif;
      box-shadow: 0 8px 24px rgba(0, 0, 0, 0.45);
      transition: all var(--transition);
    }
    #searchInput:focus {
      outline: none;
      transform: translateY(-2px);
      box-shadow: 0 12px 36px rgba(0, 0, 0, 0.6);
    }

    /*
     * New CSS for vertical list and slim cards
     * تنسيقات جديدة للقوائم العمودية والبطاقات
     */
    .channel-list{
      display: flex;
      flex-direction: column;
      gap: 8px;
      padding: 10px;
      max-width: var(--max-width);
      margin: 12px auto 80px;
      position: relative;
      z-index: 20;
    }
    .channel-list .group-card {
      background: linear-gradient(180deg, rgba(255,255,255,0.012), rgba(255,255,255,0.006));
      border: 1px solid rgba(255,255,255,0.03);
      border-radius: 12px;
      padding: 12px;
      display: flex;
      align-items: center;
      gap: 16px;
      cursor: pointer;
      transition: transform .18s cubic-bezier(.2,.9,.3,1), box-shadow .18s;
      box-shadow: 0 8px 20px rgba(8,12,16,0.45);
    }
    .channel-list .group-card:hover{
      transform: translateY(-4px);
      box-shadow: 0 14px 36px rgba(8,12,16,0.5);
    }
    .channel-list .group-card img {
      width: 60px;
      height: 60px;
      object-fit: contain;
      border-radius: 8px;
    }

    /* Custom logo size for the new group */
    .channel-list .group-card.large-logo-group img {
      width: 80px;
      height: 80px;
    }

    .channel-list .group-card h3 {
      font-size: 18px;
      font-weight: 800;
      margin: 0;
      flex-grow: 1;
    }
    .channel-list .group-card .arrow {
      font-size: 24px;
      color: var(--muted);
      transition: transform 0.2s;
    }

    .channel-list .slim-card {
      background: linear-gradient(180deg, rgba(255,255,255,0.012), rgba(255,255,255,0.006));
      border: 1px solid rgba(255,255,255,0.03);
      border-radius: 12px;
      padding: 10px;
      display: flex;
      align-items: center;
      gap: 12px;
      cursor: pointer;
      transition: transform .18s cubic-bezier(.2,.9,.3,1), box-shadow .18s;
      box-shadow: 0 4px 12px rgba(8,12,16,0.3);
    }
    .channel-list .slim-card:hover{
      transform: translateY(-2px);
      box-shadow: 0 8px 24px rgba(8,12,16,0.4);
    }
    .channel-list .slim-card img {
      width: 48px;
      height: 48px;
      object-fit: contain;
      border-radius: 6px;
    }
    .channel-list .slim-card h4 {
      font-size: 16px;
      font-weight: 700;
      margin: 0;
      flex-grow: 1;
    }

    .live-tag{position:absolute;top:8px;left:8px;width:12px;height:12px;border-radius:50%;background:var(--live-dot);box-shadow:0 6px 18px rgba(0,0,0,0.4)}

    /* Player and Modals */
    #playerModal{position:fixed;inset:0;display:none;align-items:center;justify-content:center;background:linear-gradient(180deg, rgba(2,6,8,0.78), rgba(2,6,8,0.9));z-index:13000;padding:12px}
    #playerInner{width:100%;max-width:980px;height:56vh;background:#000;border-radius:12px;overflow:hidden;position:relative;box-shadow:0 20px 60px rgba(0,0,0,0.6);border:1px solid rgba(255,255,255,0.03);display:flex;flex-direction:column;align-items:stretch;transition:all 260ms ease}
    #playerInner iframe,#playerInner video{width:100%;height:100%;border:0;display:block;background:transparent;object-fit:contain}

    #qualityModal{ position:fixed; inset:0; display:none; align-items:center; justify-content:center; z-index:14000; background:rgba(2,6,8,0.75) }
    .quality-card{ width:420px; max-width:94%; padding:18px; border-radius:12px; background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01)); box-shadow:0 18px 48px rgba(0,0,0,0.6); text-align:center; color:var(--text) }
    .quality-card h3{margin:0 0 12px; font-weight:900}

    .source-actions{ 
      display:flex; 
      flex-direction:column; 
      gap:8px;
      align-items:stretch; 
      width:100% 
    }
    .source-actions .src{ 
      padding:10px 12px;
      border-radius:999px; 
      font-weight:800; 
      font-size:14px;
      border:0; 
      cursor:pointer; 
      box-shadow:0 8px 20px rgba(2,6,8,0.45);
      transition:transform var(--transition); 
      display:flex; 
      align-items:center; 
      justify-content:center; 
      gap:10px;
    }
    .source-actions .src img { 
      height: 48px;
      width: 48px; 
      border-radius: 6px; 
      object-fit: contain; 
    }
    .source-actions .src.color-1{ background: linear-gradient(90deg,#34c89a,#26a69a); color:#071014 }
    .source-actions .src.color-2{ background: linear-gradient(90deg,#90caf9,#6ec6ff); color:#021826 }
    .source-actions .src.color-3{ background: linear-gradient(90deg,#ffa726,#ffb74d); color:#071014 }
    .source-actions .src.color-4{ background: linear-gradient(90deg,#b39ddb,#9575cd); color:#071014 }
    .source-actions .src.color-5{ background: linear-gradient(90deg,#e57373,#ef5350); color:#071014 }
    .source-actions .src.color-6{ background: linear-gradient(90deg,#ff6b6b,#ff8e8e); color:#071014 }
    .source-actions .src.fb{ background: linear-gradient(90deg,#3b5998,#4c66a4); color:#fff; }

    .close-q{ 
      margin-top:12px; 
      background: #e53935;
      border:1px solid rgba(255,255,255,0.06); 
      padding:8px 12px; 
      border-radius:8px; 
      cursor:pointer; 
      color:#fff;
      font-weight: bold;
    }
    
    /* Player Controls - Updated */
    .controls-row{
      position:absolute;
      left:12px;
      top:12px;
      z-index:12111;
      display:flex;
      gap:8px
    }
    .player-control{
      background:linear-gradient(90deg, #1e88e5, #2196F3);
      border:none;
      padding:8px 10px;
      border-radius:10px;
      color:#fff;
      font-weight:700;
      cursor:pointer;
      transition:all var(--transition)
    }
    /* Removed .share-channel as per user request */
    .btn-close{
      position:absolute; 
      top:12px; 
      right:12px; 
      z-index:13010;
      background:var(--close-default); 
      color:#fff; 
      border:none; 
      padding:8px 10px; 
      border-radius:10px; 
      font-weight:800; 
      cursor:pointer
    }

    /* Spinner */
    .spinner-wrap{position:absolute;inset:0;display:none;align-items:center;justify-content:center;z-index:12102;background:linear-gradient(180deg, rgba(0,0,0,0.18), rgba(0,0,0,0.28));pointer-events:none}
    .spinner-circle{width:46px;height:46px;border-radius:50%;border:5px solid rgba(255,255,255,0.06);border-top-color:var(--accent);animation:spin 1s linear infinite;margin-bottom:8px}
    @keyframes spin{from{transform:rotate(0)}to{transform:rotate(360deg)}}

    /* Toast notification */
    #toast { position:fixed; left:50%; transform:translateX(-50%); bottom:calc(var(--bar-height) + 12px); z-index:14000; background:rgba(0,0,0,0.6); color:#fff; padding:10px 14px; border-radius:10px; font-weight:700; display:none }

    /*
     * Portrait Mode for Fullscreen
     * الوضع الطولي لملء الشاشة
     */
    body.portrait-mode .telegram-bar,
    body.portrait-mode header,
    body.portrait-mode .search-bar,
    body.portrait-mode .channel-list,
    body.portrait-mode .dev-contacts { display:none !important; }

    body.portrait-mode #playerModal {
        display: flex !important;
        background: black;
        padding: 0;
        z-index: 15000;
    }

    body.portrait-mode #playerInner {
        position: fixed;
        inset: 0;
        width: 100vw;
        height: 100vh;
        max-width: unset;
        max-height: unset;
        border-radius: 0;
        box-shadow: none;
        border: none;
        transform: none;
    }

    body.portrait-mode #playerInner iframe,
    body.portrait-mode #playerInner video {
        object-fit: contain;
        width: 100%;
        height: 100%;
    }

    body.portrait-mode .player-control,
    body.portrait-mode .btn-close {
      background: rgba(0, 0, 0, 0.4);
      color: #fff;
    }

    @media (max-width: 520px){
      body.portrait-mode #playerInner {
        width: 100vw;
        height: 100vh;
        border-radius: 0;
      }
      .channel-list{ grid-template-columns:repeat(auto-fit,minmax(140px,1fr)); }
    }

    /*
     * Unlock Overlay
     * شاشة القفل
     */
    #unlockOverlay{position:fixed;inset:0;z-index:22000;display:flex;align-items:center;justify-content:center;background:linear-gradient(135deg,rgba(0,0,0,0.85),rgba(0,0,0,0.9));backdrop-filter:blur(4px)}
    #unlockBox{width:92%;max-width:420px;background:linear-gradient(180deg,#ffffff,#f7fafb);padding:22px;border-radius:14px;text-align:center;box-shadow:0 18px 60px rgba(2,6,8,0.6);border:1px solid rgba(0,0,0,0.04)}
    #unlockBox h2{margin:0 0 10px;font-weight:900;font-size:20px;color:var(--accent-2)}
    #unlockBox p{margin:0 0 14px;color:var(--muted);font-size:14px}
    #unlockInput{width:100%;padding:12px;border-radius:10px;border:1px solid rgba(0,0,0,0.06);margin-bottom:14px;font-size:15px;text-align:center;background:transparent}
    .unlockBtns{display:flex;gap:10px}
    .unlockBtns button{flex:1;padding:12px;border-radius:10px;border:0;color:#fff;font-weight:800;font-size:15px;cursor:pointer}
    #unlockBtn{background:linear-gradient(90deg,var(--accent-2),var(--accent))}
    #overlayTelegram{background:var(--telegram)}
    #unlockOverlay[hidden]{display:none}

  </style>
</head>
<body>
  <div id="unlockOverlay" aria-hidden="false">
    <div id="unlockBox" role="dialog" aria-modal="true" aria-label="قفل الموقع">
      <h2>🔒 الموقع محمي</h2>
      <p>أدخل الكود المنشور في قناتنا التلجرام 🔴🔴الكود الحالي.(2025)
      <input id="unlockInput" type="text" placeholder="أدخل الرمز هنا" aria-label="رمز الفتح">
      <div class="unlockBtns">
        <button id="unlockBtn">فتح</button>
        <button id="overlayTelegram">التليجرام</button>
      </div>
    </div>
  </div>  
  <div id="siteContent" style="display:none">
    <div class="telegram-bar" role="note" aria-label="رابط قناة التليجرام الرسمية">
      <div class="tg-left">
        <img src="https://upload.wikimedia.org/wikipedia/commons/8/82/Telegram_logo.svg" alt="تلغرام" />
        <div>
          <div class="tg-text">قناة التليجرام الرسمية</div>
          <small class="tg-handle">@alialiah123456</small>
        </div>
      </div>
      <!--
        تم حذف زر "نسخ" و "المبرمجون" بناءً على طلبك
        Removed "copy" and "dev contacts" buttons as per your request
      -->
    </div>
    <header>
      <div class="brand">
        <img id="brandLogo" src="https://livetvali.neocities.org/1754740387347.jpg" alt="لوغو لايف سبورت" />
        <h1>لايف سبورت ⚽</h1>
      </div>
      <!--
        تم حذف أزرار المشاركة والتحديث بناءً على طلبك
        Removed "share" and "refresh" buttons as per your request
      -->
      <div class="controls">
        <button id="themeToggle" class="icon-btn" title="الوضع الليلي/النهاري" aria-pressed="false">🌙</button>
      </div>
    </header>

    <div class="search-bar" id="searchBar">
      <input id="searchInput" type="text" placeholder="🔍 ابحث عن مجموعة قنوات..." aria-label="ابحث عن مجموعة قنوات" />
    </div>

    <section id="channelList" class="channel-list" aria-live="polite"></section>

    <div id="playerModal" aria-hidden="true">
      <div id="playerInner" role="dialog" aria-modal="true" aria-label="مشغل القناة">
        <div class="controls-row">
          <!--
            تم حذف زر المشاركة من المشغل بناءً على طلبك
            Removed share button from player as per your request
          -->
          <button id="fullscreenBtn" class="player-control ripple" title="ملء الشاشة">ملء الشاشة</button>
        </div>
        <button id="btnClose" class="btn-close" title="إغلاق">إغلاق</button>
        <div class="spinner-wrap" id="playerSpinner" aria-hidden="false">
          <div style="display:flex;flex-direction:column;align-items:center;justify-content:center;color:#e6fff8">
            <div class="spinner-circle" role="status" aria-label="جار التحميل"></div>
            <div id="spinnerText">جارِ تحميل القناة...</div>
          </div>
        </div>
        <video id="playerVideo" playsinline controls style="display:none;pointer-events:auto;background:#000"></video>
        <iframe id="playerFrame" allow="autoplay; fullscreen" style="display:none;pointer-events:none"></iframe>
      </div>
    </div>

    <div id="qualityModal" role="dialog" aria-modal="true" style="display:none">
      <div class="quality-card" role="document">
        <h3 id="qualityChannelName">اختر القناة</h3>
        <div class="source-actions" id="sourceActions"></div>
        <button id="closeQuality" class="close-q">إلغاء</button>
      </div>
    </div>

    <div id="toast" role="status" aria-live="polite"></div>

    <script>
      // =========================================================================================
      // 🛠️  اعدادات القنوات والبيانات - يمكنك تعديل الروابط والمصادر من هنا  🛠️
      // =========================================================================================
      
      /**
       * تعليمات إضافة قنوات جديدة:
       * 1. للعثور على قنوات جديدة، ابحث عن ملفات m3u8.
       * 2. يمكنك تعديل أي من المجموعات أدناه.
       * 3. لإضافة قناة جديدة، أضف كائنًا جديدًا (Object) داخل مصفوفة `channels` في المجموعة المطلوبة.
       * 4. يجب أن يحتوي الكائن على حقلين: `name` (اسم القناة) و `sources` (مصفوفة الروابط).
       * 5. داخل مصفوفة `sources`, أضف كائنًا جديدًا لكل مصدر، يحتوي على `name` (اسم المصدر) و `url` (رابط البث).
       * 6. **لإضافة لوغو مخصص لقناة معينة، أضف حقل `logo` إلى كائن القناة.**
       * * مثال: `{ name: 'قناتي الخاصة', logo: 'رابط-اللوغو.png', sources: [...] }`
       * * إذا لم يتم تحديد `logo` للقناة، سيتم استخدام لوغو المجموعة الافتراضي.
       * * ملاحظة: المجموعات التي تحتوي على `sourcesOnly: true` ستعرض المصادر مباشرة عند الضغط عليها.
       * */
      
      const CHANNEL_GROUPS = [
        {
          name: 'beIN Sports HD',
          logo: 'https://ysygjsusah.neocities.org/Utool-20250819-185249015.png',
          channels: [
            { 
              name: 'beIN SPORTS 1', 
              sources: [
                { name: 'المصدر الأول', url: 'https://stream.supertv.gg:3001/supertv/sport/stv1/ch1/ch1_1080.m3u8' },
                { name: 'المصدر الثاني', url: 'https://wo.cma.footballii.ir/hls2/b1_src.m3u8' }
              ] 
            },
            { 
              name: 'beIN SPORTS 2', 
              sources: [
                { name: 'المصدر الأول', url: 'https://stream.supertv.gg:3002/supertv/sport/stv2/ch2/ch2_1080.m3u8' },
                { name: 'المصدر الثاني', url: 'https://stream.supertv.gg:3002/supertv/sport/stv2/ch2/ch2_720.m3u8' }
              ] 
            },
            { 
              name: 'beIN SPORTS 3', 
              sources: [
                { name: 'المصدر الأول', url: 'https://stream.supertv.gg:3003/supertv/sport/stv3/ch3/ch3_1080.m3u8' },
                { name: 'المصدر الثاني', url: 'https://wo.cma.footballii.ir/hls2/b3.m3u8' }
              ] 
            },
            { 
              name: 'beIN SPORTS 4', 
              sources: [
                { name: 'المصدر الأول', url: 'https://stream.supertv.gg:3004/supertv/sport/stv4/ch4/ch4_1080.m3u8' },
                { name: 'المصدر الثاني', url: 'https://your-second-link-here.com' }
              ] 
            },
            { 
              name: 'beIN SPORTS 5', 
              sources: [
                { name: 'المصدر الأول', url: 'https://stream.supertv.gg:3005/supertv/sport/stv5/ch5/ch5_1080.m3u8' },
                { name: 'المصدر الثاني', url: 'https://your-second-link-here.com' }
              ] 
            },
            { 
              name: 'beIN SPORTS 6', 
              sources: [
                { name: 'المصدر الأول', url: 'https://stream.supertv.gg:3006/supertv/sport/stv6/ch6/ch6_1080.m3u8' },
                { name: 'المصدر الثاني', url: 'https://your-second-link-here.com' }
              ] 
            },
            {
              name: 'beIN SPORTS 7',
              logo: 'https://placehold.co/60x60/34c89a/ffffff?text=B7',
              sources: [
                { name: 'المصدر الأول', url: 'https://your-new-link-for-beIN-7.com/stream.m3u8' }
              ]
            }
          ]
        },
        {
          name: 'bilN Sports SD',
          logo: 'https://ysygjsusah.neocities.org/Utool-20250819-185249015.png',
          channels: [
            {
              name: 'beIN SPORTS SD 1',
              sources: [
                { name: 'المصدر الأول', url: 'https://stream.supertv.gg:3001/supertv/sport/stv1/ch1/ch1_360.m3u8' }
              ]
            },
            {
              name: 'beIN SPORTS SD 2',
              sources: [
                { name: 'المصدر الأول', url: 'https://stream.supertv.gg:3002/supertv/sport/stv2/ch2/ch2_720.m3u8' }
              ]
            },
            {
              name: 'beIN SPORTS SD 3',
              sources: [
                { name: 'المصدر الأول', url: 'https://stream.supertv.gg:3003/supertv/sport/stv3/ch3/ch3_720.m3u8' }
              ]
            },
            {
              name: 'beIN SPORTS SD 4',
              sources: [
                { name: 'المصدر الأول', url: 'https://stream.supertv.gg:3004/supertv/sport/stv4/ch4/ch4_720.m3u8' }
              ]
            },
            {
              name: 'beIN SPORTS SD 5',
              sources: [
                { name: 'المصدر الأول', url: 'https://stream.supertv.gg:3005/supertv/sport/stv5/ch5/ch5_720.m3u8' }
              ]
            },
            {
              name: 'beIN SPORTS SD 6',
              sources: [
                { name: 'المصدر الأول', url: 'https://stream.supertv.gg:3006/supertv/sport/stv6/ch6/ch6_720.m3u8' }
              ]
            }
          ]
        },
        {
          name: 'الدوري النجليزي',
          logo: 'https://ysygjsusah.neocities.org/Utool-20250818-034801096.png',
          sourcesOnly: true, // تفعيل الانتقال المباشر للمصادر
          channels: [
            {
              name: 'الدوري النجليزي',
              sources: [
                { name: 'NRT ', url: 'https://cdn.karwan.tv/nrt-sport/tracks-v1a1/mono.m3u8', logo:'https://ysygjsusah.neocities.org/Utool-20250819-185418477.png' },
                { name: 'Solhtfils ', url: 'https://solhtvhls.wns.live/hls/stream.m3u8', logo:'https://ysygjsusah.neocities.org/Utool-20250819-185334901.png' },
                { name: 'bilN sport', url: 'https://stream.supertv.gg:3001/supertv/sport/stv1/ch1/ch1_1080.m3u8', logo:'https://ysygjsusah.neocities.org/Utool-20250819-185249015.png' },
                { name: 'بديل bilN sport ', url: 'https://stream.live12.ir/hls2/bein1.m3u8', logo:'https://ysygjsusah.neocities.org/Utool-20250819-185249015.png' }
              ]
            }
          ]
        },
        {
          name: 'الدوري الاسباني',
          logo:'https://ysygjsusah.neocities.org/Utool-20250818-034854385.png',
          sourcesOnly: true, // تفعيل الانتقال المباشر للمصادر
          channels: [
            {
              name: 'الدوري الاسباني',
              sources: [
                { name: 'NRT ', url: 'https://cdn.karwan.tv/nrt-sport/tracks-v1a1/mono.m3u8', logo:'https://ysygjsusah.neocities.org/Utool-20250819-185418477.png' },
                { name: 'Solhtfils ', url: 'https://solhtvhls.wns.live/hls/stream.m3u8', logo:'https://ysygjsusah.neocities.org/Utool-20250819-185334901.png' },
                { name: 'bilN sport', url: 'https://stream.supertv.gg:3003/supertv/sport/stv3/ch3/ch3_1080.m3u8', logo:'https://ysygjsusah.neocities.org/Utool-20250819-185249015.png' }
              ]
            }
          ]
        },
        {
          name: 'الدوري الايطالي ',
          logo: 'https://i.ibb.co/HDhVfYvs/1000013586.png',
          sourcesOnly: true, // تفعيل الانتقال المباشر للمصادر
          channels: [
            {
              name: 'الدوري الايطالي ',
              sources: [
                { name: '1 ابو ظبي', url: 'https://vo-live.cdb.cdn.orange.com/Content/Channel/AbuDhabiSportsChannel1/HLS/index.m3u8', logo:'https://i.ibb.co/20wyYBHj/1000013584.png' },
                { name: 'ابو ظبي 2', url: 'https://vo-live-media.cdb.cdn.orange.com/Content/Channel/AbuDhabiSportsChannel2/HLS/index.m3u8', logo:'https://i.ibb.co/vtHLSP3/1000013585.png' }
              ]
            }
          ]
        },
        {
          name: 'الدوري السعودي',
          logo: 'https://i.ibb.co/WWZcYQ3k/1000013587.png',
          sourcesOnly: true, // تفعيل الانتقال المباشر للمصادر
          channels: [
            {
              name: 'الدوري السعودي',
              sources: [
                { name: 'الثامنه', url: 'https://your-premierleague-stream-link.m3u8' }
              ]
            }
          ]
        },
        {
          name: 'الدوري الفرنسي',
          logo: 'https://i.ibb.co/sdKDq9cC/1000013588.png',
          sourcesOnly: true, // تفعيل الانتقال المباشر للمصادر
          channels: [
            {
              name: 'الدوري الفرنسي',
              sources: [
                { name: 'bilN Sport HD', url: 'https://stream.supertv.gg:3004/supertv/sport/stv4/ch4/ch4_1080.m3u8', logo:'https://ysygjsusah.neocities.org/Utool-20250819-185249015.png' },
                { name: 'bilN sport SD', url: 'https://stream.supertv.gg:3004/supertv/sport/stv4/ch4/ch4_720.m3u8', logo:'https://ysygjsusah.neocities.org/Utool-20250819-185249015.png' }
              ]
            }
          ]
        },
        {
          name: 'قنوات لايف تي في',
          logo: 'https://ysygjsusah.neocities.org/Utool-20250818-031400368.png',
          channels: [
            { 
              name: 'Live Tv 1', 
              sources: [
                { name: 'المصدر الأول', url: 'https://stream.supertv.gg:3001/supertv/sport/stv1/ch1/ch1_360.m3u8' },
                { name: 'المصدر الثاني', url: 'https://your-second-link-here.com' }
              ] 
            },
            { 
              name: 'Live Tv 2', 
              sources: [
                { name: 'المصدر الأول', url: 'https://stream.supertv.gg:3002/supertv/sport/stv2/ch2/ch2_720.m3u8' },
                { name: 'المصدر الثاني', url: 'https://your-second-link-here.com' }
              ] 
            },
            { 
              name: 'Live Tv 3', 
              sources: [
                { name: 'المصدر الأول', url: 'https://stream.supertv.gg:3003/supertv/sport/stv3/ch3/ch3_720.m3u8' },
                { name: 'المصدر الثاني', url: 'https://your-second-link-here.com' }
              ] 
            },
            { 
              name: 'Live Tv 4', 
              sources: [
                { name: 'المصدر الأول', url: 'https://stream.supertv.gg:3004/supertv/sport/stv4/ch4/ch4_720.m3u8' },
                { name: 'المصدر الثاني', url: 'https://your-second-link-here.com' }
              ] 
            },
            { 
              name: 'Live Tv 5', 
              sources: [
                { name: 'المصدر الأول', url: 'https://stream.supertv.gg:3005/supertv/sport/stv5/ch5/ch5_720.m3u8' },
                { name: 'المصدر الثاني', url: 'https://your-second-link-here.com' }
              ] 
            },
            { 
              name: 'Live Tv 6', 
              sources: [
                { name: 'المصدر الأول', url: 'https://stream.supertv.gg:3006/supertv/sport/stv6/ch6/ch6_720.m3u8' },
                { name: 'المصدر الثاني', url: 'https://your-second-link-here.com' }
              ] 
            }
          ]
        }
      ];

      // إعدادات أخرى
      const TELEGRAM_HANDLE = '@alialiah123456';

      // ===========================================
      // ⚠️ لا تعدل الكود أسفل هذا الخط إلا إذا كنت تعرف ما تفعله
      // ===========================================

      const channelGroups = CHANNEL_GROUPS;

      const listContainer = document.getElementById('channelList');
      const searchInput = document.getElementById('searchInput');

      const playerModal = document.getElementById('playerModal');
      const playerInner = document.getElementById('playerInner');
      const playerVideo = document.getElementById('playerVideo');
      const playerFrame = document.getElementById('playerFrame');
      const spinnerWrap = document.getElementById('playerSpinner');
      const spinnerText = document.getElementById('spinnerText');
      const btnClose = document.getElementById('btnClose');
      const fullscreenBtn = document.getElementById('fullscreenBtn');

      const qualityModal = document.getElementById('qualityModal');
      const qualityChannelName = document.getElementById('qualityChannelName');
      const sourceActionsEl = document.getElementById('sourceActions');
      const closeQualityBtn = document.getElementById('closeQuality');

      const toastEl = document.getElementById('toast');
      const telegramBar = document.querySelector('.telegram-bar');

      let lastOpenedChannelUrl = null;
      let lastOpenedChannelType = null;

      // لتتبع حالة الـ qualityModal
      let currentModalView = 'groups'; // 'groups', 'channels', 'sources'

      function showToast(msg, ms=2200){
        toastEl.textContent = msg; toastEl.style.display = 'block'; toastEl.style.opacity = '1';
        clearTimeout(toastEl._t); toastEl._t = setTimeout(()=>{ toastEl.style.opacity='0'; setTimeout(()=> toastEl.style.display='none',300); }, ms);
      }
      function escapeHtml(s){ return (s+'').replace(/[&<>\"']/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','\"':'&quot;',"'":"&#39;"}[c])); }
      
      // Function to render the main channel groups
      function renderChannelGroups(list = channelGroups){
        listContainer.innerHTML = '';
        list.forEach((group, idx) => {
          const groupCard = document.createElement('div');
          groupCard.className = 'group-card';
          // Add a special class for the group with the larger logo
          if (group.name === 'قنوات الدوريات العالمية') {
            groupCard.classList.add('large-logo-group');
          }
          groupCard.innerHTML = `
            <img loading="lazy" src="${escapeHtml(group.logo)}" alt="logo" />
            <h3>${escapeHtml(group.name)}</h3>
            <span class="arrow">›</span>
          `;
          
          if (group.sourcesOnly) {
            // New logic: Directly open sources for these specific groups
            groupCard.addEventListener('click', () => {
                if (group.channels && group.channels.length > 0) {
                    renderSourcesForChannel(group.channels[0], group.logo);
                    qualityModal.style.display = 'flex';
                }
            });
          } else {
            // Original logic: Open the channel list for other groups
            groupCard.addEventListener('click', () => {
              renderChannelsInGroup(group);
            });
          }
          listContainer.appendChild(groupCard);
        });
      }

      // Modified function to render channels within a selected group
      function renderChannelsInGroup(group) {
        currentModalView = 'channels';
        qualityChannelName.textContent = group.name;
        sourceActionsEl.innerHTML = '';
        closeQualityBtn.style.display = 'block';

        group.channels.forEach((channel, srcIndex) => {
          if(!channel.sources || channel.sources.length === 0) return;
          const btn = document.createElement('button');
          btn.className = 'src';
          
          const colorClassIndex = (srcIndex % 6) + 1;
          btn.classList.add(`color-${colorClassIndex}`);
          
          // Use the channel's specific logo if available, otherwise use the group's logo
          const channelLogo = channel.logo || group.logo;
          if(channelLogo){
            const img = document.createElement('img');
            img.src = escapeHtml(channelLogo);
            img.alt = '';
            btn.appendChild(img);
          }
          const span = document.createElement('span');
          span.textContent = escapeHtml(channel.name);
          btn.appendChild(span);
          
          btn.addEventListener('click', () => {
            if (channel.sources.length > 1) {
              // Pass the channel's logo to the next function
              renderSourcesForChannel(channel, channel.logo || group.logo);
            } else {
              qualityModal.style.display = 'none';
              openWithSpinner(channel.sources[0].url, 'hls');
            }
          });
          sourceActionsEl.appendChild(btn);
        });

        qualityModal.style.display = 'flex';
      }

      // Modified function to render sources for a specific channel
      function renderSourcesForChannel(channel, channelLogo) {
        currentModalView = 'sources';
        qualityChannelName.textContent = channel.name;
        sourceActionsEl.innerHTML = '';
        closeQualityBtn.style.display = 'block'; // Make sure the main close button is visible

        channel.sources.forEach((source, srcIndex) => {
          const btn = document.createElement('button');
          btn.className = 'src';
          const colorClassIndex = (srcIndex % 6) + 1;
          btn.classList.add(`color-${colorClassIndex}`);
          
          // Use the source's specific logo if available, otherwise use the channel/group logo
          const logoToUse = source.logo || channelLogo;
          if(logoToUse){
            const img = document.createElement('img');
            img.src = escapeHtml(logoToUse);
            img.alt = '';
            btn.appendChild(img);
          }
          const span = document.createElement('span');
          span.textContent = escapeHtml(source.name);
          btn.appendChild(span);
          
          btn.addEventListener('click', () => {
            qualityModal.style.display = 'none';
            openWithSpinner(source.url, 'hls');
          });
          sourceActionsEl.appendChild(btn);
        });
      }


      let retryTimer = null;
      let retryAttempt = 0;
      const MAX_RETRY_ATTEMPTS = 8;
      const BASE_RETRY_DELAY = 1200;

      function showSpinner(text='جارِ تحميل القناة...'){ spinnerText.textContent = text; if(spinnerWrap) spinnerWrap.style.display='flex'; }
      function hideSpinner(){ if(spinnerWrap) spinnerWrap.style.display='none'; }

      function clearRetry(){
        if(retryTimer) { clearTimeout(retryTimer); retryTimer = null; }
        retryAttempt = 0;
        try{ playerVideo.removeEventListener('error', onVideoError); playerVideo.removeEventListener('playing', onVideoPlaying); playerVideo.removeEventListener('stalled', onVideoStalled); }catch(e){}
      }

      function scheduleRetry(url){
        clearRetry();
        retryAttempt++;
        if(retryAttempt > MAX_RETRY_ATTEMPTS){
          hideSpinner();
          showToast('تعذّر تحميل البث (حاول لاحقاً).');
          return;
        }
        const delay = Math.min(BASE_RETRY_DELAY * Math.pow(1.5, retryAttempt-1), 8000);
        retryTimer = setTimeout(()=> { tryPlayM3U8(url); }, delay);
      }

      function tryPlayM3U8(url){
        try{ playerVideo.pause(); }catch(e){}
        try{ playerVideo.removeAttribute('src'); playerVideo.src = url; playerVideo.load(); }catch(e){}
        playerVideo.muted = true;
        const playPromise = playerVideo.play();
        if(playPromise && typeof playPromise.then === 'function'){
          playPromise.then(()=> {
            playerVideo.muted = false;
            hideSpinner();
          }).catch(()=> { scheduleRetry(url); });
        } else {
          scheduleRetry(url);
        }
      }

      function onVideoError(){ if(lastOpenedChannelUrl) scheduleRetry(lastOpenedChannelUrl); }
      function onVideoStalled(){ if(lastOpenedChannelUrl) scheduleRetry(lastOpenedChannelUrl); }
      function onVideoPlaying(){ hideSpinner(); try{ playerVideo.muted = false; }catch(e){} clearRetry(); }

      function openWithSpinner(url,type){ showSpinner(); setTimeout(()=> openPlayer(url,type),120); }

      function openPlayer(url,type){
        try{ playerFrame.src='about:blank'; playerFrame.style.display='none'; }catch(e){}
        try{ playerVideo.pause(); playerVideo.removeAttribute('src'); playerVideo.style.display='none'; }catch(e){}
        playerVideo.style.display='none';
        clearRetry();

        playerModal.style.display='flex'; playerModal.setAttribute('aria-hidden','false');
        showSpinner();

        lastOpenedChannelUrl = url;
        lastOpenedChannelType = type;
        
        // Removed share channel button functionality
        
        if(/\.m3u8(\?|$)/i.test(url)){
          playerVideo.addEventListener('error', onVideoError);
          playerVideo.addEventListener('stalled', onVideoStalled);
          playerVideo.addEventListener('playing', onVideoPlaying);
          playerVideo.style.display = 'block';
          playerVideo.controls = true;
          retryAttempt = 0;
          tryPlayM3U8(url);
          return;
        }

        const isYouTube = (type==='youtube' || /youtube\.com|youtu\.be/.test(url));
        if(isYouTube){
          let embed = url;
          try{
            if(/watch\?v=/.test(url)) embed = `https://www.youtube.com/embed/${new URL(url).searchParams.get('v')}?rel=0&autoplay=1&controls=1`;
            else if(/youtu\.be\//.test(url)){ const m=url.match(/youtu\.be\/([^?&]+)/); if(m) embed=`https://www.youtube.com/embed/${m[1]}?rel=0&autoplay=1&controls=1`; }
          }catch(e){}
          playerFrame.src = embed;
          playerFrame.style.display='block';
          playerFrame.onload = ()=> hideSpinner();
          return;
        }

        if(/facebook\.com/i.test(url) || /^https?:\/\//i.test(url)){
          hideSpinner();
          window.open(url, '_blank');
          showToast('تم فتح المصدر في نافذة جديدة');
          playerModal.style.display='none'; playerModal.setAttribute('aria-hidden','true');
          return;
        }

        try{
          playerFrame.src = url;
          playerFrame.style.display='block';
          playerFrame.onload = ()=> hideSpinner();
        }catch(e){
          hideSpinner();
          showToast('تعذّر فتح الرابط.');
        }
      }

      function copyToClipboard(text){ try{ navigator.clipboard.writeText(text); }catch(e){ const ta = document.createElement('textarea'); ta.value = text; document.body.appendChild(ta); ta.select(); try{ document.execCommand('copy'); }catch(_){ } ta.remove(); } }

      let isPortraitMode = false;
      function enterPortraitMode(){
        if(isPortraitMode) return;
        document.body.classList.add('portrait-mode');
        if(playerModal.style.display !== 'flex'){
          playerModal.style.display = 'flex';
          playerModal.setAttribute('aria-hidden','false');
        }
        fullscreenBtn.textContent = 'خروج من الملء';
        isPortraitMode = true;
      }
      function exitPortraitMode(){
        if(!isPortraitMode) return;
        document.body.classList.remove('portrait-mode');
        fullscreenBtn.textContent = 'ملء الشاشة';
        isPortraitMode = false;
      }
      function togglePortraitMode(){
        if(isPortraitMode) exitPortraitMode();
        else enterPortraitMode();
      }

      fullscreenBtn.addEventListener('click', (e)=>{
        e.preventDefault();
        togglePortraitMode();
      });

      function closePlayer(){
        try{ playerFrame.src='about:blank'; playerFrame.style.display='none'; }catch(e){}
        try{ playerVideo.pause(); playerVideo.removeAttribute('src'); playerVideo.style.display='none'; }catch(e){}
        playerModal.style.display='none'; playerModal.setAttribute('aria-hidden','true'); hideSpinner();
        clearRetry();
        try{ btnClose.style.background = getComputedStyle(document.documentElement).getPropertyValue('--close-default') || 'rgba(229,57,53,0.95)'; }catch(e){}
        exitPortraitMode();
      }
      btnClose.addEventListener('click', closePlayer);
      playerModal.addEventListener('click', (ev)=>{ if(ev.target===playerModal) closePlayer(); });

      window.addEventListener('keydown', (e)=>{
        if(e.key==='Escape'){
          if(qualityModal.style.display==='flex'){ qualityModal.style.display='none'; }
          else if(isPortraitMode){ exitPortraitMode(); }
          else closePlayer();
        }
      });

      function debounce(fn, wait=180){ let t=null; return (...a)=>{ clearTimeout(t); t=setTimeout(()=> fn(...a), wait); }; };
      const doSearch = debounce(()=>{
        const q=(searchInput.value||'').toLowerCase().trim();
        renderChannelGroups(channelGroups.filter(g => g.name.toLowerCase().includes(q) || g.channels.some(c => c.name.toLowerCase().includes(q))));
      }, 180);
      searchInput.addEventListener('input', doSearch);
      window.addEventListener('keydown', (e)=>{ if(e.key === '/') { e.preventDefault(); searchInput.focus(); searchInput.select(); } });

      // Removed share site and refresh buttons as per user request

      if (telegramBar) {
        telegramBar.addEventListener('click', (e) => {
          // If the user clicks on the telegram bar (but not a link), open the telegram channel
          const tgUrl = 'https://t.me/alialiah123456';
          try {
            window.open(tgUrl, '_blank', 'noopener');
            showToast('فتح قناة التليجرام');
          } catch (err) {
            location.href = tgUrl;
          }
        });
      }

      closeQualityBtn.addEventListener('click', () => {
        qualityModal.style.display = 'none';
        closeQualityBtn.style.display = 'block'; // Ensure it is visible for next time
      });

      function openChannelFromQuery(){ const params = new URLSearchParams(location.search); const ch = params.get('ch'); if(ch){ try{ const url = decodeURIComponent(ch); setTimeout(()=> openWithSpinner(url, /\.m3u8(\?|$)/i.test(url)?'hls':( /youtube\.com|youtu\.be/.test(url)?'youtube':'' )), 400); }catch(e){} } }
      
      const themeToggle = document.getElementById('themeToggle');
      function applyTheme(theme){ document.documentElement.setAttribute('data-theme', theme); localStorage.setItem('ls_theme', theme); themeToggle.setAttribute('aria-pressed', theme==='dark' ? 'true' : 'false'); themeToggle.textContent = theme==='dark' ? '☀️' : '🌙'; }
      function initTheme(){ const saved = localStorage.getItem('ls_theme'); if(saved){ applyTheme(saved); return; } const prefersDark = window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches; applyTheme(prefersDark ? 'dark' : 'light'); }
      themeToggle.addEventListener('click', ()=>{ const current = document.documentElement.getAttribute('data-theme') || 'light'; applyTheme(current === 'dark' ? 'light' : 'dark'); });

      document.addEventListener('DOMContentLoaded', ()=>{
        renderChannelGroups();
        initTheme(); // Initialize theme on load
      });
    </script>
  </div>

  <script>
    /****************************************************
     ✨ مهم: لتغيير الكود يومياً عدّل قيمة SITE_UNLOCK_CODE أدناه
     وضع الرمز الذي تنشره في قناتكم على التليجرام.
     ****************************************************/
    const SITE_UNLOCK_CODE = '2025';

    function initSiteLockGlobal(){
      const overlay = document.getElementById('unlockOverlay');
      const siteContent = document.getElementById('siteContent');
      const unlockInput = document.getElementById('unlockInput');
      const unlockBtn = document.getElementById('unlockBtn');
      const overlayTelegramBtn = document.getElementById('overlayTelegram');

      function lockIsActive(){ return typeof SITE_UNLOCK_CODE === 'string' && SITE_UNLOCK_CODE.trim().length>0; }

      try{
        if(sessionStorage.getItem('site_unlocked') === '1' && lockIsActive()){
          overlay.style.display = 'none';
          overlay.setAttribute('aria-hidden','true');
          siteContent.style.display = '';
        }
      }catch(e){}

      unlockBtn.addEventListener('click', ()=>{
        const val = (unlockInput.value||'').trim();
        if(!lockIsActive()){
          alert('⚠️ لم يتم إعداد رمز الفتح. قم بتعديل SITE_UNLOCK_CODE داخل الكود.');
          return;
        }
        if(val === SITE_UNLOCK_CODE){
          overlay.style.display = 'none';
          overlay.setAttribute('aria-hidden','true');
          siteContent.style.display = '';
          try{ sessionStorage.setItem('site_unlocked','1'); }catch(e){}
        } else {
          alert('❌ رمز غير صحيح');
          unlockInput.value = '';
          try{ unlockInput.focus(); }catch(e){}
        }
      });

      unlockInput.addEventListener('keydown', (e)=>{ if(e.key === 'Enter') unlockBtn.click(); });

      overlayTelegramBtn.addEventListener('click', ()=>{
        try{ window.open('https://t.me/alialiah123456', '_blank', 'noopener'); }catch(e){ location.href = 'https://t.me/alialiah123456'; }
      });
    }

    document.addEventListener('DOMContentLoaded', initSiteLockGlobal);
  </script>
  <!-- Default Statcounter code for live tv apk
  https://ysygjsusah.neocities.org/ -->
  <script type="text/javascript">
  var sc_project=13161346; 
  var sc_invisible=1; 
  var sc_security="b45ced0e"; 
  </script>
  <script type="text/javascript"
  src="https://www.statcounter.com/counter/counter.js"
  async></script>
  <noscript><div class="statcounter"><a title="Web Analytics"
  href="https://statcounter.com/" target="_blank"><img
  class="statcounter"
  src="https://c.statcounter.com/13161346/0/b45ced0e/1/"
  alt="Web Analytics"
  referrerPolicy="no-referrer-when-downgrade"></a></div></noscript>
  <!-- End of Statcounter Code -->
</body>
</html>
