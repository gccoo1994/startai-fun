# StartAI.fun

AI 工具导航网站 - 完整源码

> 在线访问：https://startai.fun

## 项目简介

StartAI.fun 是一个 AI 工具导航站，帮助用户从零开始掌握 AI 工具的使用。

网站采用五步学习路径设计：
1. 领养 AI 工具（入门工具推荐）
2. 喂养数据（API 与数据源）
3. 教技能（Prompt 与训练）
4. 配装备（MCP 等扩展）
5. 找伙伴（Multi-Agent 协作）

## 文件说明

本项目为单页应用（SPA），所有内容均在以下 HTML 文件中：

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>AI 上手指南 — 5步从零掌握 AI</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+SC:wght@300;400;500;600;700;800;900&family=Inter:wght@400;500;600;700;800;900&display=swap" rel="stylesheet">
<style>
*,*::before,*::after{margin:0;padding:0;box-sizing:border-box}
:root{
  --bg:#F7F8FA;--bg2:#FFFFFF;--bg3:#F0F1F3;
  --tx1:#111318;--tx2:#555D6B;--tx3:#9AA0AB;
  --bd:#E2E4E9;--bd2:#ECEEF2;
  --g1:#00C853;--g2:#00E676;--g3:#E8F5E9;
  --b1:#2979FF;--b2:#448AFF;--b3:#E3F2FD;
  --p1:#7C4DFF;--p2:#B388FF;--p3:#EDE7F6;
  --o1:#FF6D00;--o2:#FF9100;--o3:#FFF3E0;
  --k1:#FFD600;--k3:#FFFDE7;
  --r1:#FF1744;--r3:#FFEBEE;
  --t1:#00BFA5;--t3:#E0F2F1;
  --sh1:0 1px 3px rgba(0,0,0,.04);--sh2:0 4px 16px rgba(0,0,0,.06);--sh3:0 12px 40px rgba(0,0,0,.08);--sh4:0 16px 48px rgba(0,0,0,.10);
  --r1r:10px;--r2r:14px;--r3r:18px;--r4r:24px;--rf:999px;
}
html{scroll-behavior:smooth}
body{font-family:'Noto Sans SC','Inter',-apple-system,sans-serif;background:var(--bg);color:var(--tx1);line-height:1.6;-webkit-font-smoothing:antialiased;overflow-x:hidden}

/* NAV */
nav{position:sticky;top:0;z-index:100;background:rgba(247,248,250,.88);backdrop-filter:blur(20px) saturate(180%);border-bottom:1px solid var(--bd2);transition:box-shadow .3s}
nav.scrolled{box-shadow:var(--sh2)}
.ni{max-width:1160px;margin:0 auto;padding:0 28px;height:60px;display:flex;align-items:center;justify-content:space-between}
.nl{display:flex;align-items:center;gap:10px;text-decoration:none;font-weight:800;font-size:16px;color:var(--tx1)}
.nl-i{width:30px;height:30px;border-radius:8px;background:linear-gradient(135deg,var(--g1),var(--t1));display:flex;align-items:center;justify-content:center;color:#fff;font-size:14px;font-weight:800}
.nsteps{display:flex;gap:2px;background:var(--bg3);border-radius:var(--rf);padding:3px}
.nsteps a{padding:6px 14px;border-radius:var(--rf);font-size:12.5px;font-weight:600;color:var(--tx3);text-decoration:none;transition:all .25s;white-space:nowrap}
@media(hover:hover){.nsteps a:hover{color:var(--tx2);background:var(--bg2)}}

/* HERO */
.hero{max-width:1160px;margin:0 auto;padding:88px 28px 64px;text-align:center;position:relative}
.hd{position:absolute;pointer-events:none;border-radius:50%}
.hd1{width:180px;height:180px;background:radial-gradient(circle,rgba(0,200,83,.07) 0%,transparent 70%);top:10px;right:40px}
.hd2{width:100px;height:100px;background:radial-gradient(circle,rgba(124,77,255,.06) 0%,transparent 70%);bottom:60px;left:60px;border-radius:30%;transform:rotate(25deg)}
.hd3{width:40px;height:40px;border-radius:10px;background:var(--o1);opacity:.10;top:180px;left:14%}
.hd4{width:28px;height:28px;border-radius:50%;background:var(--p1);opacity:.12;bottom:90px;right:16%}

.hb{display:inline-flex;align-items:center;gap:7px;padding:5px 14px 5px 7px;border-radius:var(--rf);background:var(--g3);color:var(--g1);font-size:12.5px;font-weight:700;margin-bottom:24px}
.hb-d{width:20px;height:20px;border-radius:50%;background:var(--g1);display:flex;align-items:center;justify-content:center;font-size:10px;color:#fff}
.hero h1{font-size:clamp(32px,5vw,52px);font-weight:900;line-height:1.15;letter-spacing:-.02em;margin-bottom:16px}
.hero h1 em{font-style:normal;background:linear-gradient(135deg,var(--g1),var(--t1));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text}
.hero>p{font-size:17px;color:var(--tx2);max-width:580px;margin:0 auto 48px;line-height:1.7}

/* TIMELINE */
.tl{display:flex;gap:8px;justify-content:center;flex-wrap:wrap;margin-bottom:12px}
.ts{display:flex;align-items:center;gap:10px}
.ts-n{width:36px;height:36px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:14px;font-weight:800;flex-shrink:0}
.ts-c{font-size:14px;font-weight:600;color:var(--tx2);text-align:left}
.ts-c small{display:block;font-size:11px;color:var(--tx3);font-weight:400;margin-top:1px}
.tl-div{width:40px;height:2px;background:var(--bd);margin:0 4px;align-self:center;flex-shrink:0}
.n1{background:var(--g1);color:#fff}.n2{background:var(--b1);color:#fff}.n3{background:var(--p1);color:#fff}.n4{background:var(--o1);color:#fff}.n5{background:var(--k1);color:var(--tx1)}

.hsub{font-size:13px;color:var(--tx3);margin-top:8px}
.hsub span{color:var(--g1);font-weight:600}

/* SECTION */
.sec{max-width:1160px;margin:0 auto;padding:72px 28px}
.sec-hd{margin-bottom:40px}
.stag{display:inline-flex;align-items:center;gap:6px;padding:4px 12px;border-radius:var(--rf);font-size:11.5px;font-weight:700;letter-spacing:.04em;margin-bottom:14px}
.stg1{background:var(--g3);color:var(--g1)}.stg2{background:var(--b3);color:var(--b1)}.stg3{background:var(--p3);color:var(--p1)}.stg4{background:var(--o3);color:var(--o1)}.stg5{background:var(--k3);color:#F9A825}
.stit{font-size:clamp(24px,3.5vw,36px);font-weight:800;letter-spacing:-.02em;margin-bottom:8px}
.sdesc{font-size:15px;color:var(--tx2);max-width:520px;line-height:1.7}

/* STEP NOTE */
.snote{display:flex;align-items:flex-start;gap:14px;padding:20px 24px;background:var(--bg2);border-radius:var(--r3r);border:1px solid var(--bd2);margin-bottom:32px}
.snote-ico{width:40px;height:40px;border-radius:10px;display:flex;align-items:center;justify-content:center;font-size:18px;flex-shrink:0}
.snote-txt{font-size:14px;color:var(--tx2);line-height:1.7}
.snote-txt strong{color:var(--tx1);font-weight:700}

/* CARDS */
.cg{display:grid;grid-template-columns:repeat(auto-fill,minmax(300px,1fr));gap:16px}
.c{background:var(--bg2);border-radius:var(--r3r);border:1px solid var(--bd2);padding:24px;transition:all .35s cubic-bezier(.25,.46,.45,.94);position:relative;overflow:hidden;display:flex;flex-direction:column}
@media(hover:hover){.c:hover{box-shadow:var(--sh4);transform:translateY(-3px);border-color:transparent}}
.c:active{box-shadow:var(--sh4);transform:translateY(-1px);border-color:transparent}
.ca{position:absolute;top:0;left:0;right:0;height:3px}
.ci{width:44px;height:44px;border-radius:var(--r2r);display:flex;align-items:center;justify-content:center;font-size:20px;margin-bottom:14px}
.cn{font-size:16px;font-weight:700;margin-bottom:4px;display:flex;align-items:center;gap:8px;flex-wrap:wrap}
.cbn{font-size:9.5px;font-weight:700;padding:2px 7px;border-radius:var(--rf);letter-spacing:.03em}
.bh{background:var(--r3);color:var(--r1)}.bn{background:var(--g3);color:var(--g1)}.bf{background:var(--b3);color:var(--b1)}.bc{background:var(--o3);color:var(--o1)}.bo{background:var(--p3);color:var(--p1)}.br{background:var(--k3);color:#F9A825}
.cd{font-size:13px;color:var(--tx2);line-height:1.65;margin-bottom:14px;flex:1}
.ct{display:flex;flex-wrap:wrap;gap:5px;margin-bottom:14px}
.ctg{font-size:10.5px;padding:2px 9px;border-radius:var(--rf);background:var(--bg);color:var(--tx3);font-weight:500}
.cl{display:inline-flex;align-items:center;gap:5px;font-size:13px;font-weight:600;color:var(--g1);text-decoration:none;transition:gap .2s;flex-shrink:0}
@media(hover:hover){.cl:hover{gap:9px}}
.cl:visited{color:var(--g1)}

/* LINK CARDS (API providers — more compact, link-focused) */
.lcg{display:grid;grid-template-columns:repeat(auto-fill,minmax(260px,1fr));gap:12px}
.lc{display:flex;align-items:center;gap:14px;padding:16px 20px;background:var(--bg2);border-radius:var(--r2r);border:1px solid var(--bd2);transition:all .3s;text-decoration:none;color:inherit;cursor:pointer}
@media(hover:hover){.lc:hover{box-shadow:var(--sh3);transform:translateY(-2px);border-color:transparent}}
.lc:active{box-shadow:var(--sh3);transform:translateY(-1px);border-color:transparent}
.lc-av{width:36px;height:36px;border-radius:9px;display:flex;align-items:center;justify-content:center;font-size:14px;font-weight:800;color:#fff;flex-shrink:0}
.lc-info{flex:1;min-width:0}
.lc-name{font-size:14px;font-weight:700;display:flex;align-items:center;gap:6px}
.lc-desc{font-size:12px;color:var(--tx3);white-space:nowrap;overflow:hidden;text-overflow:ellipsis;margin-top:2px}
.lc-arrow{color:var(--tx3);font-size:16px;flex-shrink:0;transition:all .2s}
@media(hover:hover){.lc:hover .lc-arrow{color:var(--g1);transform:translateX(3px)}}

/* SECTION DIVIDER */
.sdiv{max-width:1160px;margin:0 auto;padding:0 28px}
.sdiv-inner{height:1px;background:linear-gradient(90deg,transparent 0%,var(--bd) 20%,var(--bd) 80%,transparent 100%)}

/* CTA */
.cta-wrap{max-width:760px;margin:72px auto;padding:0 28px}
.cta-card{background:var(--tx1);border-radius:var(--r4r);padding:56px 44px;text-align:center;position:relative;overflow:hidden}
.cta-card h2{font-size:28px;font-weight:800;color:#fff;margin-bottom:10px}
.cta-card p{font-size:15px;color:rgba(255,255,255,.6);margin-bottom:28px;max-width:440px;margin-left:auto;margin-right:auto}
.cta-btn{display:inline-flex;align-items:center;gap:7px;padding:13px 28px;border-radius:var(--rf);background:var(--g1);color:#fff;font-size:14px;font-weight:700;text-decoration:none;border:none;cursor:pointer;transition:all .25s;font-family:inherit}
@media(hover:hover){.cta-btn:hover{background:var(--g2);transform:translateY(-2px);box-shadow:0 8px 24px rgba(0,200,83,.3)}}
.cta-btn:active{background:var(--g2);transform:translateY(-1px)}
.ccf{position:absolute;pointer-events:none}
.ccf1{width:70px;height:70px;border-radius:50%;background:rgba(0,200,83,.12);top:-15px;right:50px}
.ccf2{width:45px;height:45px;border-radius:10px;background:rgba(124,77,255,.12);bottom:-8px;left:60px;transform:rotate(18deg)}
.ccf3{width:25px;height:25px;border-radius:50%;background:rgba(255,109,0,.15);top:25px;left:30px}

/* FOOTER */
footer{border-top:1px solid var(--bd2);padding:36px 28px;text-align:center;color:var(--tx3);font-size:12.5px}
footer a{color:var(--tx2);text-decoration:none}

/* ANIM */
@keyframes fiu{from{opacity:0;transform:translateY(20px)}to{opacity:1;transform:translateY(0)}}
.ai{opacity:0;animation:fiu .55s ease-out forwards}
.d1{animation-delay:.08s}.d2{animation-delay:.16s}.d3{animation-delay:.24s}.d4{animation-delay:.32s}.d5{animation-delay:.4s}

/* DEV ENTRY BUTTON */
.dev-entry{display:inline-flex;align-items:center;gap:5px;padding:6px 14px;border-radius:var(--rf);background:var(--tx1);color:#fff;font-size:12px;font-weight:600;text-decoration:none;transition:all .25s;letter-spacing:.01em}
@media(hover:hover){.dev-entry:hover{background:#2A2D35;transform:translateY(-1px);box-shadow:0 4px 12px rgba(0,0,0,.15)}}
.dev-entry:active{background:#2A2D35;transform:translateY(-1px)}

/* RESPONSIVE */
@media(max-width:768px){
  .nsteps{display:none}
  .hero{padding:56px 20px 40px}
  .tl{flex-direction:column;align-items:center}
  .tl-div{width:2px;height:20px;margin:0}
  .sec{padding:48px 20px}
  .cg,.lcg{grid-template-columns:1fr}
  .cta-card{padding:36px 20px}
}

/* P0 QUESTIONNAIRE - 浮窗模式 */
.p0-overlay{position:fixed;top:0;left:0;right:0;bottom:0;z-index:2000;display:flex;align-items:center;justify-content:center;background:rgba(17,19,24,.6);backdrop-filter:blur(12px);-webkit-backdrop-filter:blur(12px)}
.p0-overlay.hidden{display:none}
.p0-wrap{width:100%;max-width:520px;padding:20px}
.p0-card{background:#fff;border-radius:var(--r4r);border:1px solid var(--bd2);padding:36px 32px;position:relative;overflow:hidden;box-shadow:0 24px 80px rgba(0,0,0,.25)}
.p0-card::before{content:'';position:absolute;top:0;left:0;right:0;height:4px;background:linear-gradient(90deg,var(--g1),var(--t1),var(--b1))}
.p0-header{text-align:center;margin-bottom:24px}
.p0-header h2{font-size:20px;font-weight:800;margin-bottom:4px}
.p0-header p{font-size:12px;color:var(--tx3)}
.p0-progress{display:flex;justify-content:center;gap:6px;margin-bottom:20px}
.p0-dot{width:10px;height:10px;border-radius:50%;background:var(--bd);transition:all .3s}
.p0-dot.active{background:var(--g1);transform:scale(1.3)}
.p0-dot.done{background:var(--g1)}
.p0-question{display:none}
.p0-question.active{display:block;animation:fiu .35s ease-out}
.p0-q-num{font-size:12px;font-weight:600;color:var(--tx3);text-align:center;margin-bottom:8px}
.p0-q-num span{color:var(--b1);font-weight:700}
.p0-q-title{font-size:16px;font-weight:700;margin-bottom:18px;text-align:center;color:var(--tx1);line-height:1.5}
.p0-q-note{font-size:11px;color:var(--tx3);text-align:center;margin-top:-10px;margin-bottom:14px;font-style:italic}
.p0-options{display:flex;flex-direction:column;gap:10px}
.p0-opt{padding:14px 18px;background:var(--bg);border:2px solid var(--bd2);border-radius:var(--r2r);cursor:pointer;transition:all .15s;font-size:14px;color:var(--tx2);text-align:left}
@media(hover:hover){.p0-opt:hover{border-color:var(--g1);background:var(--g3)}}
.p0-opt:active{border-color:var(--g1);background:var(--g3)}
.p0-opt.selected{border-color:var(--g1);background:var(--g3);color:var(--g1);font-weight:600}
.p0-nav{display:flex;justify-content:center;margin-top:20px}
.p0-btn-skip{background:transparent;color:var(--tx3);border:none;font-size:12px;padding:6px 12px;cursor:pointer;transition:color .2s;font-family:inherit}
@media(hover:hover){.p0-btn-skip:hover{color:var(--tx2);text-decoration:underline}}

/* USER ID BADGE */
.user-badge{position:fixed;bottom:20px;right:20px;background:var(--bg2);border:1px solid var(--bd2);border-radius:var(--r2r);padding:10px 16px;font-size:12px;color:var(--tx3);box-shadow:var(--sh2);z-index:1000;display:flex;align-items:center;gap:8px}
.user-badge span{color:var(--b1);font-weight:600;font-family:monospace}

@media(max-width:768px){
  .p0-card{padding:32px 24px}
  .user-badge{font-size:10px;padding:8px 12px}
}
.page-content{transition:filter .3s}
.page-content.blurred{filter:blur(8px);pointer-events:none}

/* MULTI-COLUMN TABLE STYLES - 真正的表格布局 */
.data-table{width:100%;border-collapse:collapse;background:var(--bg);border-radius:var(--r3r);overflow:hidden;border:1px solid var(--bd2)}
.data-table thead{display:table-header-group;background:var(--bg)}
.data-table th{padding:12px 16px;text-align:left;font-size:12px;font-weight:700;color:var(--tx3);border-bottom:1px solid var(--bd2);letter-spacing:.02em}
.data-table tbody tr{cursor:pointer;transition:all .3s cubic-bezier(.25,.46,.45,.94);height:56px}
.data-table tbody tr:nth-child(odd){background:var(--bg)}
.data-table tbody tr:nth-child(even){background:var(--bg2)}
@media(hover:hover){.data-table tbody tr:hover{background:var(--g3);box-shadow:inset 3px 0 0 var(--g1)}}
.data-table tbody tr:active{background:var(--g3)}
.data-table td{padding:12px 16px;border-bottom:1px solid var(--bd2);vertical-align:middle}
.data-table tbody tr:last-child td{border-bottom:none}
.data-table td.ico{width:44px;padding:8px 12px}
.data-table td.ico span{display:inline-flex;width:32px;height:32px;border-radius:8px;align-items:center;justify-content:center;font-size:14px;font-weight:700}
.data-table td.name{font-weight:700;color:var(--tx1);min-width:100px}
.data-table td.name .cbn{margin-left:6px}
.data-table td.desc{color:var(--tx3);font-size:13px;line-height:1.4}
.data-table td.price{color:var(--g1);font-weight:600;white-space:nowrap}
.data-table td.promo{font-size:12px;color:var(--o1)}
.data-table td.note{font-size:12px;color:var(--tx3)}
@media(hover:hover){.data-table tbody tr:hover td.name{color:var(--g1)}}

@media(max-width:1024px){
  .data-table{overflow-x:auto;-webkit-overflow-scrolling:touch;display:block}
  .data-table thead,.data-table tbody{display:table;width:100%}
  .data-table tr{display:table-row}
  .data-table th,.data-table td{display:table-cell}
}

@media(max-width:768px){
  .data-table th,.data-table td{padding:10px 12px;font-size:12px}
  .data-table td.ico{padding:6px 8px}
  .data-table td.desc{max-width:120px;overflow:hidden;text-overflow:ellipsis}
  .data-table{overflow-x:auto;-webkit-overflow-scrolling:touch;display:block}
  .data-table thead,.data-table tbody{display:table;width:100%}
  .data-table tr{display:table-row}
  .data-table th,.data-table td{display:table-cell}
}
</style>
</head>
<body>

<!-- P0 QUESTIONNAIRE OVERLAY - 浮窗在最上层，不受虚化影响 -->
<div class="p0-overlay" id="p0Overlay">
  <div class="p0-wrap">
    <div class="p0-card">
      <div class="p0-header">
        <h2>🎯 帮我了解你</h2>
        <p>回答几个问题，推荐最适合你的 AI 入门路径</p>
      </div>
      
      <div class="p0-progress">
        <div class="p0-dot active" data-q="1"></div>
        <div class="p0-dot" data-q="2"></div>
        <div class="p0-dot" data-q="3"></div>
        <div class="p0-dot" data-q="4"></div>
      </div>

      <!-- Question 1/4 -->
      <div class="p0-question active" data-question="1">
        <div class="p0-q-num"><span>1</span> / 4</div>
        <div class="p0-q-title">你现在最希望 AI 先帮你做什么？</div>
        <div class="p0-options">
          <div class="p0-opt" data-value="time" onclick="selectOption(this)">让我现在的工作/学习更省时间</div>
          <div class="p0-opt" data-value="content" onclick="selectOption(this)">帮我尝试内容创作或副业机会</div>
          <div class="p0-opt" data-value="learn" onclick="selectOption(this)">让我系统学会 AI，做更复杂的事</div>
          <div class="p0-opt" data-value="explore" onclick="selectOption(this)">我还不确定，我先看看它能为我做什么</div>
        </div>
      </div>

      <!-- Question 2/4 -->
      <div class="p0-question" data-question="2">
        <div class="p0-q-num"><span>2</span> / 4</div>
        <div class="p0-q-title">你现在离真正开始用 AI，还有多远？</div>
        <div class="p0-options">
          <div class="p0-opt" data-value="ready" onclick="selectOption(this)">我已经有明确想做的事，只差开始</div>
          <div class="p0-opt" data-value="direction" onclick="selectOption(this)">我有一些方向，但还不知道怎么落地</div>
          <div class="p0-opt" data-value="unclear" onclick="selectOption(this)">我还不清楚 AI 具体能帮我做什么</div>
        </div>
      </div>

      <!-- Question 3/4 -->
      <div class="p0-question" data-question="3">
        <div class="p0-q-num"><span>3</span> / 4</div>
        <div class="p0-q-title">你更想用哪种方式开始？</div>
        <div class="p0-options">
          <div class="p0-opt" data-value="simple" onclick="selectOption(this)">越简单越好，最好马上就能试</div>
          <div class="p0-opt" data-value="stable" onclick="selectOption(this)">可以多一点设置，只要更稳定</div>
          <div class="p0-opt" data-value="power" onclick="selectOption(this)">可以折腾一点，我想要更强能力</div>
        </div>
      </div>

      <!-- Question 4/4 (Optional) -->
      <div class="p0-question" data-question="4">
        <div class="p0-q-num"><span>4</span> / 4</div>
        <div class="p0-q-note">（此题可以不回答）</div>
        <div class="p0-q-title">前期需要一点成本，你能接受吗？</div>
        <div class="p0-options">
          <div class="p0-opt" data-value="free" onclick="selectOption(this)">只想先免费试</div>
          <div class="p0-opt" data-value="low" onclick="selectOption(this)">可以接受少量花费</div>
          <div class="p0-opt" data-value="any" onclick="selectOption(this)">只要值得，成本不是主要问题</div>
        </div>
      </div>

      <div class="p0-nav">
        <button class="p0-btn p0-btn-skip" onclick="skipP0()">跳过</button>
      </div>
    </div>
  </div>
</div>

<!-- 页面内容容器 - 可以被虚化 -->
<div class="page-content" id="pageContent">

<!-- NAV -->
<nav id="nav">
  <div class="ni">
    <a href="#" class="nl"><div class="nl-i">AI</div>StartAI</a>
    <div class="nsteps">
      <a href="#step1">①领养</a>
      <a href="#step2">②喂养</a>
      <a href="#step3">③技能</a>
      <a href="#step4">④装备</a>
      <a href="#step5">⑤找个新伙伴</a>
    </div>
    <a href="dev.html" class="dev-entry" title="开发者中心">⚙️ 开发者中心</a>
  </div>
</nav>

<!-- HERO -->
<section class="hero">
  <div class="hd hd1"></div><div class="hd hd2"></div><div class="hd hd3"></div><div class="hd hd4"></div>
  <div class="ai"><div class="hb"><span class="hb-d">✦</span>用养宠物的思路理解 AI · 2026 持续更新</div></div>
  <h1 class="ai d1">5 步领养你的<em> AI 帮手</em></h1>
  <p class="ai d2">不需要懂编程，像养宠物一样，按顺序走完这 5 步，你就能拥有一个能帮你写文档、搜信息、管邮件、做设计的 AI 伙伴。</p>

  <div class="tl ai d3">
    <div class="ts"><div class="ts-n n1">1</div><div class="ts-c">领养<small>挑一个合眼缘的</small></div></div>
    <div class="tl-div"></div>
    <div class="ts"><div class="ts-n n2">2</div><div class="ts-c">喂养<small>给它充口粮（API）</small></div></div>
    <div class="tl-div"></div>
    <div class="ts"><div class="ts-n n3">3</div><div class="ts-c">教技能<small>让它学会干活</small></div></div>
    <div class="tl-div"></div>
    <div class="ts"><div class="ts-n n4">4</div><div class="ts-c">配装备<small>给它工具操作世界</small></div></div>
    <div class="tl-div"></div>
    <div class="ts"><div class="ts-n n5">5</div><div class="ts-c">找个新伙伴<small>多只协作更强</small></div></div>
  </div>
  <p class="hsub ai d4"><span>前三步 = 它能干活了</span> · 后两步 = 它更厉害了</p>
</section>

<!-- ═══════════════ STEP 1: 领养 ═══════════════ -->
<section class="sec" id="step1">
  <div class="sec-hd">
    <div class="stag stg1">Step 1</div>
    <h2 class="stit">领养你的 AI 帮手</h2>
    <p class="sdesc">就像领养宠物一样，先挑一个合眼缘的。这些产品都是 AI 帮手的不同品种，选一个适合你的，下载安装就能用。</p>
  </div>

  <div class="snote ai">
    <div class="snote-ico" style="background:var(--g3);color:var(--g1)">💡</div>
    <div class="snote-txt"><strong>怎么选？</strong><br>
      📦 <strong>QClaw</strong> — 一键安装，下载即用。内置技能包，Mac/Windows通用。每天送4000万Token，新手省心首选。<br>
      💻 <strong>Workbuddy</strong> — 本地桌面端，数据不出本地。新人送4800积分+每日100积分，够用很久。<br>
      🍒 <strong>Cherry Studio</strong> — 可同时配置几十个模型切换着玩，可配置多MCP。<br>
      🌐 <strong>CodeArts</strong> — 华为云CodeArts，编程专用，支持glm5.1模型，公测完全免费。
    </div>
  </div>

  <!-- 主推卡片（前3个） -->
  <h3 style="font-size:15px;font-weight:600;margin-bottom:12px;color:var(--tx2)">⭐推荐首选</h3>
  <div class="cg" style="margin-bottom:32px">
    <!-- 1. QClaw - 主推 -->
    <div class="c ai" onclick="window.open('https://qclaw.qq.com','_blank')" style="cursor:pointer">
      <div class="ca" style="background:var(--b1)"></div>
      <div class="ci" style="background:var(--b3);color:var(--b1)">📦</div>
      <div class="cn">QClaw <span class="cbn bh">🕐限时免费</span></div>
      <div class="cd">一键安装，下载即用。内置技能包，Mac/Windows通用。每天送4000万Token，新手省心首选。<br><strong style="color:var(--g1)">💰 限时免费 | 🎁 每天4000万Token</strong></div>
      <div class="ct"><span class="ctg">省心首选</span><span class="ctg">一键安装</span><span class="ctg">Mac/Windows</span></div>
      <span class="cl">qclaw.qq.com →</span>
    </div>

    <!-- 2. Workbuddy - 桌面端 -->
    <div class="c ai d1" onclick="window.open('https://www.codebuddy.cn','_blank')" style="cursor:pointer">
      <div class="ca" style="background:var(--g1)"></div>
      <div class="ci" style="background:var(--g3);color:var(--g1)">W</div>
      <div class="cn">Workbuddy <span class="cbn bh">🆓完全免费</span></div>
      <div class="cd">本地桌面端，数据不出本地。新人送4800积分+每日100积分，够用很久。<br><strong style="color:var(--g1)">💰 完全免费 | 🎁 新人4800积分</strong></div>
      <div class="ct"><span class="ctg">桌面本地</span><span class="ctg">数据安全</span><span class="ctg">新人积分</span></div>
      <span class="cl">codebuddy.cn →</span>
    </div>

    <!-- 3. Cherry Studio - 跨平台 -->
    <div class="c ai d2" onclick="window.open('https://cherry-ai.com','_blank')" style="cursor:pointer">
      <div class="ca" style="background:var(--r1)"></div>
      <div class="ci" style="background:var(--r3);color:var(--r1)">🍒</div>
      <div class="cn">Cherry Studio <span class="cbn bh">🆓完全免费</span></div>
      <div class="cd">跨平台客户端，Windows/Mac/Linux都能用。可同时配置几十个模型切换着玩，开源免费。<br><strong style="color:var(--g1)">💰 完全免费 | 🎁 开源免费</strong></div>
      <div class="ct"><span class="ctg">跨平台</span><span class="ctg">多模型切换</span><span class="ctg">开源</span></div>
      <span class="cl">cherry-ai.com →</span>
    </div>
  </div>

  <!-- 更多选择（表格） -->
  <h3 style="font-size:15px;font-weight:600;margin-bottom:12px;color:var(--tx2)">📋更多选择</h3>
  <table class="data-table">
    <thead>
      <tr>
        <th class="ico"></th>
        <th class="name">名称</th>
        <th class="desc">介绍</th>
        <th class="price">价格</th>
        <th class="promo">活动</th>
        <th class="note">备注</th>
      </tr>
    </thead>
    <tbody>
      <tr onclick="window.open('https://docs.anthropic.com/en/docs/claude-code','_blank')">
        <td class="ico"><span style="background:var(--b3);color:var(--b1)">CC</span></td>
        <td class="name">Claude Code</td>
        <td class="desc">终端编程Agent，自主写代码，需自己配置</td>
        <td class="price">完全免费（无免费额度）</td>
        <td class="promo">无新用户活动</td>
        <td class="note">开源</td>
      </tr>
      <tr onclick="window.open('https://www.kimi.com/bot','_blank')">
        <td class="ico"><span style="background:var(--tx1)">🌙</span></td>
        <td class="name">Kimi Claw</td>
        <td class="desc">打开网页就能聊，无需安装。支持20万字长文本、深度推理、联网搜索</td>
        <td class="price">具体价格：49元/月</td>
        <td class="promo">Kimi会员可用</td>
        <td class="note">零门槛</td>
      </tr>
      <tr onclick="window.open('https://openclaw.ai','_blank')">
        <td class="ico"><span style="background:linear-gradient(90deg,var(--g1),var(--t1))">🦞</span></td>
        <td class="name">OpenClaw</td>
        <td class="desc">功能最全、自由度最高。支持技能扩展、工具连接、定时任务、多渠道接入</td>
        <td class="price">完全免费</td>
        <td class="promo">-</td>
        <td class="note">功能最全·开源</td>
      </tr>
      <tr onclick="window.open('https://www.volcengine.com/docs/82379/2229107?lang=zh','_blank')">
        <td class="ico"><span style="background:var(--p3);color:var(--p1)">A</span></td>
        <td class="name">ArkClaw</td>
        <td class="desc">字节出品，飞书集成，需购买Coding Plan Pro版才可以使用</td>
        <td class="price">200元/月</td>
        <td class="promo">需购买Coding Plan Pro版才可以使用</td>
        <td class="note">新人不建议·价格贵</td>
      </tr>
      <tr onclick="window.open('https://jvs.wuying.aliyun.com/','_blank')">
        <td class="ico"><span style="background:var(--o3);color:var(--o1)">JV</span></td>
        <td class="name">JVSClaw</td>
        <td class="desc">阿里云，多Agent协同，包含网页版、手机app、Mac电脑端，无Windows端</td>
        <td class="price">部分免费（7天免费）</td>
        <td class="promo">新人7天免费试用</td>
        <td class="note">无Windows端</td>
      </tr>
      <tr onclick="window.open('https://qoder.com/qoderwork','_blank')">
        <td class="ico"><span style="background:var(--t3);color:var(--t1)">Q</span></td>
        <td class="name">QoderWork</td>
        <td class="desc">阿里出品，文档生成</td>
        <td class="price">完全免费</td>
        <td class="promo">2周Pro试用+300 Credits</td>
        <td class="note">桌面端</td>
      </tr>
      <tr onclick="window.open('https://cloud.baidu.com/product/duclaw.html','_blank')">
        <td class="ico"><span style="background:var(--b3);color:var(--b1)">D</span></td>
        <td class="name">DuClaw</td>
        <td class="desc">百度DuClaw服务 + 千帆Coding Plan</td>
        <td class="price">具体价格：17.8元/月</td>
        <td class="promo">首月17.8元</td>
        <td class="note">云端</td>
      </tr>
      <tr onclick="window.open('https://codearts.huaweicloud.com/','_blank')">
        <td class="ico"><span style="background:var(--r3);color:var(--r1)">华</span></td>
        <td class="name">CodeArts</td>
        <td class="desc">华为云CodeArts，编程专用，支持glm5.1模型，公测完全免费。</td>
        <td class="price">完全免费</td>
        <td class="promo">公测阶段</td>
        <td class="note">编程专用</td>
      </tr>
      <tr onclick="window.open('https://maxclaw.ai','_blank')">
        <td class="ico"><span style="background:var(--k3);color:#F9A825">M</span></td>
        <td class="name">MaxClaw</td>
        <td class="desc">MiniMax出品，200K记忆</td>
        <td class="price">具体价格：MiniMax订阅</td>
        <td class="promo">🎁新用户有礼</td>
        <td class="note">云端</td>
      </tr>
    </tbody>
  </table>
</section>

<div class="sdiv"><div class="sdiv-inner"></div></div>

<!-- ═══════════════ STEP 2: 喂养 ═══════════════ -->
<section class="sec" id="step2">
  <div class="sec-hd">
    <div class="stag stg2">Step 2</div>
    <h2 class="stit">给它充口粮（API）</h2>
    <p class="sdesc">AI 帮手需要"口粮"才能干活。口粮就是大模型 API，你需要选择一个口粮供应站，注册充值，拿到提货码（API Key）填入你的助手即可。</p>
  </div>

  <div class="snote ai">
    <div class="snote-ico" style="background:var(--b3);color:var(--b1)">💡</div>
    <div class="snote-txt"><strong>怎么选口粮？</strong><br>
      想便宜/免费 → <strong>DeepSeek</strong>（白菜价）<br>
      想综合最强 → <strong>OpenAI / Claude</strong>（行业标杆）<br>
      不想折腾网络 → <strong>中转站</strong>（国内直连，支付宝充值）
    </div>
  </div>

  <!-- 主推卡片（前3个） -->
  <h3 style="font-size:15px;font-weight:600;margin-bottom:12px;color:var(--tx2)">⭐推荐首选</h3>
  <div class="cg" style="margin-bottom:32px">
    <!-- 1. DeepSeek -->
    <div class="c ai" onclick="window.open('https://platform.deepseek.com','_blank')" style="cursor:pointer">
      <div class="ca" style="background:var(--g1)"></div>
      <div class="ci" style="background:var(--g3);color:var(--g1)">D</div>
      <div class="cn">DeepSeek</div>
      <div class="cd">推理之王，开源白菜价，性价比最高。适合预算有限但想要强大能力的用户。<br><strong style="color:var(--g1)">💰 白菜价</strong></div>
      <div class="ct"><span class="ctg">推理强</span><span class="ctg">性价比</span><span class="ctg">开源</span></div>
      <span class="cl">platform.deepseek.com →</span>
    </div>

    <!-- 2. 硅基流动 -->
    <div class="c ai d1" onclick="window.open('https://siliconflow.cn','_blank')" style="cursor:pointer">
      <div class="ca" style="background:var(--p1)"></div>
      <div class="ci" style="background:var(--p3);color:var(--p1)">硅</div>
      <div class="cn">硅基流动 <span class="cbn bn">🎁2000万Token</span></div>
      <div class="cd">多模型聚合，送2000万Tokens。国内直连，模型丰富，注册即用。<br><strong style="color:var(--g1)">💰 免费+付费</strong></div>
      <div class="ct"><span class="ctg">聚合</span><span class="ctg">2000万Token</span><span class="ctg">国内直连</span></div>
      <span class="cl">siliconflow.cn →</span>
    </div>

    <!-- 3. 美团龙猫 -->
    <div class="c ai d2" onclick="window.open('https://longcat.chat','_blank')" style="cursor:pointer">
      <div class="ca" style="background:#FF6D00"></div>
      <div class="ci" style="background:#FFF3E0;color:#FF6D00">龙</div>
      <div class="cn">美团龙猫 <span class="cbn bh">🔥强烈力推</span></div>
      <div class="cd">美团出品，大模型 API 平台。国内直连，支付宝充值。免费额度 50,000,000 token，简单省事。<br><strong style="color:var(--g1)">💰 免费</strong></div>
      <div class="ct"><span class="ctg">美团出品</span><span class="ctg">国内直连</span><span class="ctg">5千万Token</span></div>
      <span class="cl">longcat.chat →</span>
    </div>
  </div>

  <!-- 更多选择（表格） -->
  <h3 style="font-size:15px;font-weight:600;margin-bottom:12px;color:var(--tx2)">📋更多官方口粮站</h3>
  <table class="data-table" style="margin-bottom:36px">
    <thead>
      <tr>
        <th class="ico"></th>
        <th class="name">名称</th>
        <th class="desc">介绍</th>
        <th class="price">价格</th>
        <th class="promo">活动</th>
        <th class="note">备注</th>
      </tr>
    </thead>
    <tbody>
      <tr onclick="window.open('https://platform.openai.com','_blank')">
        <td class="ico"><span style="background:var(--g3);color:var(--g1)">O</span></td>
        <td class="name">OpenAI</td>
        <td class="desc">GPT-4o/5，综合最强，行业标杆</td>
        <td class="price">付费</td>
        <td class="promo">-</td>
        <td class="note">需代理</td>
      </tr>
      <tr onclick="window.open('https://console.anthropic.com','_blank')">
        <td class="ico"><span style="background:var(--p3);color:var(--p1)">A</span></td>
        <td class="name">Anthropic</td>
        <td class="desc">Claude 4，安全可靠，长文本强</td>
        <td class="price">付费</td>
        <td class="promo">-</td>
        <td class="note">需代理</td>
      </tr>
      <tr onclick="window.open('https://bailian.console.aliyun.com','_blank')">
        <td class="ico"><span style="background:var(--o3);color:var(--o1)">阿</span></td>
        <td class="name">阿里云百炼</td>
        <td class="desc">Qwen3，通义千问，多语言强</td>
        <td class="price">免费+付费</td>
        <td class="promo">🎁有礼</td>
        <td class="note">国内直连</td>
      </tr>
      <tr onclick="window.open('https://www.bigmodel.cn/invite?icode=szzzcE07Xs9HDlNsy%2BXXcn3uFJ1nZ0jLLgipQkYjpcA%3D','_blank')">
        <td class="ico"><span style="background:var(--p3);color:var(--p1)">智</span></td>
        <td class="name">智谱AI</td>
        <td class="desc">GLM-5，清华系，编程能力强</td>
        <td class="price">免费+付费</td>
        <td class="promo">🎁有礼</td>
        <td class="note">国内直连</td>
      </tr>
      <tr onclick="window.open('https://platform.moonshot.cn','_blank')">
        <td class="ico"><span style="background:var(--b3);color:var(--b1)">月</span></td>
        <td class="name">月之暗面</td>
        <td class="desc">Kimi，20万字超长上下文</td>
        <td class="price">付费</td>
        <td class="promo">-</td>
        <td class="note">国内直连</td>
      </tr>
      <tr onclick="window.open('https://cloud.baidu.com/product/wenxinworkshop','_blank')">
        <td class="ico"><span style="background:var(--r3);color:var(--r1)">百</span></td>
        <td class="name">百度文心</td>
        <td class="desc">ERNIE 5，中文能力顶级</td>
        <td class="price">付费</td>
        <td class="promo">-</td>
        <td class="note">国内直连</td>
      </tr>
      <tr onclick="window.open('https://hunyuan.tencent.com','_blank')">
        <td class="ico"><span style="background:var(--t3);color:var(--t1)">腾</span></td>
        <td class="name">腾讯混元</td>
        <td class="desc">多模态，中文AI标杆</td>
        <td class="price">付费</td>
        <td class="promo">-</td>
        <td class="note">国内直连</td>
      </tr>
      <tr onclick="window.open('https://platform.lingyiwanwu.com','_blank')">
        <td class="ico"><span style="background:var(--k3);color:#F9A825">零</span></td>
        <td class="name">零一万物</td>
        <td class="desc">Yi-Lightning，100万token 0.99元</td>
        <td class="price">白菜价</td>
        <td class="promo">-</td>
        <td class="note">国内直连</td>
      </tr>
      <tr onclick="window.open('https://xinghuo.xfyun.cn/sparkapi','_blank')">
        <td class="ico"><span style="background:var(--p3);color:var(--p1)">讯</span></td>
        <td class="name">科大讯飞</td>
        <td class="desc">星火 X2，语音识别合成领先</td>
        <td class="price">免费+付费</td>
        <td class="promo">🎁有礼</td>
        <td class="note">国内直连</td>
      </tr>
      <tr onclick="window.open('https://www.minimaxi.com','_blank')">
        <td class="ico"><span style="background:var(--b3);color:var(--b1)">M</span></td>
        <td class="name">MiniMax</td>
        <td class="desc">海螺AI，多模态，港股上市</td>
        <td class="price">付费</td>
        <td class="promo">-</td>
        <td class="note">国内直连</td>
      </tr>
      <tr onclick="window.open('https://ai.google.dev','_blank')">
        <td class="ico"><span style="background:var(--g3);color:var(--g1)">G</span></td>
        <td class="name">Google</td>
        <td class="desc">Gemini 3，搜索生态整合</td>
        <td class="price">付费</td>
        <td class="promo">-</td>
        <td class="note">需代理</td>
      </tr>
    </tbody>
  </table>

  <!-- 中转站 -->
  <h3 style="font-size:15px;font-weight:600;margin-bottom:12px;color:var(--tx2)">⚡中转站（国内直连·支付宝充值）</h3>
  <div class="snote ai" style="margin-bottom:16px">
    <div class="snote-ico" style="background:var(--o3);color:var(--o1)">💡</div>
    <div class="snote-txt" style="font-size:13px"><strong>中转站是什么？</strong> 不想找官方注册/不方便科学上网 → 中转站帮你搞定。国内直连，支付宝充值。<strong>1元≈1美金</strong>。</div>
  </div>

  <!-- 中转站主推卡片（前4个） -->
  <div class="cg" style="margin-bottom:32px">
    <div class="c ai" onclick="window.open('https://openrouter.ai','_blank')" style="cursor:pointer">
      <div class="ca" style="background:var(--g1)"></div>
      <div class="ci" style="background:var(--g3);color:var(--g1)">OR</div>
      <div class="cn">OpenRouter <span class="cbn bh">全球最大</span></div>
      <div class="cd">400+模型聚合，30+免费模型。全球最大API聚合平台。</div>
      <div class="ct"><span class="ctg">聚合</span><span class="ctg">免费</span><span class="ctg">全球</span></div>
      <span class="cl">openrouter.ai →</span>
    </div>
    <div class="c ai d1" onclick="window.open('https://4sapi.com','_blank')" style="cursor:pointer">
      <div class="ca" style="background:var(--p1)"></div>
      <div class="ci" style="background:var(--p3);color:var(--p1)">4S</div>
      <div class="cn">星链 4SAPI <span class="cbn bh">排名第一</span></div>
      <div class="cd">CN2专线，99.9% SLA，国内速度最快。</div>
      <div class="ct"><span class="ctg">专线</span><span class="ctg">稳定</span><span class="ctg">快速</span></div>
      <span class="cl">4sapi.com →</span>
    </div>
    <div class="c ai d2" onclick="window.open('https://api.weelinking.com','_blank')" style="cursor:pointer">
      <div class="ca" style="background:var(--b1)"></div>
      <div class="ci" style="background:var(--b3);color:var(--b1)">WL</div>
      <div class="cn">Weelinking <span class="cbn bn">性价比王</span></div>
      <div class="cd">成本控制优秀，99.99%稳定，价格透明。</div>
      <div class="ct"><span class="ctg">性价比</span><span class="ctg">稳定</span><span class="ctg">透明</span></div>
      <span class="cl">weelinking.com →</span>
    </div>
    <div class="c ai d3" onclick="window.open('https://www.arccodex.com/signup?ref=d3ozlllzba','_blank')" style="cursor:pointer">
      <div class="ca" style="background:var(--o1)"></div>
      <div class="ci" style="background:var(--o3);color:var(--o1)">A</div>
      <div class="cn">Arc Codex <span class="cbn bh">🔥强烈力推</span></div>
      <div class="cd">可用GPT-5.4，稳定可靠，起步套餐首月15.9元，适合程序开发。<br><strong style="color:var(--o1)">💰 付费白菜起步</strong></div>
      <div class="ct"><span class="ctg">GPT-5.4</span><span class="ctg">稳定</span><span class="ctg">开发首选</span></div>
      <span class="cl">arccodex.com →</span>
    </div>
  </div>

  <!-- 中转站表格 -->
  <h3 style="font-size:15px;font-weight:600;margin-bottom:12px;color:var(--tx2)">📋更多中转站</h3>
  <table class="data-table">
    <thead>
      <tr>
        <th class="ico"></th>
        <th class="name">名称</th>
        <th class="desc">介绍</th>
        <th class="price">价格</th>
        <th class="promo">活动</th>
        <th class="note">备注</th>
      </tr>
    </thead>
    <tbody>
      <tr onclick="window.open('https://hohy6.com','_blank')">
        <td class="ico"><span style="background:var(--t3);color:var(--t1)">海</span></td>
        <td class="name">海鸥云</td>
        <td class="desc">新用户送200万Token</td>
        <td class="price">付费</td>
        <td class="promo">🎁送200万</td>
        <td class="note">国内直连</td>
      </tr>
      <tr onclick="window.open('https://api.rcouyi.com','_blank')">
        <td class="ico"><span style="background:var(--o3);color:var(--o1)">No</span></td>
        <td class="name">No.1-API</td>
        <td class="desc">380+模型，数万用户</td>
        <td class="price">付费</td>
        <td class="promo">-</td>
        <td class="note">国内直连</td>
      </tr>
      <tr onclick="window.open('https://open.cherryin.ai','_blank')">
        <td class="ico"><span style="background:var(--r3);color:var(--r1)">🍒</span></td>
        <td class="name">Cherry AI</td>
        <td class="desc">新用户送Tokens</td>
        <td class="price">付费</td>
        <td class="promo">🎁邀请有礼</td>
        <td class="note">国内直连</td>
      </tr>
      <tr onclick="window.open('https://github.com/newaiproxy/gpt-proxy','_blank')">
        <td class="ico"><span style="background:var(--k3);color:#F9A825">神</span></td>
        <td class="name">神马中转</td>
        <td class="desc">OpenAI/Claude国内直连</td>
        <td class="price">付费</td>
        <td class="promo">-</td>
        <td class="note">开源</td>
      </tr>
      <tr onclick="window.open('https://gaorui.cc/register?aff=XJm9','_blank')">
        <td class="ico"><span style="background:var(--r3);color:var(--r1)">高</span></td>
        <td class="name">高瑞API</td>
        <td class="desc">多模型中转，速度快价格低</td>
        <td class="price">付费</td>
        <td class="promo">-</td>
        <td class="note">国内直连</td>
      </tr>
    </tbody>
  </table>
</section>

<div class="sdiv"><div class="sdiv-inner"></div></div>

<!-- ═══════════════ STEP 3: 教技能 ═══════════════ -->
<section class="sec" id="step3">
  <div class="sec-hd">
    <div class="stag stg3">Step 3</div>
    <h2 class="stit">教它学技能</h2>
    <p class="sdesc">技能 = AI 的"专业技能"。装了就能用，让你的 AI 帮手从"只会聊天"变成"全能打工仔"。</p>
  </div>

  <div class="snote ai">
    <div class="snote-ico" style="background:var(--p3);color:var(--p1)">💡</div>
    <div class="snote-txt"><strong>怎么教？</strong><br>
      在 OpenClaw / QClaw 中，输入 <code style="background:var(--bg);padding:2px 8px;border-radius:4px;font-size:13px">skillhub install &lt;名称&gt;</code> 即可一键安装。<br>
      比如想处理 Word 文档：<code style="background:var(--bg);padding:2px 8px;border-radius:4px;font-size:13px">skillhub install docx</code>
    </div>
  </div>

  <!-- 主推卡片（前3个） -->
  <h3 style="font-size:15px;font-weight:600;margin-bottom:12px;color:var(--tx2)">⭐必备技能</h3>
  <div class="cg" style="margin-bottom:32px">
    <!-- 1. Docx -->
    <div class="c ai" onclick="window.open('https://skillhub.dev/skill/docx','_blank')" style="cursor:pointer">
      <div class="ca" style="background:linear-gradient(90deg,#3B82F6,#06B6D4)"></div>
      <div class="ci" style="background:var(--b3);color:var(--b1)">📄</div>
      <div class="cn">Docx <span class="cbn bh">必备</span></div>
      <div class="cd">Word 文档全能力：创建、编辑、读取。支持目录、页眉页脚、表格、图片。<br><strong style="color:var(--b1)">📦 skillhub install docx</strong></div>
      <div class="ct"><span class="ctg">Word</span><span class="ctg">文档</span><span class="ctg">格式化</span></div>
      <span class="cl">skillhub.dev →</span>
    </div>

    <!-- 2. PDF -->
    <div class="c ai d1" onclick="window.open('https://skillhub.dev/skill/pdf','_blank')" style="cursor:pointer">
      <div class="ca" style="background:linear-gradient(90deg,var(--r1),var(--o1))"></div>
      <div class="ci" style="background:var(--r3);color:var(--r1)">📕</div>
      <div class="cn">PDF</div>
      <div class="cd">PDF 全能工具：读取提取、合并拆分、水印、加密解密、OCR 识别。<br><strong style="color:var(--b1)">📦 skillhub install pdf</strong></div>
      <div class="ct"><span class="ctg">PDF</span><span class="ctg">OCR</span><span class="ctg">合并拆分</span></div>
      <span class="cl">skillhub.dev →</span>
    </div>

    <!-- 3. Online Search -->
    <div class="c ai d2" onclick="window.open('https://skillhub.dev/skill/online-search','_blank')" style="cursor:pointer">
      <div class="ca" style="background:var(--b1)"></div>
      <div class="ci" style="background:var(--b3);color:var(--b1)">🔍</div>
      <div class="cn">Online Search <span class="cbn bh">推荐</span></div>
      <div class="cd">联网搜索：实时检索互联网信息，覆盖国内主流网站。<br><strong style="color:var(--b1)">📦 skillhub install online-search</strong></div>
      <div class="ct"><span class="ctg">搜索</span><span class="ctg">实时</span><span class="ctg">新闻</span></div>
      <span class="cl">skillhub.dev →</span>
    </div>
  </div>

  <!-- 更多技能（表格） -->
  <h3 style="font-size:15px;font-weight:600;margin-bottom:12px;color:var(--tx2)">📋更多技能</h3>
  <table class="data-table">
    <thead>
      <tr>
        <th class="ico"></th>
        <th class="name">名称</th>
        <th class="desc">介绍</th>
        <th class="cmd" style="min-width:180px">安装命令</th>
      </tr>
    </thead>
    <tbody>
      <tr onclick="window.open('https://skillhub.dev/skill/pptx','_blank')">
        <td class="ico"><span style="background:var(--o3);color:var(--o1)">📊</span></td>
        <td class="name">PPTX</td>
        <td class="desc">PowerPoint 演示文稿</td>
        <td class="cmd" style="font-family:monospace;font-size:12px;color:var(--b1)">skillhub install pptx</td>
      </tr>
      <tr onclick="window.open('https://skillhub.dev/skill/xlsx','_blank')">
        <td class="ico"><span style="background:var(--g3);color:var(--g1)">📋</span></td>
        <td class="name">XLSX</td>
        <td class="desc">电子表格 Excel/CSV</td>
        <td class="cmd" style="font-family:monospace;font-size:12px;color:var(--b1)">skillhub install xlsx</td>
      </tr>
      <tr onclick="window.open('https://skillhub.dev/skill/frontend-design','_blank')">
        <td class="ico"><span style="background:var(--p3);color:var(--p1)">🎨</span></td>
        <td class="name">Frontend Design</td>
        <td class="desc">生成前端代码网页</td>
        <td class="cmd" style="font-family:monospace;font-size:12px;color:var(--b1)">skillhub install frontend-design</td>
      </tr>
      <tr onclick="window.open('https://skillhub.dev/skill/canvas-design','_blank')">
        <td class="ico"><span style="background:var(--r3);color:var(--r1)">🖼️</span></td>
        <td class="name">Canvas Design</td>
        <td class="desc">海报设计 PNG/PDF</td>
        <td class="cmd" style="font-family:monospace;font-size:12px;color:var(--b1)">skillhub install canvas-design</td>
      </tr>
      <tr onclick="window.open('https://skillhub.dev','_blank')">
        <td class="ico"><span style="background:var(--b3);color:var(--b1)">✉️</span></td>
        <td class="name">Email</td>
        <td class="desc">邮件收发 163/QQ/IMAP</td>
        <td class="cmd" style="font-family:monospace;font-size:12px;color:var(--b1)">skillhub install email</td>
      </tr>
      <tr onclick="window.open('https://skillhub.dev','_blank')">
        <td class="ico"><span style="background:var(--k3);color:#F9A825">📰</span></td>
        <td class="name">News Summary</td>
        <td class="desc">每日新闻简报</td>
        <td class="cmd" style="font-family:monospace;font-size:12px;color:var(--b1)">skillhub install news-summary</td>
      </tr>
      <tr onclick="window.open('https://skillhub.dev','_blank')">
        <td class="ico"><span style="background:var(--t3);color:var(--t1)">🌤️</span></td>
        <td class="name">Weather</td>
        <td class="desc">天气查询穿衣建议</td>
        <td class="cmd" style="font-family:monospace;font-size:12px;color:var(--b1)">skillhub install weather</td>
      </tr>
      <tr onclick="window.open('https://skillhub.dev','_blank')">
        <td class="ico"><span style="background:var(--g3);color:var(--g1)">📝</span></td>
        <td class="name">腾讯文档</td>
        <td class="desc">在线文档操作</td>
        <td class="cmd" style="font-family:monospace;font-size:12px;color:var(--b1)">skillhub install tencent-docs</td>
      </tr>
      <tr onclick="window.open('https://skillhub.dev','_blank')">
        <td class="ico"><span style="background:var(--p3);color:var(--p1)">📹</span></td>
        <td class="name">腾讯会议</td>
        <td class="desc">会议管理录制转写</td>
        <td class="cmd" style="font-family:monospace;font-size:12px;color:var(--b1)">skillhub install tencent-meeting</td>
      </tr>
      <tr onclick="window.open('https://skillhub.dev','_blank')">
        <td class="ico"><span style="background:var(--o3);color:var(--o1)">📊</span></td>
        <td class="name">腾讯问卷</td>
        <td class="desc">问卷创建管理</td>
        <td class="cmd" style="font-family:monospace;font-size:12px;color:var(--b1)">skillhub install tencent-survey</td>
      </tr>
    </tbody>
  </table>
</section>

<div class="sdiv"><div class="sdiv-inner"></div></div>

<!-- ═══════════════ STEP 4: 配装备 (MCP) ═══════════════ -->
<section class="sec" id="step4" style="background:var(--bg3);max-width:100%;padding-left:calc((100% - 1104px)/2);padding-right:calc((100% - 1104px)/2);">
  <div class="sec-hd">
    <div class="stag stg4">Step 4 · 进阶</div>
    <h2 class="stit">给它配装备（MCP）</h2>
    <p class="sdesc">MCP 就像给 AI 配的工具箱——让它能浏览网页、读文件、执行命令。走完前三步后再来。</p>
  </div>

  <div class="snote ai">
    <div class="snote-ico" style="background:var(--o3);color:var(--o1)">💡</div>
    <div class="snote-txt"><strong>为什么需要装备？</strong><br>
      没有装备的 AI 只能"动嘴"——回答问题、生成文本。<br>
      配了装备的 AI 能"动手"——帮你浏览网页、操作文件系统、运行程序。<br>
      <strong>这一步是 AI 从"聊天伙伴"变成"数字员工"的关键。</strong>
    </div>
  </div>

  <!-- 主推卡片（前3个） -->
  <h3 style="font-size:15px;font-weight:600;margin-bottom:12px;color:var(--tx2)">⭐核心装备</h3>
  <div class="cg" style="margin-bottom:32px">
    <div class="c ai">
      <div class="ca" style="background:var(--b1)"></div>
      <div class="ci" style="background:var(--b3);color:var(--b1)">🌐</div>
      <div class="cn">Browser Control <span class="cbn bh">核心</span></div>
      <div class="cd">浏览器自动化：截图、点击、填写表单、导航页面。Playwright 驱动。</div>
      <div class="ct"><span class="ctg">Playwright</span><span class="ctg">自动化</span><span class="ctg">截图</span></div>
    </div>
    <div class="c ai d1">
      <div class="ca" style="background:var(--g1)"></div>
      <div class="ci" style="background:var(--g3);color:var(--g1)">📂</div>
      <div class="cn">File System</div>
      <div class="cd">文件系统操作：读取、创建、编辑文件，目录管理，文件搜索。</div>
      <div class="ct"><span class="ctg">读写</span><span class="ctg">目录</span><span class="ctg">搜索</span></div>
    </div>
    <div class="c ai d2">
      <div class="ca" style="background:var(--p1)"></div>
      <div class="ci" style="background:var(--p3);color:var(--p1)">⌨️</div>
      <div class="cn">Shell / Terminal</div>
      <div class="cd">命令行执行：运行脚本、安装依赖、编译构建，完整 Shell 交互。</div>
      <div class="ct"><span class="ctg">Shell</span><span class="ctg">命令行</span><span class="ctg">自动化</span></div>
    </div>
  </div>

  <!-- 更多装备（表格） -->
  <h3 style="font-size:15px;font-weight:600;margin-bottom:12px;color:var(--tx2)">📋更多装备</h3>
  <table class="data-table">
    <thead>
      <tr>
        <th class="ico"></th>
        <th class="name">名称</th>
        <th class="desc">介绍</th>
        <th class="note">备注</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td class="ico"><span style="background:var(--t3);color:var(--t1)">🔍</span></td>
        <td class="name">Web Search</td>
        <td class="desc">通过 Brave/Google API 获取实时互联网信息</td>
        <td class="note">需API</td>
      </tr>
      <tr>
        <td class="ico"><span style="background:var(--o3);color:var(--o1)">📱</span></td>
        <td class="name">Device Pairing</td>
        <td class="desc">连接手机，相机拍照、GPS定位、通知推送</td>
        <td class="note">手机配对</td>
      </tr>
      <tr>
        <td class="ico"><span style="background:var(--r3);color:var(--r1)">⏰</span></td>
        <td class="name">Cron / Scheduler</td>
        <td class="desc">定时提醒、周期检查、一次性任务调度</td>
        <td class="note">内置</td>
      </tr>
    </tbody>
  </table>
</section>

<div class="sdiv"><div class="sdiv-inner"></div></div>

<!-- ═══════════════ STEP 5: 找个新伙伴 ═══════════════ -->
<section class="sec" id="step5">
  <div class="sec-hd">
    <div class="stag stg5">Step 5 · 进阶</div>
    <h2 class="stit">找个新伙伴</h2>
    <p class="sdesc">一只 AI 干不过来？找个新伙伴，让它们协作！到这里你已经是一个合格的 AI 主人了。</p>
  </div>

  <div class="snote ai">
    <div class="snote-ico" style="background:var(--k3);color:#F9A825">💡</div>
    <div class="snote-txt"><strong>多只 AI 能做什么？</strong><br>
      一只写文档 + 一只搜资料 + 一只做表格 → <strong>并行处理，效率翻倍</strong><br>
      一只管前端 + 一只管后端 → <strong>分工协作，各司其职</strong><br>
      一只搞研究 + 一只写论文 → <strong>AI 科学家</strong>
    </div>
  </div>

  <!-- 主推卡片（前3个） -->
  <h3 style="font-size:15px;font-weight:600;margin-bottom:12px;color:var(--tx2)">⭐多Agent平台</h3>
  <div class="cg" style="margin-bottom:32px">
    <div class="c ai" onclick="window.open('https://docs.anthropic.com/en/docs/claude-code','_blank')" style="cursor:pointer">
      <div class="ca" style="background:linear-gradient(90deg,#D4A574,var(--o1))"></div>
      <div class="ci" style="background:var(--o3);color:var(--o1)">🧑‍💻</div>
      <div class="cn">Claude Code</div>
      <div class="cd">Anthropic 终端编程 Agent，命令行中自主编写、修改、调试代码。</div>
      <div class="ct"><span class="ctg">编程</span><span class="ctg">终端</span><span class="ctg">Anthropic</span></div>
      <span class="cl">docs.anthropic.com →</span>
    </div>
    <div class="c ai d1" onclick="window.open('https://openai.com/index/codex/','_blank')" style="cursor:pointer">
      <div class="ca" style="background:linear-gradient(90deg,#10A37F,var(--b1))"></div>
      <div class="ci" style="background:var(--b3);color:var(--b1)">🤖</div>
      <div class="cn">OpenAI Codex</div>
      <div class="cd">OpenAI 云端沙箱编程 Agent，自主完成代码编写、测试、调试。</div>
      <div class="ct"><span class="ctg">编程</span><span class="ctg">云端</span><span class="ctg">OpenAI</span></div>
      <span class="cl">openai.com →</span>
    </div>
    <div class="c ai d2" onclick="window.open('https://dify.ai','_blank')" style="cursor:pointer">
      <div class="ca" style="background:linear-gradient(90deg,var(--t1),var(--g1))"></div>
      <div class="ci" style="background:var(--t3);color:var(--t1)">🔧</div>
      <div class="cn">Dify <span class="cbn bo">开源</span></div>
      <div class="cd">开源 LLM 应用平台：可视化编排 Agent 工作流，支持 RAG。</div>
      <div class="ct"><span class="ctg">工作流</span><span class="ctg">RAG</span><span class="ctg">可视化</span></div>
      <span class="cl">dify.ai →</span>
    </div>
  </div>

  <!-- 更多工具（表格） -->
  <h3 style="font-size:15px;font-weight:600;margin-bottom:12px;color:var(--tx2)">📋更多工具</h3>
  <table class="data-table">
    <thead>
      <tr>
        <th class="ico"></th>
        <th class="name">名称</th>
        <th class="desc">介绍</th>
        <th class="note">备注</th>
      </tr>
    </thead>
    <tbody>
      <tr onclick="window.open('https://n8n.io','_blank')">
        <td class="ico"><span style="background:var(--o3);color:var(--o1)">⚡</span></td>
        <td class="name">n8n</td>
        <td class="desc">工作流自动化平台，400+集成</td>
        <td class="note">开源</td>
      </tr>
      <tr onclick="window.open('https://langchain.com','_blank')">
        <td class="ico"><span style="background:var(--k3);color:#F9A825">⛓️</span></td>
        <td class="name">LangChain</td>
        <td class="desc">最流行的LLM框架，Chain/Agent/Memory/Tool</td>
        <td class="note">框架</td>
      </tr>
      <tr onclick="window.open('https://github.com/SakanaAI/AI-Scientist','_blank')">
        <td class="ico"><span style="background:var(--p3);color:var(--p1)">🔬</span></td>
        <td class="name">AI Scientist</td>
        <td class="desc">自动化科研系统，生成论文</td>
        <td class="note">开源</td>
      </tr>
      <tr>
        <td class="ico"><span style="background:var(--g3);color:var(--g1)">👥</span></td>
        <td class="name">Sub-Agent</td>
        <td class="desc">多Agent协作，生成隔离子Agent并行处理</td>
        <td class="note">内置</td>
      </tr>
    </tbody>
  </table>
</section>

<!-- ═══════════════ CTA ═══════════════ -->
<div class="cta-wrap">
  <div class="cta-card">
    <div class="ccf ccf1"></div><div class="ccf ccf2"></div><div class="ccf ccf3"></div>
    <h2>🚀 准备好出发了吗？</h2>
    <p>回到顶部，从 Step 1 开始，一步步掌握 AI 工具。</p>
    <div style="display:flex;gap:12px;justify-content:center;flex-wrap:wrap">
      <button class="cta-btn" onclick="window.scrollTo({top:0,behavior:'smooth'})">↑ 从第 1 步开始</button>
      <a href="dev.html" class="cta-btn" style="background:var(--tx1);text-decoration:none">⚙️ 开发者深度指南 →</a>
    </div>
  </div>
</div>

<!-- FOOTER -->
<footer>
  <p>AI 上手指南 · 2026 · 面向普通人的 AI 工具索引 · 信息仅供参考，以官方为准</p>
  <p style="margin-top:6px">最后更新：2026-04-09</p>
</footer>

</div><!-- END page-content -->

<script>
  // Nav scroll
  const nav=document.getElementById('nav');
  window.addEventListener('scroll',()=>nav.classList.toggle('scrolled',scrollY>10));

  // Intersection Observer for scroll animations
  const obs=new IntersectionObserver(es=>{
    es.forEach(e=>{if(e.isIntersecting){e.target.style.animationPlayState='running';obs.unobserve(e.target)}});
  },{threshold:.08});
  document.querySelectorAll('.ai').forEach(el=>{el.style.animationPlayState='paused';obs.observe(el)});

  // Smooth scroll for nav steps
  document.querySelectorAll('.nsteps a').forEach(a=>{
    a.addEventListener('click',e=>{e.preventDefault();const t=document.querySelector(a.getAttribute('href'));if(t)t.scrollIntoView({behavior:'smooth',block:'start'})});
  });
</script>

<!-- USER ID BADGE -->
<div class="user-badge" id="userBadge">
  🔑 ID: <span id="userIdDisplay">...</span>
</div>

<script>
// ═══════════════════════════════════════════════════════════
// TRACKING SYSTEM
// ═══════════════════════════════════════════════════════════

// Backend API endpoint - 修改为你的服务器地址
const API_ENDPOINT = 'http://101.132.129.12:3000/api/track';

// User ID management
let USER_ID = null;
let SESSION_START = Date.now();
let CURRENT_STEP = null;
let STEP_START = null;
let P0_ANSWERS = {};

// Generate UUID
function generateUUID() {
  return 'u-' + Date.now().toString(36) + '-' + Math.random().toString(36).substr(2, 9);
}

// Initialize user
function initUser() {
  const stored = localStorage.getItem('ai_tools_user_id');
  if (stored) {
    USER_ID = stored;
    console.log('Returning user:', USER_ID);
  } else {
    USER_ID = generateUUID();
    localStorage.setItem('ai_tools_user_id', USER_ID);
    console.log('New user:', USER_ID);
    trackEvent('init', 'visit', { referrer: document.referrer });
  }
  
  document.getElementById('userIdDisplay').textContent = USER_ID.substring(0, 12) + '...';
}

// Track event
function trackEvent(step, event, data = {}) {
  const payload = {
    uuid: USER_ID,
    ts: new Date().toISOString(),
    step: step,
    event: event,
    data: data,
    duration: STEP_START ? Math.floor((Date.now() - STEP_START) / 1000) : null
  };
  
  // Send to backend
  fetch(API_ENDPOINT, {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(payload)
  }).catch(err => console.log('Track error:', err));
  
  console.log('Tracked:', step, event, data);
}

// ═══════════════════════════════════════════════════════════
// P0 QUESTIONNAIRE
// ═══════════════════════════════════════════════════════════

let currentQuestion = 1;
const totalQuestions = 4;

// 关闭问卷浮窗，显示主页面
function closeP0AndShowPage() {
  localStorage.setItem('ai_tools_p0_done', 'true');
  document.getElementById('p0Overlay').classList.add('hidden');
  document.getElementById('pageContent').classList.remove('blurred');
  trackEvent('P0', 'complete', P0_ANSWERS);
  window.scrollTo({ top: 0, behavior: 'smooth' });
}

// 选择选项后自动跳转下一题
function selectOption(element) {
  const question = element.closest('.p0-question');
  const questionNum = parseInt(question.dataset.question);
  
  // 标记选中状态
  question.querySelectorAll('.p0-opt').forEach(o => o.classList.remove('selected'));
  element.classList.add('selected');
  
  // 保存答案
  P0_ANSWERS['q' + questionNum] = element.dataset.value;
  
  // 追踪
  trackEvent('P0', 'answer', { question: questionNum, answer: element.dataset.value });
  
  // 更新进度点
  document.querySelector(`.p0-dot[data-q="${questionNum}"]`).classList.remove('active');
  document.querySelector(`.p0-dot[data-q="${questionNum}"]`).classList.add('done');
  
  // 延迟跳转（给用户视觉反馈）
  setTimeout(() => {
    question.classList.remove('active');
    
    if (questionNum >= totalQuestions) {
      // 最后一题，关闭浮窗
      closeP0AndShowPage();
    } else {
      // 显示下一题
      currentQuestion = questionNum + 1;
      const nextQ = document.querySelector(`.p0-question[data-question="${currentQuestion}"]`);
      if (nextQ) {
        nextQ.classList.add('active');
        document.querySelector(`.p0-dot[data-q="${currentQuestion}"]`).classList.add('active');
      }
    }
  }, 200);
}

function skipP0() {
  localStorage.setItem('ai_tools_p0_done', 'true');
  trackEvent('P0', 'skip');
  document.getElementById('p0Overlay').classList.add('hidden');
  document.getElementById('pageContent').classList.remove('blurred');
}

// ═══════════════════════════════════════════════════════════
// STEP TRACKING (Intersection Observer)
// ═══════════════════════════════════════════════════════════

const stepObserver = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      const stepId = entry.target.id;
      if (stepId && stepId.startsWith('step')) {
        if (CURRENT_STEP !== stepId) {
          if (CURRENT_STEP && STEP_START) {
            trackEvent(CURRENT_STEP, 'exit');
          }
          CURRENT_STEP = stepId;
          STEP_START = Date.now();
          trackEvent(stepId, 'view');
        }
      }
    }
  });
}, { threshold: 0.3 });

document.querySelectorAll('section[id^="step"]').forEach(section => {
  stepObserver.observe(section);
});

// ═══════════════════════════════════════════════════════════
// INIT
// ═══════════════════════════════════════════════════════════

document.addEventListener('DOMContentLoaded', () => {
  initUser();
  trackEvent('init', 'page_load');
  
  // 检查是否已经完成过问卷
  const p0Done = localStorage.getItem('ai_tools_p0_done');
  if (p0Done) {
    // 已完成问卷，直接关闭浮窗
    document.getElementById('p0Overlay').classList.add('hidden');
  } else {
    // 未完成问卷，页面虚化，显示问卷
    document.getElementById('pageContent').classList.add('blurred');
  }
});

// Track page unload
window.addEventListener('beforeunload', () => {
  trackEvent('session', 'end', { duration: Math.floor((Date.now() - SESSION_START) / 1000) });
});
</script>
</body>
</html>
```

## 技术栈

- 纯 HTML/CSS/JavaScript
- 无框架依赖
- 响应式设计

## 部署

直接部署到任意静态托管服务即可（GitHub Pages、Vercel、Netlify 等）。

## 许可证

MIT
