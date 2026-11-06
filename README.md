
<!DOCTYPE html>
<html lang="ru" data-theme="dark">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<meta name="theme-color" content="#0a0b10">
<title>FLOW</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Manrope:wght@400;500;600;700;800&family=Unbounded:wght@400;500;600&display=swap" rel="stylesheet">
<style>
*{box-sizing:border-box;-webkit-tap-highlight-color:transparent}
:root{--bg:#0a0b10;--card:rgba(255,255,255,.05);--card2:rgba(255,255,255,.08);--line:rgba(255,255,255,.1);--tx:#eef0f6;--mut:#8b91a4;--a1:#8b5cf6;--a2:#38bdf8;--sb:env(safe-area-inset-bottom,0px);--st:env(safe-area-inset-top,0px);--nav-h:96px}
[data-theme="light"]{--bg:#f3f5fa;--card:#fff;--card2:#eef1f8;--line:rgba(10,20,40,.09);--tx:#11131a;--mut:#5a6272}
[hidden]{display:none!important}
html,body{margin:0;padding:0;overscroll-behavior:none}
body{font-family:'Manrope',system-ui,sans-serif;background:var(--bg);color:var(--tx);min-height:100dvh;overflow-x:hidden;-webkit-font-smoothing:antialiased;transition:background .4s,color .4s}
button{font-family:inherit;touch-action:manipulation;-webkit-touch-callout:none}
:focus-visible{outline:2px solid var(--a1);outline-offset:3px;border-radius:10px}
svg{flex:0 0 auto}
.blobs{position:fixed;inset:0;overflow:hidden;pointer-events:none;z-index:0}
.blob{position:absolute;width:58vmax;height:58vmax;border-radius:50%;filter:blur(80px);opacity:.26;will-change:transform}
.b1{background:var(--a1);top:-22vmax;left:-22vmax;animation:f1 28s ease-in-out infinite}
.b2{background:var(--a2);bottom:-26vmax;right:-20vmax;animation:f2 34s ease-in-out infinite}
[data-theme="light"] .blob{opacity:.34}
@keyframes f1{0%,100%{transform:translate(0,0) scale(1)}50%{transform:translate(9vmax,7vmax) scale(1.18)}}
@keyframes f2{0%,100%{transform:translate(0,0) scale(1.1)}50%{transform:translate(-8vmax,-6vmax) scale(.9)}}
.app{position:relative;z-index:1;max-width:480px;margin:0 auto;padding:calc(14px + var(--st)) 16px calc(140px + var(--sb))}
.view{display:none}
.view.active{display:block;animation:fade .25s ease}
@keyframes fade{from{opacity:0;transform:translateY(6px)}to{opacity:1;transform:none}}
#v-home.active{display:flex;flex-direction:column;min-height:calc(100dvh - var(--st) - var(--sb) - 14px - 140px)}
#v-home .center-block{flex:1;display:flex;flex-direction:column;align-items:center;justify-content:center;padding:8px 0}
h1.h1{font-family:'Unbounded',sans-serif;font-size:22px;font-weight:500;margin:6px 0 4px;letter-spacing:-.01em}
h2.h2{font-family:'Unbounded',sans-serif;font-size:14px;font-weight:500;margin:22px 0 10px}
.p{font-size:13.5px;line-height:1.55;color:var(--mut);margin:0 0 14px}
.card{background:var(--card);border:1px solid var(--line);border-radius:20px;padding:16px;margin-bottom:12px;backdrop-filter:blur(14px);-webkit-backdrop-filter:blur(14px)}
.lbl{display:block;font-size:11.5px;font-weight:700;letter-spacing:.06em;text-transform:uppercase;color:var(--mut);margin-bottom:9px}
.input{width:100%;background:var(--card2);border:1px solid transparent;border-radius:13px;color:var(--tx);font:500 16px 'Manrope';padding:13px 14px;outline:none;transition:.2s}
.input:focus{border-color:var(--a1);background:var(--card)}
.topbar{display:flex;align-items:center;gap:8px;margin-bottom:6px}
.tb-right{margin-left:auto;display:flex;gap:6px}
.iconbtn{width:44px;height:44px;border-radius:50%;border:1px solid var(--line);background:var(--card);color:var(--tx);display:grid;place-items:center;cursor:pointer;transition:.2s}
.iconbtn:active{transform:scale(.93)}
.iconbtn svg{width:21px;height:21px}
.iconbtn.on{color:var(--a1);border-color:color-mix(in srgb,var(--a1) 55%,transparent);background:color-mix(in srgb,var(--a1) 16%,transparent)}
.rest-badge{display:flex;align-items:center;gap:7px;margin:0 auto 16px;padding:7px 15px;border-radius:100px;background:color-mix(in srgb,var(--a1) 15%,transparent);border:1px solid color-mix(in srgb,var(--a1) 38%,transparent);color:var(--a1);font:800 11px 'Manrope';letter-spacing:.12em;text-transform:uppercase;width:fit-content}
.rest-badge svg{width:13px;height:13px}
.timerwrap{position:relative;width:min(88vw,360px);aspect-ratio:1;margin:0 auto;cursor:pointer}
.timerwrap svg{width:100%;height:100%;display:block;transform:rotate(-90deg)}
.ring-bg{fill:none;stroke:var(--line);stroke-width:8}
.ring-fg{fill:none;stroke:url(#grad);stroke-width:8;stroke-linecap:round;transition:stroke-dashoffset .3s linear}
.ring-fg.warn{animation:ringSoft 1.4s ease-in-out infinite}
@keyframes ringSoft{50%{opacity:.55}}
.timer-center{position:absolute;inset:0;display:flex;flex-direction:column;align-items:center;justify-content:center;pointer-events:none}
.breathe{position:absolute;width:66%;aspect-ratio:1;border-radius:50%;background:radial-gradient(circle at 38% 32%,var(--a1),transparent 70%);opacity:.22;filter:blur(22px);animation:breathe var(--br,6s) ease-in-out infinite}
@keyframes breathe{0%,100%{transform:scale(.84)}40%{transform:scale(1)}}
.time{font-family:'Unbounded',sans-serif;font-size:clamp(42px,13vw,58px);font-weight:500;letter-spacing:-.025em;line-height:1;font-variant-numeric:tabular-nums;position:relative}
.sub{margin-top:14px;font-size:13px;font-weight:700;color:var(--mut);max-width:78%;text-align:center;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;position:relative;transition:opacity .3s,visibility .3s}
.controls{display:flex;align-items:center;gap:14px;margin-top:26px;width:100%;max-width:360px}
.ctl{width:62px;height:62px;border-radius:50%;border:1px solid var(--line);background:var(--card);color:var(--tx);display:grid;place-items:center;cursor:pointer;flex:0 0 auto;transition:.18s}
.ctl:active{transform:scale(.9)}
.ctl svg{width:26px;height:26px}
.bigbtn{flex:1;height:72px;border:0;border-radius:24px;cursor:pointer;background:linear-gradient(135deg,var(--a1),var(--a2));color:#fff;font-family:'Unbounded',sans-serif;font-size:17px;font-weight:500;letter-spacing:.02em;box-shadow:0 16px 38px -12px var(--a1);transition:transform .16s,box-shadow .25s;display:flex;align-items:center;justify-content:center;gap:11px}
.bigbtn:active{transform:scale(.96)}
.bigbtn svg{width:24px;height:24px}
.links{display:flex;flex-direction:column;gap:2px;margin-top:16px}
.linkbtn{border:0;background:none;color:var(--a2);font:700 13.5px 'Manrope';padding:13px;border-radius:14px;cursor:pointer;transition:.18s;min-height:48px}
[data-theme="light"] .linkbtn{color:var(--a1)}
.linkbtn:active{background:var(--card2)}
.linkbtn.danger{color:#f87171}
.ideacard{font-size:13.5px;line-height:1.5;color:var(--mut);display:none;margin-top:20px}
.ideacard.on{display:block}
.ideacard b{color:var(--tx);font-weight:700}
.modecard{display:block;width:100%;text-align:left;border:1px solid var(--line);background:var(--card);border-radius:17px;padding:15px 17px;margin-bottom:9px;cursor:pointer;color:var(--tx);transition:.2s}
.modecard.active{border-color:transparent;background:linear-gradient(135deg,color-mix(in srgb,var(--a1) 22%,var(--card)),color-mix(in srgb,var(--a2) 16%,var(--card)));box-shadow:inset 0 0 0 1.5px color-mix(in srgb,var(--a1) 60%,transparent)}
.mname{font:700 15px 'Manrope';margin-bottom:3px}
.mvals{font-size:12px;color:var(--mut);font-weight:600}
.slider{margin-bottom:16px}
.slider:last-child{margin-bottom:0}
.slider label{display:flex;justify-content:space-between;font-size:13px;font-weight:700;margin-bottom:11px}
.slider label b{color:var(--a2);font-weight:800}
[data-theme="light"] .slider label b{color:var(--a1)}
input[type=range]{-webkit-appearance:none;appearance:none;width:100%;height:6px;border-radius:6px;background:var(--line);outline:none;margin:0}
input[type=range]::-webkit-slider-thumb{-webkit-appearance:none;width:26px;height:26px;border-radius:50%;background:linear-gradient(135deg,var(--a1),var(--a2));cursor:pointer;border:2.5px solid var(--bg)}
input[type=range]::-moz-range-thumb{width:26px;height:26px;border-radius:50%;border:2.5px solid var(--bg);background:var(--a1);cursor:pointer}
.summary{font-size:13px;line-height:1.7;color:var(--mut)}
.summary b{color:var(--tx);font-weight:800}
.row{display:flex;align-items:center;justify-content:space-between;gap:14px;padding:14px 0;border-bottom:1px solid var(--line);font-size:14px;font-weight:600;cursor:pointer;min-height:52px}
.row:last-child{border-bottom:0}
.row span{flex:1}
.row.disabled{opacity:.45;cursor:not-allowed}
.sw{position:absolute;opacity:0;width:0;height:0;pointer-events:none}
.sw+i{width:48px;height:28px;border-radius:14px;background:var(--line);position:relative;transition:.25s;flex:0 0 auto;display:block}
.sw+i::after{content:'';position:absolute;top:4px;left:4px;width:20px;height:20px;border-radius:50%;background:var(--mut);transition:.25s}
.sw:checked+i{background:linear-gradient(135deg,var(--a1),var(--a2))}
.sw:checked+i::after{transform:translateX(20px);background:#fff}
.sw:disabled+i{opacity:.4}
.cat{border:1px solid var(--line);background:var(--card);border-radius:18px;overflow:hidden;margin-bottom:9px}
.cathead{display:flex;align-items:center;gap:12px;width:100%;padding:16px;background:none;border:0;color:var(--tx);font:700 13.5px 'Manrope';cursor:pointer;text-align:left;min-height:56px}
.cathead svg.ic{width:21px;height:21px;color:var(--a1);flex:0 0 auto}
.cathead .chev{margin-left:auto;color:var(--mut);transition:transform .25s;flex:0 0 auto;width:16px;height:16px}
.cat.open .chev{transform:rotate(90deg)}
.catbody{display:none;padding:0 16px 16px}
.cat.open .catbody{display:block}
.ideas{list-style:none;margin:0 0 12px;padding:0;display:flex;flex-direction:column;gap:7px}
.ideas li{position:relative;padding-left:15px;font-size:13px;line-height:1.45;color:var(--mut)}
.ideas li::before{content:'';position:absolute;left:0;top:7px;width:5px;height:5px;border-radius:50%;background:var(--a2);opacity:.8}
.sbtn{display:inline-flex;align-items:center;gap:7px;border:1px solid var(--line);background:var(--card2);color:var(--tx);border-radius:12px;padding:12px 16px;font:700 12.5px 'Manrope';cursor:pointer;min-height:44px}
.sbtn.primary{background:linear-gradient(135deg,var(--a1),var(--a2));color:#fff;border-color:transparent}
.sounds{display:flex;flex-wrap:wrap;gap:7px;margin-bottom:14px}
.snd{border:1px solid var(--line);background:var(--card2);color:var(--tx);border-radius:11px;padding:11px 13px;font:700 12px 'Manrope';cursor:pointer;min-height:44px}
.snd.active{background:linear-gradient(135deg,var(--a1),var(--a2));color:#fff;border-color:transparent}
.volrow{display:flex;align-items:center;gap:12px;margin-bottom:14px}
.volrow svg{width:18px;height:18px;color:var(--mut)}
.stats3{display:grid;grid-template-columns:repeat(3,1fr);gap:9px;margin-bottom:12px}
.stat{background:var(--card);border:1px solid var(--line);border-radius:17px;padding:15px 10px;text-align:center}
.stat b{display:block;font-family:'Unbounded',sans-serif;font-size:22px;font-weight:500;line-height:1.1}
.stat span{display:block;font-size:10.5px;font-weight:700;color:var(--mut);margin-top:6px;letter-spacing:.03em}
.rec{font-size:13.5px;line-height:1.55;color:var(--tx)}
.bars{display:flex;align-items:flex-end;gap:6px;height:108px;padding-top:8px}
.bar{flex:1;display:flex;flex-direction:column;align-items:center;gap:7px;height:100%}
.btrack{flex:1;width:100%;display:flex;align-items:flex-end;border-radius:7px;background:var(--card2);overflow:hidden}
.btrack i{display:block;width:100%;border-radius:7px;background:linear-gradient(180deg,var(--a2),var(--a1));transition:height .5s ease;min-height:0}
.bar span{font-size:10px;font-weight:700;color:var(--mut)}
.hrow{display:flex;align-items:baseline;gap:10px;padding:10px 0;border-bottom:1px solid var(--line);font-size:12.5px}
.hrow:last-child{border-bottom:0}
.hdate{color:var(--mut);font-weight:600;flex:0 0 auto}
.hmode{flex:1;font-weight:700;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.hmin{font-weight:800}
.hmin em{font-style:normal;color:var(--mut);font-weight:600;font-size:11px}
#v-tasks .empty-state{display:flex;flex-direction:column;align-items:center;justify-content:center;padding:60px 20px;text-align:center;color:var(--mut)}
#v-tasks .empty-state svg{width:64px;height:64px;opacity:.35;margin-bottom:20px}
#v-tasks .empty-state p{font-size:14px;line-height:1.55;max-width:280px;margin:0}
.profile-header{display:flex;align-items:center;gap:14px;padding:8px 0 22px}
.avatar{width:68px;height:68px;border-radius:50%;flex:0 0 auto;background:linear-gradient(135deg,var(--a1),var(--a2));display:grid;place-items:center;font-family:'Unbounded',sans-serif;font-size:26px;font-weight:500;color:#fff;box-shadow:0 10px 26px -10px var(--a1)}
.profile-name-wrap{flex:1;min-width:0}
.profile-nick{font-family:'Unbounded',sans-serif;font-size:18px;font-weight:500;letter-spacing:-.01em;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;margin-bottom:4px;color:var(--tx)}
.profile-edit{border:0;background:none;color:var(--a2);font:700 12px 'Manrope';cursor:pointer;padding:0;text-decoration:underline;text-decoration-color:color-mix(in srgb,var(--a2) 35%,transparent);text-underline-offset:3px}
[data-theme="light"] .profile-edit{color:var(--a1)}
.section-btn{display:flex;align-items:center;gap:12px;width:100%;padding:16px 18px;margin-bottom:8px;border:1px solid var(--line);background:var(--card);border-radius:16px;color:var(--tx);font:700 14px 'Manrope';cursor:pointer;text-align:left;min-height:56px;transition:.2s}
.section-btn svg.ico{width:20px;height:20px;color:var(--a1);flex:0 0 auto}
.section-btn > span{flex:1}
.section-btn .chev{width:16px;height:16px;color:var(--mut);transition:transform .25s;flex:0 0 auto}
.section-btn.open{border-color:color-mix(in srgb,var(--a1) 40%,transparent);background:color-mix(in srgb,var(--a1) 8%,var(--card))}
.section-btn.open .chev{transform:rotate(90deg)}
.section-content{background:var(--card);border:1px solid var(--line);border-radius:16px;padding:16px;margin-bottom:10px}
.seg{display:flex;gap:5px;background:var(--card2);padding:4px;border-radius:14px}
.seg button{flex:1;border:0;background:none;color:var(--mut);font:700 12.5px 'Manrope';padding:11px 4px;border-radius:11px;cursor:pointer;min-height:42px}
.seg button.active{background:var(--card);color:var(--tx)}
.themes{display:grid;grid-template-columns:repeat(3,1fr);gap:9px}
.theme{border:1.5px solid var(--line);background:var(--card2);border-radius:15px;padding:8px;cursor:pointer;display:flex;flex-direction:column;gap:7px;align-items:center}
.theme.active{border-color:var(--a1)}
.tswatch{width:100%;height:34px;border-radius:10px}
.theme span{font-size:10.5px;font-weight:700;color:var(--mut)}
.theme.active span{color:var(--tx)}
.dangerbtn{width:100%;border:1px solid var(--line);background:var(--card2);color:#f87171;border-radius:14px;padding:14px;font:700 13.5px 'Manrope';cursor:pointer;min-height:48px}
.dangerbtn.armed{background:#f87171;color:#fff;border-color:transparent}
.exportrow{display:flex;gap:8px;margin-bottom:8px}
.exportrow .sbtn{flex:1;justify-content:center}
.foot{font-size:11.5px;line-height:1.65;color:var(--mut);text-align:center;padding:22px 12px 8px}
.lang-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:8px}
.lang-btn{display:flex;align-items:center;gap:10px;padding:13px 15px;border:1px solid var(--line);background:var(--card2);color:var(--tx);border-radius:14px;font:700 13px 'Manrope';cursor:pointer;text-align:left;min-height:50px;transition:.2s}
.lang-btn.active{border-color:var(--a1);background:color-mix(in srgb,var(--a1) 12%,var(--card2))}
.lang-btn .flag{font-family:'Unbounded',sans-serif;font-weight:600;font-size:11.5px;color:var(--a1);min-width:28px;letter-spacing:.04em}
.nav{position:fixed;left:0;right:0;bottom:0;z-index:30;display:flex;justify-content:center;padding:0 12px calc(12px + var(--sb));pointer-events:none;transition:transform .4s cubic-bezier(.2,.8,.2,1), opacity .28s ease}
.nav-inner{pointer-events:auto;display:flex;gap:5px;width:100%;max-width:460px;background:color-mix(in srgb,var(--bg) 82%,transparent);backdrop-filter:blur(24px);-webkit-backdrop-filter:blur(24px);border:1px solid var(--line);border-radius:26px;padding:10px;box-shadow:0 12px 40px -14px rgba(0,0,0,.6)}
.nav.hide{transform:translateY(calc(100% + 24px));opacity:0}
.nav.hide .nav-inner{pointer-events:none}
.navbtn{flex:1;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:5px;padding:12px 4px;border:0;background:none;color:var(--mut);font:700 11px 'Manrope';border-radius:20px;cursor:pointer;min-height:68px;position:relative}
.navbtn svg{width:26px;height:26px}
.navbtn.active{color:var(--tx);background:linear-gradient(135deg,color-mix(in srgb,var(--a1) 24%,transparent),color-mix(in srgb,var(--a2) 16%,transparent));box-shadow:inset 0 0 0 1px color-mix(in srgb,var(--a1) 30%,transparent)}
.navbtn.active svg{color:var(--a1)}
.navbtn.active::after{content:'';position:absolute;bottom:6px;width:18px;height:2.5px;border-radius:2px;background:linear-gradient(90deg,var(--a1),var(--a2))}
.minitimer{position:fixed;left:50%;transform:translateX(-50%);bottom:calc(var(--nav-h) + var(--sb) + 6px);z-index:25;display:flex;align-items:center;gap:10px;padding:8px 8px 8px 14px;border-radius:100px;background:color-mix(in srgb,var(--bg) 90%,transparent);border:1px solid var(--line);backdrop-filter:blur(20px);-webkit-backdrop-filter:blur(20px);font:700 13px 'Manrope';max-width:calc(100vw - 24px);cursor:pointer;min-height:44px}
.minitimer[hidden]{display:none}
.mt-dot{width:8px;height:8px;border-radius:50%;background:var(--a1);flex:0 0 auto}
.mt-dot.paused{background:var(--mut)}
.mt-time{font-family:'Unbounded';font-weight:500;font-variant-numeric:tabular-nums}
.mt-phase{color:var(--mut);font-weight:600;font-size:12px;max-width:110px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.mt-btn{width:36px;height:36px;border-radius:50%;border:0;background:var(--card2);color:var(--tx);display:grid;place-items:center;cursor:pointer;flex:0 0 auto}
.mt-btn svg{width:16px;height:16px}
.ov{position:fixed;inset:0;z-index:100;background:#000;display:flex;align-items:center;justify-content:center;padding:24px;text-align:center;animation:ovin .4s ease}
@keyframes ovin{from{opacity:0}to{opacity:1}}
.ov-inner{max-width:340px;width:100%;display:flex;flex-direction:column;align-items:center}
.ov h2{font-family:'Unbounded',sans-serif;font-size:19px;font-weight:500;color:#fff;margin:0 0 10px;line-height:1.3}
.ov p{font-size:13.5px;line-height:1.55;color:#8b91a4;margin:0 0 24px;max-width:280px}
.gcircle{width:150px;height:150px;border-radius:50%;margin-bottom:26px;background:radial-gradient(circle at 40% 35%,var(--a1),transparent 68%);opacity:.4;filter:blur(14px);transform:scale(.8)}
.gcount{font-family:'Unbounded',sans-serif;font-size:46px;font-weight:400;color:#fff;margin-bottom:26px;line-height:1;min-height:46px}
.ghost{border:1px solid rgba(255,255,255,.16);background:none;color:#c7cbd8;border-radius:16px;padding:14px 30px;font:700 13.5px 'Manrope';cursor:pointer;margin-top:4px;min-height:44px}
.sleep{background:#000;flex-direction:column;gap:18px}
.sleepclock{font-family:'Unbounded',sans-serif;font-size:64px;font-weight:300;color:#fff;opacity:.9}
.sleephint{font-size:12px;color:#333;font-weight:600}
.ov-rest{background:#000;padding:24px}
.ov-rest-inner{display:flex;flex-direction:column;align-items:center;justify-content:center;width:100%;max-width:340px;text-align:center;min-height:100%}
.rest-breath{width:190px;height:190px;border-radius:50%;background:radial-gradient(circle at 40% 35%,var(--a1),transparent 72%);opacity:.10;filter:blur(40px);animation:restBreath 10s ease-in-out infinite;margin-bottom:52px}
@keyframes restBreath{0%,100%{transform:scale(.78);opacity:.08}50%{transform:scale(1.28);opacity:.22}}
.rest-title{font-family:'Unbounded',sans-serif;font-size:20px;font-weight:400;color:rgba(255,255,255,.55);margin:0 0 12px;line-height:1.35}
.rest-sub{font-size:12.5px;line-height:1.55;color:rgba(255,255,255,.22);margin:0 0 44px;max-width:260px}
.rest-count{font-family:'Unbounded',sans-serif;font-size:11px;font-weight:400;color:rgba(255,255,255,.13);letter-spacing:.14em;font-variant-numeric:tabular-nums;margin-bottom:4px}
.rest-go{background:none;border:1px solid rgba(255,255,255,.2);color:rgba(255,255,255,.72);padding:14px 36px;border-radius:16px;font:600 14px 'Manrope';cursor:pointer;margin-top:30px;min-height:48px}
.rest-skip{background:none;border:0;color:rgba(255,255,255,.32);padding:12px 24px;font:600 13px 'Manrope';cursor:pointer;margin-top:22px;min-height:44px;letter-spacing:.02em;animation:ovin .4s ease}
.rest-skip:active{color:rgba(255,255,255,.65)}
.sheet{position:fixed;inset:0;z-index:150;display:flex;align-items:flex-end;justify-content:center}
.sheet-bg{position:absolute;inset:0;background:rgba(0,0,0,.55)}
.sheet-panel{position:relative;width:100%;max-width:480px;background:var(--bg);border-radius:24px 24px 0 0;padding:12px 20px calc(20px + var(--sb));border-top:1px solid var(--line);animation:up .3s ease;max-height:90vh;overflow-y:auto}
@keyframes up{from{transform:translateY(100%)}to{transform:none}}
.sheet-handle{width:38px;height:4px;border-radius:2px;background:var(--line);margin:0 auto 16px}
.sheet h2{font-family:'Unbounded';font-size:16px;font-weight:500;margin:0 0 8px}
.sheet p{font-size:13px;color:var(--mut);line-height:1.5;margin:0 0 14px}
.park-actions{display:flex;gap:8px;margin-top:14px}
.park-actions .sbtn{flex:1;justify-content:center}
.onb{position:fixed;inset:0;z-index:180;background:rgba(5,6,10,.94);display:flex;align-items:center;justify-content:center;padding:24px;backdrop-filter:blur(10px);-webkit-backdrop-filter:blur(10px)}
.onb-content{max-width:380px;width:100%;background:var(--card);border:1px solid var(--line);border-radius:24px;padding:28px 24px;text-align:center}
.onb-content h2{font-family:'Unbounded';font-size:19px;font-weight:500;margin:0 0 12px;color:var(--tx);line-height:1.3}
.onb-content p{font-size:14px;line-height:1.55;color:var(--mut);margin:0 0 20px}
.onb-content .bigbtn{width:100%;margin-bottom:8px}
.onb-dots{display:flex;gap:6px;justify-content:center;margin:16px 0}
.onb-dots i{width:6px;height:6px;border-radius:50%;background:var(--line)}
.onb-dots i.on{background:var(--a1);width:20px;border-radius:3px}
@media (prefers-reduced-motion:reduce){.blob,.breathe,.minitimer,.view,.rest-breath,.ring-fg.warn{animation:none!important}*{transition-duration:.01ms!important}}
</style>
</head>
<body>

<div class="blobs" aria-hidden="true"><div class="blob b1"></div><div class="blob b2"></div></div>

<div class="app" id="app">
  <main id="v-home" class="view active">
    <div class="topbar">
      <button class="iconbtn" id="btnModes" data-i18n-aria="modes">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.7" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M4 7h16M4 12h16M4 17h16"/><circle cx="9" cy="7" r="2" fill="var(--bg)"/><circle cx="15" cy="12" r="2" fill="var(--bg)"/><circle cx="7" cy="17" r="2" fill="var(--bg)"/></svg>
      </button>
      <div class="tb-right"><button class="iconbtn" id="btnMute"></button></div>
    </div>
    <div class="center-block">
      <div class="rest-badge" id="restBadge" hidden>
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M20 14.5A8 8 0 0 1 9.5 4 8 8 0 1 0 20 14.5z"/></svg>
        <span id="restBadgeText"></span>
      </div>
      <div class="timerwrap" id="timerwrap">
        <svg viewBox="0 0 260 260" aria-hidden="true">
          <defs><linearGradient id="grad" x1="0" y1="0" x2="1" y2="1"><stop offset="0%" stop-color="var(--a1)"/><stop offset="100%" stop-color="var(--a2)"/></linearGradient></defs>
          <circle class="ring-bg" cx="130" cy="130" r="118"/>
          <circle class="ring-fg" id="ring" cx="130" cy="130" r="118"/>
        </svg>
        <div class="timer-center">
          <div class="breathe" id="breathe"></div>
          <div class="time" id="timeText">25:00</div>
          <div class="sub" id="subText" aria-live="polite"></div>
        </div>
      </div>
      <div class="controls">
        <button class="ctl" id="btnReset" data-i18n-aria="reset"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M3.5 12a8.5 8.5 0 1 0 2.6-6.1"/><path d="M3.5 4.5v5h5"/></svg></button>
        <button class="bigbtn" id="btnStart"><span></span></button>
        <button class="ctl" id="btnSkip" data-i18n-aria="skip_label"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M6 5.5 15 12l-9 6.5z"/><path d="M19 5v14"/></svg></button>
      </div>
    </div>
    <div class="links">
      <button class="linkbtn" id="btnEasy" data-i18n="easy_start"></button>
      <button class="linkbtn danger" id="btnEndSess" data-i18n="end_session"></button>
    </div>
    <div class="card ideacard" id="restIdea"></div>
  </main>

  <main id="v-modes" class="view">
    <h1 class="h1" data-i18n="modes"></h1>
    <p class="p" data-i18n="modes_sub"></p>
    <div id="modeList"></div>
    <h2 class="h2" data-i18n="custom_mode"></h2>
    <div class="card">
      <div class="slider"><label><span data-i18n="work"></span> <b><span id="lw">25</span> <span data-i18n="min"></span></b></label><input type="range" id="sw" min="2" max="120" step="1" value="25"></div>
      <div class="slider"><label><span data-i18n="short_rest"></span> <b><span id="lr">5</span> <span data-i18n="min"></span></b></label><input type="range" id="sr" min="2" max="30" step="1" value="5"></div>
      <div class="slider"><label><span data-i18n="long_rest_label"></span> <b><span id="ll">15</span> <span data-i18n="min"></span></b></label><input type="range" id="sl" min="2" max="60" step="1" value="15"></div>
      <div class="slider"><label><span data-i18n="cycles"></span> <b><span id="lc">4</span></b></label><input type="range" id="sc" min="1" max="8" step="1" value="4"></div>
      <label class="row" style="border-top:1px solid var(--line);margin-top:4px"><span data-i18n="auto_switch"></span><input type="checkbox" class="sw" id="tgAuto" checked><i></i></label>
    </div>
    <div class="card summary" id="customSummary"></div>
  </main>

  <main id="v-tasks" class="view">
    <h1 class="h1" data-i18n="tasks"></h1>
    <div class="empty-state">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.4" stroke-linecap="round" stroke-linejoin="round"><rect x="4" y="5" width="3" height="3" rx="1"/><rect x="4" y="11" width="3" height="3" rx="1"/><rect x="4" y="17" width="3" height="3" rx="1"/><path d="M10 6.5h10M10 12.5h10M10 18.5h10"/></svg>
      <p data-i18n="tasks_empty"></p>
    </div>
  </main>

  <main id="v-rest" class="view">
    <h1 class="h1" data-i18n="rest_title"></h1>
    <p class="p" data-i18n="rest_sub"></p>
    <div class="cat open">
      <button class="cathead">
        <svg class="ic" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"><path d="M3 13.5c3-3.2 6-3.2 9 0s6 3.2 9 0"/><path d="M6.5 7.5 5.5 5M12 6.5V3.5M17.5 7.5l1-2"/></svg>
        <span data-i18n="relaxation"></span>
        <svg class="chev" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><path d="m9 6 6 6-6 6"/></svg>
      </button>
      <div class="catbody"><ul class="ideas"><li data-i18n="idea1"></li><li data-i18n="idea2"></li><li data-i18n="idea3"></li></ul></div>
    </div>
    <div class="cat">
      <button class="cathead">
        <svg class="ic" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"><path d="M9 17.5V5l10-2v12.5"/><circle cx="6" cy="17.5" r="3"/><circle cx="16" cy="15.5" r="3"/></svg>
        <span data-i18n="music_sounds"></span>
        <svg class="chev" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><path d="m9 6 6 6-6 6"/></svg>
      </button>
      <div class="catbody">
        <div class="sounds" id="sounds">
          <button class="snd active" data-s="none" data-i18n="silence"></button>
          <button class="snd" data-s="white" data-i18n="white_noise"></button>
          <button class="snd" data-s="brown" data-i18n="brown_noise"></button>
          <button class="snd" data-s="rain" data-i18n="rain"></button>
          <button class="snd" data-s="ocean" data-i18n="ocean"></button>
          <button class="snd" data-s="ambient" data-i18n="ambient"></button>
        </div>
        <div class="volrow">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"><path d="M4 9v6h4l5 4V5L8 9H4z"/><path d="M16.5 8.5a5 5 0 0 1 0 7"/></svg>
          <input type="range" id="volRange" min="0" max="100" value="50">
        </div>
      </div>
    </div>
    <div class="cat">
      <button class="cathead">
        <svg class="ic" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"><path d="M3 8h9a3 3 0 1 0-3-3"/><path d="M3 12h13a3 3 0 1 1-3 3"/><path d="M3 16h6"/></svg>
        <span data-i18n="breathing"></span>
        <svg class="chev" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><path d="m9 6 6 6-6 6"/></svg>
      </button>
      <div class="catbody"><ul class="ideas"><li data-i18n="breath_idea1"></li><li data-i18n="breath_idea2"></li></ul></div>
    </div>
  </main>

  <main id="v-stats" class="view">
    <h1 class="h1" data-i18n="stats"></h1>
    <p class="p" data-i18n="stats_sub"></p>
    <div class="stats3">
      <div class="stat"><b id="statToday">0</b><span data-i18n="today_min"></span></div>
      <div class="stat"><b id="statWeek">0</b><span data-i18n="week_min"></span></div>
      <div class="stat"><b id="statTotal">0</b><span data-i18n="total_sessions"></span></div>
    </div>
    <div class="card"><div class="rec" id="statRec">—</div></div>
    <h2 class="h2" data-i18n="last_7_days"></h2>
    <div class="card"><div class="bars" id="bars"></div></div>
    <h2 class="h2" data-i18n="history"></h2>
    <div class="card" id="history"></div>
  </main>

  <main id="v-profile" class="view">
    <div class="profile-header">
      <div class="avatar" id="avatarEl">U</div>
      <div class="profile-name-wrap">
        <div class="profile-nick" id="nickEl"></div>
        <button class="profile-edit" id="btnEditNick" data-i18n="edit_name"></button>
      </div>
    </div>
    <button class="section-btn" data-target="sec-lang">
      <svg class="ico" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.7" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="9"/><path d="M3 12h18M12 3a14 14 0 0 1 0 18a14 14 0 0 1 0-18z"/></svg>
      <span data-i18n="language"></span>
      <svg class="chev" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="m9 6 6 6-6 6"/></svg>
    </button>
    <div class="section-content" id="sec-lang" hidden><div class="lang-grid" id="langList"></div></div>
    <button class="section-btn" data-target="sec-theme">
      <svg class="ico" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.7" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="4.5"/><path d="M12 2.5v2M12 19.5v2M2.5 12h2M19.5 12h2"/></svg>
      <span data-i18n="theme"></span>
      <svg class="chev" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="m9 6 6 6-6 6"/></svg>
    </button>
    <div class="section-content" id="sec-theme" hidden>
      <div class="seg" id="segTheme">
        <button data-th="auto" data-i18n="theme_auto"></button>
        <button data-th="light" data-i18n="theme_light"></button>
        <button data-th="dark" data-i18n="theme_dark"></button>
      </div>
    </div>
    <button class="section-btn" data-target="sec-colors">
      <svg class="ico" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.7" stroke-linecap="round" stroke-linejoin="round"><circle cx="9" cy="9" r="5"/><circle cx="15" cy="15" r="5"/></svg>
      <span data-i18n="colors"></span>
      <svg class="chev" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="m9 6 6 6-6 6"/></svg>
    </button>
    <div class="section-content" id="sec-colors" hidden><div class="themes" id="themeList"></div></div>
    <button class="section-btn" data-target="sec-behavior">
      <svg class="ico" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.7" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="4"/><path d="M12 3v3M12 18v3M3 12h3M18 12h3"/></svg>
      <span data-i18n="behavior"></span>
      <svg class="chev" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="m9 6 6 6-6 6"/></svg>
    </button>
    <div class="section-content" id="sec-behavior" hidden>
      <label class="row"><span data-i18n="beep"></span><input type="checkbox" class="sw" id="tgBeep"><i></i></label>
      <label class="row"><span data-i18n="vibration"></span><input type="checkbox" class="sw" id="tgVib"><i></i></label>
      <label class="row" id="notifRow"><span id="notifLbl" data-i18n="notifications"></span><input type="checkbox" class="sw" id="tgNotif"><i></i></label>
    </div>
    <button class="section-btn" data-target="sec-data">
      <svg class="ico" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.7" stroke-linecap="round" stroke-linejoin="round"><ellipse cx="12" cy="5.5" rx="7" ry="2.5"/><path d="M5 5.5v13c0 1.4 3.1 2.5 7 2.5s7-1.1 7-2.5v-13"/></svg>
      <span data-i18n="data"></span>
      <svg class="chev" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="m9 6 6 6-6 6"/></svg>
    </button>
    <div class="section-content" id="sec-data" hidden>
      <div class="exportrow"><button class="sbtn" id="btnExport" data-i18n="download_copy"></button><button class="sbtn" id="btnImport" data-i18n="restore"></button></div>
      <input type="file" id="importFile" accept="application/json,.json" hidden>
      <button class="dangerbtn" id="btnDel" style="margin-top:6px" data-i18n="delete_history"></button>
    </div>
    <p class="foot" data-i18n="foot1"></p>
  </main>
</div>

<nav class="nav">
  <div class="nav-inner">
    <button class="navbtn active" data-tab="home"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"><path d="M3 10.2 12 3l9 7.2"/><path d="M5.5 9.4V19a1.5 1.5 0 0 0 1.5 1.5h10a1.5 1.5 0 0 0 1.5-1.5V9.4"/></svg><span data-i18n="nav_home"></span></button>
    <button class="navbtn" data-tab="tasks"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"><rect x="4" y="5" width="3" height="3" rx="1"/><rect x="4" y="11" width="3" height="3" rx="1"/><rect x="4" y="17" width="3" height="3" rx="1"/><path d="M10 6.5h10M10 12.5h10M10 18.5h10"/></svg><span data-i18n="nav_tasks"></span></button>
    <button class="navbtn" data-tab="rest"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"><path d="M20 14.5A8 8 0 0 1 9.5 4 8 8 0 1 0 20 14.5z"/></svg><span data-i18n="nav_rest"></span></button>
    <button class="navbtn" data-tab="stats"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"><path d="M5 20V12M12 20V4M19 20v-6"/></svg><span data-i18n="nav_stats"></span></button>
    <button class="navbtn" data-tab="profile"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="8" r="3.6"/><path d="M4.5 20a7.5 7.5 0 0 1 15 0"/></svg><span data-i18n="nav_profile"></span></button>
  </div>
</nav>

<div class="minitimer" id="miniTimer" hidden>
  <span class="mt-dot" id="mtDot"></span>
  <span class="mt-time" id="mtTime">25:00</span>
  <span class="mt-phase" id="mtPhase"></span>
  <button class="mt-btn" id="mtBtn"><svg viewBox="0 0 24 24" fill="currentColor"><path d="M8 5.5 18 12 8 18.5z"/></svg></button>
</div>

<div class="ov ov-rest" id="ovPause" hidden>
  <div class="ov-rest-inner">
    <div class="rest-breath"></div>
    <h2 class="rest-title" id="pauseTitle"></h2>
    <p class="rest-sub" id="pauseSub"></p>
    <div class="rest-count" id="pauseCount">0:30</div>
    <button class="rest-go" id="pauseGo" hidden></button>
    <button class="rest-skip" id="pauseSkip" hidden></button>
  </div>
</div>

<div class="ov" id="ovGuide" hidden>
  <div class="ov-inner">
    <div class="gcircle" id="guideCircle"></div>
    <h2 id="guidePhase"></h2>
    <p id="guideHint"></p>
    <div class="gcount" id="guideCount"></div>
    <button class="ghost" id="guideEnd"></button>
  </div>
</div>

<div class="ov sleep" id="ovSleep" hidden>
  <div class="sleepclock" id="sleepClock">00:00</div>
  <div class="sleephint" data-i18n="sleep_hint"></div>
</div>

<div class="sheet" id="nickSheet" hidden>
  <div class="sheet-bg" id="nickBg"></div>
  <div class="sheet-panel">
    <div class="sheet-handle"></div>
    <h2 data-i18n="what_name"></h2>
    <p data-i18n="nick_hint"></p>
    <input id="nickInput" class="input" maxlength="24" autocomplete="off">
    <div class="park-actions">
      <button class="sbtn" id="nickCancel" data-i18n="cancel"></button>
      <button class="sbtn primary" id="nickSave" data-i18n="save"></button>
    </div>
  </div>
</div>

<div class="onb" id="onb" hidden>
  <div class="onb-content">
    <h2 id="onbTitle"></h2>
    <p id="onbText"></p>
    <div class="onb-dots" id="onbDots"><i class="on"></i><i></i><i></i><i></i></div>
    <button class="bigbtn" id="onbNext"></button>
    <button class="linkbtn" id="onbSkip"></button>
  </div>
</div>

<script>
(function(){
'use strict';

var LS_KEY='flow-v2',LS_ONB='flow-onboarded',SS_TAB='flow-tab',BCAST='flow-sync';
var LANGS=['ru','en','es','zh','ja'];
var LANG_NAMES={ru:'Русский',en:'English',es:'Español',zh:'中文',ja:'日本語'};
var LANG_FLAGS={ru:'RU',en:'EN',es:'ES',zh:'ZH',ja:'JP'};

/* ============ ЯЗЫК ============ */
var I18N={
  ru:{nav_home:'Главная',nav_tasks:'Задачи',nav_rest:'Отдых',nav_stats:'Статистика',nav_profile:'Профиль',
    easy_start:'Лёгкий старт: всего 2 минуты',end_session:'Завершить сессию',
    start:'Старт',pause:'Пауза',again:'Заново',done:'Готово',session_done:'Сессия завершена',
    focus:'Фокус',rest:'Отдых',long_rest:'Длинный отдых',
    modes:'Режимы',modes_sub:'Найди свой ритм.',custom_mode:'Свой режим',
    work:'Работа',short_rest:'Короткий отдых',long_rest_label:'Длинный отдых',cycles:'Циклов',min:'мин',auto_switch:'Автопереключение',
    cycle_1:'цикл',cycle_2:'цикла',cycle_5:'циклов',
    tasks:'Задачи',tasks_empty:'Пока пусто. Скоро здесь появится управление задачами.',
    rest_title:'Отдых',rest_sub:'Отдых — часть работы.',
    relaxation:'Расслабление',idea1:'Полежи 2 минуты с закрытыми глазами',idea2:'Отпусти челюсть и плечи',idea3:'Послушай тишину без телефона',
    music_sounds:'Музыка и звуки',silence:'Тишина',white_noise:'Белый шум',brown_noise:'Коричневый',rain:'Дождь',ocean:'Океан',ambient:'Эмбиент',
    breathing:'Дыхание',breath_idea1:'4-7-8: вдох 4, задержка 7, выдох 8',breath_idea2:'Квадратное: 4-4-4-4',
    stats:'Статистика',stats_sub:'Только факты.',today_min:'Сегодня, мин',week_min:'7 дней, мин',total_sessions:'Всего сессий',
    last_7_days:'Последние 7 дней',history:'История',empty:'Пока пусто.',
    user:'Пользователь',edit_name:'Изменить имя',language:'Язык',
    theme:'Тема',theme_auto:'Авто',theme_light:'Светлая',theme_dark:'Тёмная',
    colors:'Цвета',theme_cosmos:'Космос',theme_ocean:'Океан',theme_forest:'Лес',theme_mountains:'Горы',theme_rain:'Дождь',theme_city:'Ночной город',
    behavior:'Поведение',beep:'Звук сигнала',vibration:'Вибрация',notifications:'Уведомления',
    notifications_unsupported:'Уведомления (не поддерживаются)',notifications_denied:'Уведомления (запрещены)',
    data:'Данные',download_copy:'Скачать копию',restore:'Восстановить',delete_history:'Удалить всю историю',
    delete_confirm:'Нажмите ещё раз, чтобы подтвердить',
    foot1:'Данные хранятся только на устройстве. Штрафов и серий нет.',
    close_eyes:'Закрой глаза',nothing_do:'Ничего не делай. Просто дыши.',
    continue:'Продолжить',skip:'Пропустить',can_open:'Можно открывать глаза',slowly_open:'Медленно открой глаза и вернись к делу.',
    what_name:'Как тебя зовут?',nick_hint:'Имя видно только тебе на этом устройстве.',cancel:'Отмена',save:'Сохранить',
    work_done_title:'Работа завершена',work_done_body:'Пора отдохнуть.',
    session_end_title:'Сессия завершена',session_end_body:'Хорошая работа. Отдохни.',
    all_cycles:'Все циклы пройдены. Отдохни как следует.',
    rest_done_title:'Отдых закончен',rest_done_body:'Пора вернуться к работе.',
    rec_none:'Начни с лёгкого старта — всего 2 минуты.',
    rec_broken:'Больше половины последних сессий прерваны. Попробуй режимы покороче.',
    rec_today_long:'Сегодня уже много работы. Хороший момент для длинного отдыха.',
    rec_ready_deep:'Ты редко прерываешься. Можно попробовать Deep Focus.',
    rec_ok:'Ты в своём ритме. Не забывай про отдых.',
    easy_start_session:'Лёгкий старт',
    onb1_t:'Добро пожаловать в FLOW',onb1_b:'Работа и отдых в своём ритме. Без штрафов и серий.',
    onb2_t:'После работы — остановка',onb2_b:'Когда рабочий таймер закончился — 30 секунд с закрытыми глазами. Через 5 секунд можно пропустить.',
    onb3_t:'Отдых стартует сам',onb3_b:'После остановки таймер отдыха запустится автоматически.',
    onb4_t:'Профиль и языки',onb4_b:'В Профиле твоё имя, темы, языки, поведение и данные.',
    next:'Далее',onb_start:'Начать',onb_skip:'Пропустить',
    sleep_hint:'Коснитесь экрана, чтобы выйти',rest_idea_prefix:'Идея отдыха:',
    reset:'Сброс',skip_label:'Пропустить этап',
    mute_on:'Включить звук',mute_off:'Режим без звука',
    hour_short:'ч',part:'(часть)',
    mode_work:'работа',mode_rest:'отдых'},
  en:{nav_home:'Home',nav_tasks:'Tasks',nav_rest:'Rest',nav_stats:'Stats',nav_profile:'Profile',
    easy_start:'Easy start: just 2 minutes',end_session:'End session',
    start:'Start',pause:'Pause',again:'Again',done:'Done',session_done:'Session finished',
    focus:'Focus',rest:'Rest',long_rest:'Long rest',
    modes:'Modes',modes_sub:'Find your rhythm.',custom_mode:'Custom mode',
    work:'Work',short_rest:'Short rest',long_rest_label:'Long rest',cycles:'Cycles',min:'min',auto_switch:'Auto switch',
    cycle_1:'cycles',cycle_2:'cycles',cycle_5:'cycles',
    tasks:'Tasks',tasks_empty:'Nothing yet. Task management coming soon.',
    rest_title:'Rest',rest_sub:'Rest is part of the work.',
    relaxation:'Relaxation',idea1:'Lie still for 2 minutes with eyes closed',idea2:'Let go of your jaw and shoulders',idea3:'Listen to silence without your phone',
    music_sounds:'Music & sounds',silence:'Silence',white_noise:'White noise',brown_noise:'Brown noise',rain:'Rain',ocean:'Ocean',ambient:'Ambient',
    breathing:'Breathing',breath_idea1:'4-7-8: inhale 4, hold 7, exhale 8',breath_idea2:'Box: 4-4-4-4',
    stats:'Statistics',stats_sub:'Just facts.',today_min:'Today, min',week_min:'7 days, min',total_sessions:'Total sessions',
    last_7_days:'Last 7 days',history:'History',empty:'Nothing yet.',
    user:'User',edit_name:'Change name',language:'Language',
    theme:'Theme',theme_auto:'Auto',theme_light:'Light',theme_dark:'Dark',
    colors:'Colors',theme_cosmos:'Cosmos',theme_ocean:'Ocean',theme_forest:'Forest',theme_mountains:'Mountains',theme_rain:'Rain',theme_city:'Night city',
    behavior:'Behavior',beep:'Signal sound',vibration:'Vibration',notifications:'Notifications',
    notifications_unsupported:'Notifications (unsupported)',notifications_denied:'Notifications (blocked)',
    data:'Data',download_copy:'Download copy',restore:'Restore',delete_history:'Delete all history',
    delete_confirm:'Tap again to confirm',
    foot1:'Data is stored only on this device. No penalties or streaks.',
    close_eyes:'Close your eyes',nothing_do:'Do nothing. Just breathe.',
    continue:'Continue',skip:'Skip',can_open:'You can open your eyes',slowly_open:'Slowly open your eyes and return.',
    what_name:'What should I call you?',nick_hint:'The name is visible only to you on this device.',cancel:'Cancel',save:'Save',
    work_done_title:'Work finished',work_done_body:'Time to rest.',
    session_end_title:'Session finished',session_end_body:'Good job. Take a break.',
    all_cycles:'All cycles done. Take a long rest.',
    rest_done_title:'Rest finished',rest_done_body:'Time to get back to work.',
    rec_none:'Start with an easy start — just 2 minutes.',
    rec_broken:'More than half of recent sessions were interrupted. Try shorter modes.',
    rec_today_long:'A lot of work today. Good time for a long rest.',
    rec_ready_deep:'You rarely interrupt. Try Deep Focus.',
    rec_ok:'You are in your rhythm. Remember to rest.',
    easy_start_session:'Easy start',
    onb1_t:'Welcome to FLOW',onb1_b:'Work and rest at your own pace. No penalties, no streaks.',
    onb2_t:'After work — stop',onb2_b:'When the work timer ends — 30 seconds with eyes closed. You can skip after 5 seconds.',
    onb3_t:'Rest starts itself',onb3_b:'After the stop, the rest timer starts automatically.',
    onb4_t:'Profile and languages',onb4_b:'In Profile: name, themes, languages, behavior and data.',
    next:'Next',onb_start:'Start',onb_skip:'Skip',
    sleep_hint:'Tap the screen to exit',rest_idea_prefix:'Rest idea:',
    reset:'Reset',skip_label:'Skip phase',
    mute_on:'Unmute',mute_off:'Mute',
    hour_short:'h',part:'(part)',
    mode_work:'work',mode_rest:'rest'},
  es:{nav_home:'Inicio',nav_tasks:'Tareas',nav_rest:'Descanso',nav_stats:'Datos',nav_profile:'Perfil',
    easy_start:'Inicio fácil: solo 2 minutos',end_session:'Terminar sesión',
    start:'Iniciar',pause:'Pausa',again:'Otra vez',done:'Listo',session_done:'Sesión terminada',
    focus:'Enfoque',rest:'Descanso',long_rest:'Descanso largo',
    modes:'Modos',modes_sub:'Encuentra tu ritmo.',custom_mode:'Modo propio',
    work:'Trabajo',short_rest:'Descanso corto',long_rest_label:'Descanso largo',cycles:'Ciclos',min:'min',auto_switch:'Auto cambio',
    cycle_1:'ciclos',cycle_2:'ciclos',cycle_5:'ciclos',
    tasks:'Tareas',tasks_empty:'Aún vacío. Pronto aparecerá la gestión de tareas.',
    rest_title:'Descanso',rest_sub:'Descansar es parte del trabajo.',
    relaxation:'Relajación',idea1:'Recuéstate 2 minutos con los ojos cerrados',idea2:'Suelta la mandíbula y los hombros',idea3:'Escucha el silencio sin el móvil',
    music_sounds:'Música y sonidos',silence:'Silencio',white_noise:'Ruido blanco',brown_noise:'Ruido marrón',rain:'Lluvia',ocean:'Océano',ambient:'Ambiente',
    breathing:'Respiración',breath_idea1:'4-7-8: inhala 4, retén 7, exhala 8',breath_idea2:'Cuadrada: 4-4-4-4',
    stats:'Estadísticas',stats_sub:'Solo hechos.',today_min:'Hoy, min',week_min:'7 días, min',total_sessions:'Total sesiones',
    last_7_days:'Últimos 7 días',history:'Historial',empty:'Aún vacío.',
    user:'Usuario',edit_name:'Cambiar nombre',language:'Idioma',
    theme:'Tema',theme_auto:'Auto',theme_light:'Claro',theme_dark:'Oscuro',
    colors:'Colores',theme_cosmos:'Cosmos',theme_ocean:'Océano',theme_forest:'Bosque',theme_mountains:'Montañas',theme_rain:'Lluvia',theme_city:'Ciudad nocturna',
    behavior:'Comportamiento',beep:'Sonido de señal',vibration:'Vibración',notifications:'Notificaciones',
    notifications_unsupported:'Notificaciones (no soportadas)',notifications_denied:'Notificaciones (bloqueadas)',
    data:'Datos',download_copy:'Descargar copia',restore:'Restaurar',delete_history:'Borrar todo el historial',
    delete_confirm:'Toca otra vez para confirmar',
    foot1:'Los datos se guardan solo en este dispositivo. Sin castigos ni rachas.',
    close_eyes:'Cierra los ojos',nothing_do:'No hagas nada. Solo respira.',
    continue:'Continuar',skip:'Saltar',can_open:'Puedes abrir los ojos',slowly_open:'Abre los ojos despacio y vuelve.',
    what_name:'¿Cómo te llamas?',nick_hint:'El nombre solo lo ves tú en este dispositivo.',cancel:'Cancelar',save:'Guardar',
    work_done_title:'Trabajo terminado',work_done_body:'Hora de descansar.',
    session_end_title:'Sesión terminada',session_end_body:'Buen trabajo. Descansa.',
    all_cycles:'Todos los ciclos completados. Descansa bien.',
    rest_done_title:'Descanso terminado',rest_done_body:'Hora de volver al trabajo.',
    rec_none:'Empieza con un inicio fácil — solo 2 minutos.',
    rec_broken:'Más de la mitad de las últimas sesiones se interrumpieron. Prueba modos más cortos.',
    rec_today_long:'Hoy ya has trabajado mucho. Buen momento para un descanso largo.',
    rec_ready_deep:'Rara vez interrumpes. Prueba Deep Focus.',
    rec_ok:'Estás en tu ritmo. No olvides descansar.',
    easy_start_session:'Inicio fácil',
    onb1_t:'Bienvenido a FLOW',onb1_b:'Trabajo y descanso a tu ritmo. Sin castigos ni rachas.',
    onb2_t:'Después del trabajo — pausa',onb2_b:'Cuando termina el temporizador — 30 segundos con ojos cerrados. Puedes saltar a los 5 segundos.',
    onb3_t:'El descanso empieza solo',onb3_b:'Después de la pausa, el temporizador de descanso arranca automáticamente.',
    onb4_t:'Perfil e idiomas',onb4_b:'En Perfil: nombre, temas, idiomas, comportamiento y datos.',
    next:'Siguiente',onb_start:'Empezar',onb_skip:'Saltar',
    sleep_hint:'Toca la pantalla para salir',rest_idea_prefix:'Idea de descanso:',
    reset:'Reiniciar',skip_label:'Saltar fase',
    mute_on:'Activar sonido',mute_off:'Silenciar',
    hour_short:'h',part:'(parcial)',
    mode_work:'trabajo',mode_rest:'descanso'},
  zh:{nav_home:'首页',nav_tasks:'任务',nav_rest:'休息',nav_stats:'统计',nav_profile:'我的',
    easy_start:'轻松开始：只需 2 分钟',end_session:'结束会话',
    start:'开始',pause:'暂停',again:'再来一次',done:'完成',session_done:'会话完成',
    focus:'专注',rest:'休息',long_rest:'长休息',
    modes:'模式',modes_sub:'找到你的节奏。',custom_mode:'自定义模式',
    work:'工作',short_rest:'短休息',long_rest_label:'长休息',cycles:'循环',min:'分钟',auto_switch:'自动切换',
    cycle_1:'个循环',cycle_2:'个循环',cycle_5:'个循环',
    tasks:'任务',tasks_empty:'暂时为空。任务管理即将上线。',
    rest_title:'休息',rest_sub:'休息是工作的一部分。',
    relaxation:'放松',idea1:'闭眼平躺 2 分钟',idea2:'放松下巴和肩膀',idea3:'不听手机，静一静',
    music_sounds:'音乐与声音',silence:'安静',white_noise:'白噪音',brown_noise:'棕噪音',rain:'雨声',ocean:'海浪',ambient:'氛围',
    breathing:'呼吸',breath_idea1:'4-7-8：吸 4，屏 7，呼 8',breath_idea2:'方形：4-4-4-4',
    stats:'统计',stats_sub:'只是事实。',today_min:'今天，分钟',week_min:'7 天，分钟',total_sessions:'总会话数',
    last_7_days:'最近 7 天',history:'历史',empty:'暂时为空。',
    user:'用户',edit_name:'修改名字',language:'语言',
    theme:'主题',theme_auto:'自动',theme_light:'浅色',theme_dark:'深色',
    colors:'颜色',theme_cosmos:'宇宙',theme_ocean:'海洋',theme_forest:'森林',theme_mountains:'山脉',theme_rain:'雨天',theme_city:'夜城',
    behavior:'行为',beep:'提示音',vibration:'振动',notifications:'通知',
    notifications_unsupported:'通知（不支持）',notifications_denied:'通知（已被禁止）',
    data:'数据',download_copy:'下载副本',restore:'恢复',delete_history:'删除全部历史',
    delete_confirm:'再按一次确认',
    foot1:'数据只保存在本设备上。没有惩罚，也没有连续天数。',
    close_eyes:'闭上眼睛',nothing_do:'什么都别做。只是呼吸。',
    continue:'继续',skip:'跳过',can_open:'可以睁开眼睛了',slowly_open:'慢慢睁开眼，回到事情上。',
    what_name:'怎么称呼你？',nick_hint:'名字只有你在这台设备上能看到。',cancel:'取消',save:'保存',
    work_done_title:'工作结束',work_done_body:'该休息了。',
    session_end_title:'会话完成',session_end_body:'做得好。休息一下。',
    all_cycles:'所有循环已完成。好好休息。',
    rest_done_title:'休息结束',rest_done_body:'该回去工作了。',
    rec_none:'从轻松开始——只需 2 分钟。',
    rec_broken:'最近一半以上的会话被打断。试试更短的模式。',
    rec_today_long:'今天已经工作了很多。可以长休息一下。',
    rec_ready_deep:'你很少中断。可以试试 Deep Focus。',
    rec_ok:'你找到了自己的节奏。别忘了休息。',
    easy_start_session:'轻松开始',
    onb1_t:'欢迎来到 FLOW',onb1_b:'按自己的节奏工作和休息。没有惩罚，也没有连续天数。',
    onb2_t:'工作后——停一下',onb2_b:'当工作计时结束——闭眼 30 秒。5 秒后可以跳过。',
    onb3_t:'休息自动开始',onb3_b:'停顿之后，休息计时自动开始。',
    onb4_t:'我的与语言',onb4_b:'在我的里：名字、主题、语言、行为和数据。',
    next:'下一步',onb_start:'开始',onb_skip:'跳过',
    sleep_hint:'点击屏幕退出',rest_idea_prefix:'休息灵感：',
    reset:'重置',skip_label:'跳过阶段',
    mute_on:'开启声音',mute_off:'静音',
    hour_short:'时',part:'(部分)',
    mode_work:'工作',mode_rest:'休息'},
  ja:{nav_home:'ホーム',nav_tasks:'タスク',nav_rest:'休憩',nav_stats:'統計',nav_profile:'プロフィール',
    easy_start:'かんたんスタート：2 分だけ',end_session:'セッション終了',
    start:'スタート',pause:'一時停止',again:'もう一度',done:'完了',session_done:'セッション完了',
    focus:'集中',rest:'休憩',long_rest:'長い休憩',
    modes:'モード',modes_sub:'自分のリズムを見つけよう。',custom_mode:'カスタムモード',
    work:'作業',short_rest:'短い休憩',long_rest_label:'長い休憩',cycles:'サイクル',min:'分',auto_switch:'自動切り替え',
    cycle_1:'サイクル',cycle_2:'サイクル',cycle_5:'サイクル',
    tasks:'タスク',tasks_empty:'まだ空です。タスク管理は近日公開。',
    rest_title:'休憩',rest_sub:'休憩も仕事のうち。',
    relaxation:'リラックス',idea1:'目を閉じて2分横になる',idea2:'あごと肩の力を抜く',idea3:'スマホを置いて静けさを聴く',
    music_sounds:'音楽と環境音',silence:'無音',white_noise:'ホワイトノイズ',brown_noise:'ブラウンノイズ',rain:'雨',ocean:'海',ambient:'アンビエント',
    breathing:'呼吸',breath_idea1:'4-7-8：吸う4・止める7・吐く8',breath_idea2:'ボックス：4-4-4-4',
    stats:'統計',stats_sub:'事実だけ。',today_min:'今日、分',week_min:'7日、分',total_sessions:'総セッション数',
    last_7_days:'過去7日',history:'履歴',empty:'まだ空です。',
    user:'ユーザー',edit_name:'名前を変更',language:'言語',
    theme:'テーマ',theme_auto:'自動',theme_light:'ライト',theme_dark:'ダーク',
    colors:'カラー',theme_cosmos:'コスモス',theme_ocean:'オーシャン',theme_forest:'フォレスト',theme_mountains:'マウンテン',theme_rain:'レイン',theme_city:'ナイトシティ',
    behavior:'動作',beep:'通知音',vibration:'振動',notifications:'通知',
    notifications_unsupported:'通知（非対応）',notifications_denied:'通知（ブロック中）',
    data:'データ',download_copy:'コピーをダウンロード',restore:'復元',delete_history:'履歴をすべて削除',
    delete_confirm:'もう一度タップして確認',
    foot1:'データはこの端末にのみ保存されます。罰則も連続記録もありません。',
    close_eyes:'目を閉じて',nothing_do:'何もしないで。ただ呼吸を。',
    continue:'続ける',skip:'スキップ',can_open:'目を開けていいです',slowly_open:'ゆっくり目を開けて戻りましょう。',
    what_name:'何と呼べばいい？',nick_hint:'名前はこの端末のあなたにだけ表示されます。',cancel:'キャンセル',save:'保存',
    work_done_title:'作業完了',work_done_body:'休憩しましょう。',
    session_end_title:'セッション完了',session_end_body:'お疲れさま。休んで。',
    all_cycles:'すべてのサイクル完了。ゆっくり休んでください。',
    rest_done_title:'休憩終了',rest_done_body:'仕事に戻りましょう。',
    rec_none:'かんたんスタートから——2 分だけ。',
    rec_broken:'最近のセッションの半分以上が中断されています。短いモードを試してみて。',
    rec_today_long:'今日はもうたくさん作業しました。長い休憩のいいタイミングです。',
    rec_ready_deep:'中断が少ないですね。Deep Focus を試してみて。',
    rec_ok:'自分のリズムにいます。休憩も忘れずに。',
    easy_start_session:'かんたんスタート',
    onb1_t:'FLOW へようこそ',onb1_b:'自分のリズムで働いて休む。罰則も連続記録もなし。',
    onb2_t:'作業のあと——停止',onb2_b:'作業タイマーが終わったら——目を閉じて 30 秒。5 秒後はスキップできます。',
    onb3_t:'休憩は自動でスタート',onb3_b:'停止のあと、休憩タイマーが自動で始まります。',
    onb4_t:'プロフィールと言語',onb4_b:'プロフィールに名前、テーマ、言語、動作、データ。',
    next:'次へ',onb_start:'はじめる',onb_skip:'スキップ',
    sleep_hint:'画面をタップして終了',rest_idea_prefix:'休憩のアイデア：',
    reset:'リセット',skip_label:'フェーズをスキップ',
    mute_on:'音をオン',mute_off:'ミュート',
    hour_short:'時間',part:'(一部)',
    mode_work:'作業',mode_rest:'休憩'}
};

function t(key,params){
  var lang=D.lang||'ru';
  var d=I18N[lang]||I18N.ru;
  var s=(d[key]!==undefined)?d[key]:(I18N.ru[key]!==undefined?I18N.ru[key]:key);
  if(params){
    Object.keys(params).forEach(function(k){
      s=s.replace(new RegExp('{'+k+'}','g'),params[k]);
    });
  }
  return s;
}
function cycleStr(n){
  var lang=D.lang||'ru';
  if(lang==='ru'){
    var n10=n%10,n100=n%100;
    if(n10===1&&n100!==11)return n+' '+t('cycle_1');
    if(n10>=2&&n10<=4&&(n100<10||n100>=20))return n+' '+t('cycle_2');
    return n+' '+t('cycle_5');
  }
  return n+' '+t('cycle_1');
}
function detectLang(){
  try{
    var raw=(navigator.language||navigator.userLanguage||'en').toLowerCase();
    var primary=raw.split('-')[0];
    if(LANGS.indexOf(primary)>=0)return primary;
    return 'en';
  }catch(e){return 'en';}
}
function applyLang(){
  document.querySelectorAll('[data-i18n]').forEach(function(node){
    node.textContent=t(node.getAttribute('data-i18n'));
  });
  document.querySelectorAll('[data-i18n-aria]').forEach(function(node){
    node.setAttribute('aria-label',t(node.getAttribute('data-i18n-aria')));
  });
  document.documentElement.lang=D.lang||'ru';
  updateMuteBtn();
  updateTimerUI();
  renderModes();
  renderProfile();
  renderStats();
}

/* ============ ДАННЫЕ ============ */
var MODES={
  micro:{n:'mode_micro',w:5,r:5,l:15,c:4},
  adhd:{n:'mode_adhd',w:10,r:5,l:15,c:4},
  balanced:{n:'mode_balanced',w:25,r:5,l:15,c:4},
  recovery:{n:'mode_recovery',w:15,r:15,l:15,c:2},
  deep:{n:'mode_deep',w:50,r:10,l:20,c:2},
  extended:{n:'mode_extended',w:80,r:20,l:20,c:1}
};
var MODE_ORDER=['micro','adhd','balanced','recovery','deep','extended'];
var THEMES={
  cosmos:{n:'theme_cosmos',c1:'#8b5cf6',c2:'#38bdf8'},
  ocean:{n:'theme_ocean',c1:'#0ea5e9',c2:'#14b8a6'},
  forest:{n:'theme_forest',c1:'#22c55e',c2:'#a3e635'},
  mountains:{n:'theme_mountains',c1:'#64748b',c2:'#f59e0b'},
  rain:{n:'theme_rain',c1:'#60a5fa',c2:'#94a3b8'},
  city:{n:'theme_city',c1:'#f43f5e',c2:'#a855f7'}
};

function el(id){return document.getElementById(id);}
function esc(s){return String(s==null?'':s).replace(/[&<>"']/g,function(c){return {'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c];});}
function pad2(n){return (n<10?'0':'')+n;}
function fmtTime(sec){sec=Math.max(0,Math.round(sec));return pad2(Math.floor(sec/60))+':'+pad2(sec%60);}
function blurActive(){try{if(document.activeElement&&document.activeElement.blur)document.activeElement.blur();}catch(e){}}
function currentView(){
  var v=document.querySelector('.view.active');
  return v?v.id.replace(/^v-/,''):'home';
}

function defaultD(){
  return {cfg:{mode:'balanced',w:25,r:5,l:15,c:4,auto:true},sess:[],task:'',steps:[],park:[],
    th:'auto',tm:'cosmos',vol:0.5,beep:true,vib:true,notif:false,mute:false,
    onboarded:false,nick:'',lang:detectLang()};
}
function defaultT(){
  return {ph:'work',i:1,left:25*60,run:false,end:0,easy:false,cd:0,cdSkip:0,started:false,sessStart:0,warned30:false,warned10:false};
}
var D=defaultD(),T=defaultT();
var pauseReady=false,currentSound='none',ambient=null,ambientMaster=null;
var guide=null,sleepMode=null,sleepGuard=0,lastPhaseKey='';
var bc=null;try{bc=new BroadcastChannel(BCAST);}catch(e){}

function load(){
  try{
    var raw=localStorage.getItem(LS_KEY);if(!raw)return;
    var o=JSON.parse(raw);if(!o||typeof o!=='object')return;
    var baseD=defaultD();
    if(o.D&&typeof o.D==='object'){
      var dd=Object.assign(baseD,o.D);
      dd.cfg=Object.assign(defaultD().cfg,o.D.cfg||{});
      if(!Array.isArray(dd.sess))dd.sess=[];
      if(!Array.isArray(dd.steps))dd.steps=[];
      if(!Array.isArray(dd.park))dd.park=[];
      if(LANGS.indexOf(dd.lang)<0)dd.lang=detectLang();
      if(typeof dd.nick!=='string')dd.nick='';
      D=dd;
    }
    if(o.T&&typeof o.T==='object')T=Object.assign(defaultT(),o.T);
  }catch(e){}
}
function save(){
  try{
    localStorage.setItem(LS_KEY,JSON.stringify({D:D,T:T}));
    if(bc)try{bc.postMessage({type:'sync'});}catch(e){}
  }catch(e){
    try{D.sess=D.sess.slice(-200);D.park=D.park.slice(-100);localStorage.setItem(LS_KEY,JSON.stringify({D:D,T:T}));}catch(e2){}
  }
}

function isDarkNow(){if(D.th==='dark')return true;if(D.th==='light')return false;try{return window.matchMedia('(prefers-color-scheme: dark)').matches;}catch(e){return true;}}
function applyTheme(){
  document.documentElement.dataset.theme=isDarkNow()?'dark':'light';
  var meta=document.querySelector('meta[name="theme-color"]');
  if(meta)meta.setAttribute('content',isDarkNow()?'#0a0b10':'#f3f5fa');
  applyAccent(true);
}
function applyAccent(force){
  var th=THEMES[D.tm]||THEMES.cosmos;
  var rest=(T.ph==='rest');
  var key=D.tm+'|'+rest;
  if(!force&&key===lastPhaseKey)return;
  lastPhaseKey=key;
  var root=document.documentElement.style;
  root.setProperty('--a1',rest?th.c2:th.c1);
  root.setProperty('--a2',rest?th.c1:th.c2);
}

var ac=null;
function actx(){try{if(!ac){var AC=window.AudioContext||window.webkitAudioContext;if(!AC)return null;ac=new AC();}if(ac.state==='suspended')ac.resume().catch(function(){});return ac;}catch(e){return null;}}
function beep(freq,dur,type){
  if(D.mute||!D.beep)return;
  var c=actx();if(!c)return;
  try{
    freq=freq||660;dur=dur||0.18;
    var o=c.createOscillator(),g=c.createGain();
    o.type=type||'sine';o.frequency.value=freq;
    var t0=c.currentTime;
    g.gain.setValueAtTime(0.0001,t0);
    g.gain.exponentialRampToValueAtTime(0.09,t0+0.02);
    g.gain.exponentialRampToValueAtTime(0.0001,t0+dur);
    o.connect(g);g.connect(c.destination);
    o.start(t0);o.stop(t0+dur+0.03);
  }catch(e){}
}
function vib(pattern){if(!D.vib)return;try{if(navigator.vibrate)navigator.vibrate(pattern||40);}catch(e){}}
function notify(title,body){
  if(!D.notif)return;
  try{
    if('Notification' in window&&Notification.permission==='granted'){
      var opts={body:body,silent:false,tag:'flow-'+Date.now(),requireInteraction:true,vibrate:[200,100,200,100,200]};
      var n=new Notification(title,opts);
      n.onclick=function(){try{window.focus();}catch(e){}try{n.close();}catch(e){}};
    }
  }catch(e){}
}
function requestNotifPermission(){
  try{
    if(!('Notification' in window))return Promise.resolve('unsupported');
    if(Notification.permission==='granted')return Promise.resolve('granted');
    if(Notification.permission==='denied')return Promise.resolve('denied');
    return Notification.requestPermission();
  }catch(e){return Promise.resolve('error');}
}
function noiseBuffer(ctx,kind){
  var len=Math.floor(ctx.sampleRate*2);
  var buf=ctx.createBuffer(1,len,ctx.sampleRate);
  var d=buf.getChannelData(0);var last=0;
  for(var i=0;i<len;i++){var w=Math.random()*2-1;if(kind==='brown'){last=(last+0.02*w)/1.02;d[i]=last*3.5;}else{d[i]=w;}}
  return buf;
}
function stopAmbient(){
  if(ambientMaster&&ac){try{var now=ac.currentTime;ambientMaster.gain.cancelScheduledValues(now);ambientMaster.gain.setValueAtTime(ambientMaster.gain.value,now);ambientMaster.gain.linearRampToValueAtTime(0.0001,now+0.3);}catch(e){}}
  var nodes=ambient;ambient=null;ambientMaster=null;
  if(nodes){setTimeout(function(){nodes.forEach(function(n){try{n.stop();}catch(e){}});},350);}
}
function setAmbientVolume(){if(ambientMaster){try{ambientMaster.gain.value=D.mute?0:Math.max(0,Math.min(1,D.vol))*0.3;}catch(e){}}}
function playSound(kind){
  stopAmbient();currentSound=kind;
  if(kind==='none'){markSoundButtons();return;}
  var c=actx();if(!c){markSoundButtons();return;}
  try{
    var master=c.createGain();master.gain.value=0.0001;
    var target=D.mute?0:Math.max(0,Math.min(1,D.vol))*0.3;
    master.gain.exponentialRampToValueAtTime(Math.max(target,0.0001),c.currentTime+0.4);
    master.connect(c.destination);ambientMaster=master;
    var nodes=[];
    if(kind==='white'||kind==='rain'){
      var src=c.createBufferSource();src.buffer=noiseBuffer(c,'white');src.loop=true;
      var f=c.createBiquadFilter();
      if(kind==='white'){f.type='lowpass';f.frequency.value=6000;}else{f.type='highpass';f.frequency.value=900;}
      src.connect(f);f.connect(master);src.start();nodes.push(src);
    }else if(kind==='brown'||kind==='ocean'){
      var src2=c.createBufferSource();src2.buffer=noiseBuffer(c,'brown');src2.loop=true;
      var f2=c.createBiquadFilter();f2.type='lowpass';f2.frequency.value=2500;
      src2.connect(f2);
      if(kind==='ocean'){
        var vg=c.createGain();vg.gain.value=0.55;
        var lfo=c.createOscillator();lfo.frequency.value=0.1;
        var lg=c.createGain();lg.gain.value=0.42;
        lfo.connect(lg);lg.connect(vg.gain);
        f2.connect(vg);vg.connect(master);lfo.start();nodes.push(lfo);
      }else{f2.connect(master);}
      src2.start();nodes.push(src2);
    }else if(kind==='ambient'){
      [110,165,220,277.2].forEach(function(fr,idx){
        var o=c.createOscillator();o.type='sine';o.frequency.value=fr;
        var g=c.createGain();g.gain.value=0.055;
        var lfo2=c.createOscillator();lfo2.frequency.value=0.05+idx*0.033;
        var lg2=c.createGain();lg2.gain.value=0.045;
        lfo2.connect(lg2);lg2.connect(g.gain);
        o.connect(g);g.connect(master);o.start();lfo2.start();
        nodes.push(o);nodes.push(lfo2);
      });
    }
    ambient=nodes;
  }catch(e){ambient=null;ambientMaster=null;}
  markSoundButtons();
}
function markSoundButtons(){document.querySelectorAll('.snd').forEach(function(b){b.classList.toggle('active',b.dataset.s===currentSound);});}

var wakeLock=null;
function requestWake(){try{if(!('wakeLock' in navigator)||wakeLock)return;navigator.wakeLock.request('screen').then(function(w){wakeLock=w;w.addEventListener('release',function(){wakeLock=null;});}).catch(function(){});}catch(e){}}
function releaseWake(){try{if(wakeLock){wakeLock.release();wakeLock=null;}}catch(e){}}

function getLeft(){if(T.run&&T.end)return Math.max(0,Math.ceil((T.end-Date.now())/1000));return Math.max(0,T.left||0);}
function isLongRest(i){return (i>=D.cfg.c)||(i%4===0);}
function phaseTotal(){
  if(T.ph==='done')return 1;
  if(T.ph==='work')return T.easy?120:D.cfg.w*60;
  return (isLongRest(T.i)?D.cfg.l:D.cfg.r)*60;
}
function modeLabel(){return D.cfg.mode==='custom'?t('custom_mode'):(MODES[D.cfg.mode]?t(MODES[D.cfg.mode].n):t('custom_mode'));}

function logSession(sec,ok,name){
  if(sec<30)return;
  var m=Math.max(1,Math.round(sec/60));
  D.sess.push({t:Date.now(),m:m,md:name,ok:!!ok});
  if(D.sess.length>500)D.sess=D.sess.slice(-500);
  save();
}

function startTimer(){
  if(T.ph==='done'||T.cd>0)return;
  if(getLeft()<=0)return;
  if(!T.sessStart)T.sessStart=Date.now();
  T.run=true;T.end=Date.now()+getLeft()*1000;T.started=true;
  T.warned30=false;T.warned10=false;
  requestWake();
  vib(T.ph==='work'?[20,60,20]:[80]);
  save();updateTimerUI();updateNavVisibility();
}
function pauseTimer(){
  T.left=getLeft();T.run=false;T.end=0;
  releaseWake();save();updateTimerUI();updateNavVisibility();
}

function resetSession(force){
  if(T.cd>0&&!force)return;
  var worked=T.ph==='work'&&!T.easy?(phaseTotal()-getLeft()):0;
  if(T.ph==='work'&&!T.cd&&worked>=30){logSession(worked,false,T.easy?t('easy_start_session'):modeLabel());}
  releaseWake();
  T=defaultT();T.left=D.cfg.w*60;
  pauseReady=false;el('ovPause').hidden=true;
  save();updateTimerUI();updateNavVisibility();
}

function goRest(){
  var lng=isLongRest(T.i);
  T.ph='rest';T.left=(lng?D.cfg.l:D.cfg.r)*60;
  T.run=false;T.end=0;T.easy=false;T.warned30=false;T.warned10=false;
  pickRestIdea();
}
function goWork(){
  T.ph='work';T.left=D.cfg.w*60;T.run=false;T.end=0;
  T.warned30=false;T.warned10=false;
}

function showPause(){
  pauseReady=false;
  var ov=el('ovPause');ov.hidden=false;
  el('pauseTitle').textContent=t('close_eyes');
  el('pauseSub').textContent=t('nothing_do');
  el('pauseCount').hidden=false;
  el('pauseCount').textContent='0:30';
  el('pauseGo').hidden=true;
  el('pauseSkip').hidden=true;
  el('pauseGo').textContent=t('continue');
  el('pauseSkip').textContent=t('skip');
}
function startPause(){
  T.cd=Date.now()+30000;
  T.cdSkip=Date.now()+5000;
  T.run=false;T.end=0;
  releaseWake();showPause();save();updateTimerUI();updateNavVisibility();
}
function resumePause(){
  T.cd=0;T.cdSkip=0;pauseReady=false;
  el('ovPause').hidden=true;
  el('pauseSkip').hidden=true;
  el('pauseGo').hidden=true;
  if(T.ph!=='done'){startTimer();}
  else{save();updateTimerUI();}
}
function skipPause(){
  if(T.cd>0&&T.cdSkip&&Date.now()>=T.cdSkip){resumePause();}
}

function endWork(kind){
  var total=phaseTotal();
  var left=getLeft();
  var worked=Math.max(0,Math.round(total-left));

  if(T.easy){
    if(worked>=30)logSession(worked,true,t('easy_start_session'));
    T.easy=false;T.run=false;T.end=0;T.started=false;
    if(kind==='end'){
      T.ph='done';T.left=0;T.cd=0;
      save();updateTimerUI();updateNavVisibility();
      notify(t('session_end_title'),t('session_end_body'));
      return;
    }
    goRest();startPause();
    save();updateTimerUI();updateNavVisibility();
    notify(t('work_done_title'),t('work_done_body'));
    return;
  }

  if(worked>=30)logSession(worked,kind!=='skip',modeLabel());

  if(kind==='end'){
    T.ph='done';T.run=false;T.end=0;T.left=0;T.started=false;
    T.cd=0;T.cdSkip=0;
    save();updateTimerUI();updateNavVisibility();
    notify(t('session_end_title'),t('session_end_body'));
    return;
  }

  if(kind==='skip'){
    goRest();startTimer();
    save();updateTimerUI();updateNavVisibility();
    return;
  }

  goRest();startPause();
  save();updateTimerUI();updateNavVisibility();
  notify(t('work_done_title'),t('work_done_body'));
}

function endRest(forceStart){
  if(T.i>=D.cfg.c){
    T.ph='done';T.run=false;T.end=0;T.left=0;T.started=false;
    save();updateTimerUI();updateNavVisibility();
    notify(t('session_end_title'),t('all_cycles'));
    return;
  }
  T.i++;goWork();
  notify(t('rest_done_title'),t('rest_done_body'));
  if(D.cfg.auto||forceStart)startTimer();
  else{save();updateTimerUI();updateNavVisibility();}
}

function tick(){
  var now=Date.now();

  if(T.cd>0){
    var rem=Math.ceil((T.cd-now)/1000);
    if(rem>0){
      var pc=el('pauseCount');
      var txt='0:'+pad2(Math.min(59,rem));
      if(pc.textContent!==txt)pc.textContent=txt;
      var canSkip=!!(T.cdSkip&&now>=T.cdSkip);
      var sb=el('pauseSkip');
      if(sb.hidden===canSkip)sb.hidden=!canSkip;
    }else if(!pauseReady){
      pauseReady=true;
      el('pauseCount').hidden=true;
      el('pauseGo').hidden=false;
      el('pauseSkip').hidden=true;
      el('pauseTitle').textContent=t('can_open');
      el('pauseSub').textContent=t('slowly_open');
      el('pauseGo').textContent=t('continue');
      beep(560,0.3);vib([40,80,40]);
    }
  }

  if(T.run&&T.end){
    var r=Math.max(0,Math.ceil((T.end-now)/1000));
    T.left=r;
    if(!T.warned30&&r<=30&&r>10&&T.ph==='work'){T.warned30=true;if(!D.mute&&D.beep)beep(440,0.1);}
    if(!T.warned10&&r<=10&&r>0){T.warned10=true;if(!D.mute&&D.beep)beep(520,0.12);vib([10,200,10,200,10]);}
    if(r<=0){
      T.run=false;T.end=0;T.left=0;
      beep(700,0.35);
      vib([80,60,80,60,80]);
      updateTimerUI();
      if(T.ph==='work')endWork('timer');
      else if(T.ph==='rest')endRest(false);
      return;
    }
  }

  updateTimerUI();
  updateNavVisibility();
  if(guide)guideTick(now);
  if(sleepMode)updateSleepClock();
}

var navRevealUntil=0,navHideTimer=null;
function shouldHideNav(){
  if(T.cd>0)return false;
  if(!T.run)return false;
  if(T.ph==='done')return false;
  return currentView()==='home';
}
function updateNavVisibility(){
  var nav=document.querySelector('.nav');if(!nav)return;
  var revealed=Date.now()<navRevealUntil;
  var hide=shouldHideNav()&&!revealed;
  nav.classList.toggle('hide',hide);
}
function revealNav(duration){
  navRevealUntil=Date.now()+(duration||5000);
  updateNavVisibility();
  clearTimeout(navHideTimer);
  navHideTimer=setTimeout(updateNavVisibility,duration||5000);
}

var RING_C=2*Math.PI*118;
function updateTimerUI(){
  applyAccent(false);
  var left=getLeft();
  var total=phaseTotal();
  var frac=total>0?Math.max(0,Math.min(1,left/total)):0;

  var ring=el('ring');
  ring.style.strokeDasharray=RING_C;
  ring.style.strokeDashoffset=RING_C*(1-frac);
  ring.classList.toggle('warn',T.run&&left<=10&&left>0);

  var timeEl=el('timeText');
  var timeStr=(T.ph==='done')?t('done'):fmtTime(left);
  if(timeEl.textContent!==timeStr)timeEl.textContent=timeStr;

  var sub;
  if(T.ph==='done'){sub=t('session_done');}
  else if(T.ph==='work'){
    var nm=D.task&&D.task.trim()?D.task.trim():t('focus');
    sub=nm.length>20?nm.slice(0,19)+'…':nm;
  }else{
    sub=(isLongRest(T.i)?t('long_rest'):t('rest'))+' · '+T.i+'/'+D.cfg.c;
  }
  var subEl=el('subText');
  if(subEl.textContent!==sub)subEl.textContent=sub;
  if(T.ph==='rest'&&T.cd===0){subEl.style.color='var(--a1)';subEl.style.fontWeight='800';}
  else{subEl.style.color='';subEl.style.fontWeight='';}

  var badge=el('restBadge');
  var showBadge=T.ph==='rest'&&T.cd===0;
  badge.hidden=!showBadge;
  if(showBadge){el('restBadgeText').textContent=isLongRest(T.i)?t('long_rest'):t('rest');}

  el('breathe').style.setProperty('--br',(T.ph==='rest'?10:6)+'s');

  var bs=el('btnStart');
  var wantState=(T.ph==='done')?'again':(T.run?'pause':'start');
  var stateKey=wantState+'|'+(D.lang||'ru');
  if(bs.dataset.state!==stateKey){
    bs.dataset.state=stateKey;
    var label=t(wantState==='again'?'again':(wantState==='pause'?'pause':'start'));
    var icon=wantState==='pause'
      ?'<svg viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><rect x="7" y="5" width="4" height="14" rx="1"/><rect x="13" y="5" width="4" height="14" rx="1"/></svg>'
      :(wantState==='again'
        ?'<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M3.5 12a8.5 8.5 0 1 0 2.6-6.1"/><path d="M3.5 4.5v5h5"/></svg>'
        :'<svg viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M8 5.5 18 12 8 18.5z"/></svg>');
    bs.innerHTML=icon+'<span>'+label+'</span>';
  }

  el('btnEasy').hidden=!(T.ph==='work'&&!T.started&&!T.run&&!T.easy);
  el('btnEndSess').hidden=!(T.started&&T.ph!=='done'&&T.cd===0);

  el('restIdea').classList.toggle('on',T.ph==='rest'&&T.cd===0);
  updateMuteBtn();
  updateMiniTimer();
}

var restIdeaIndex=0;
var IDEA_KEYS=['idea1','idea2','idea3','idea1','idea2','idea3','idea1','idea2','idea3','idea1'];
function pickRestIdea(){
  restIdeaIndex=Math.floor(Math.random()*IDEA_KEYS.length);
  el('restIdea').innerHTML='<b>'+esc(t('rest_idea_prefix'))+'</b> '+esc(t(IDEA_KEYS[restIdeaIndex]));
}

function updateMuteBtn(){
  var b=el('btnMute');
  b.classList.toggle('on',!!D.mute);
  b.innerHTML=D.mute
    ?'<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M4 9v6h4l5 4V5L8 9H4z"/><path d="m16.5 9 5 6M21.5 9l-5 6"/></svg>'
    :'<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M4 9v6h4l5 4V5L8 9H4z"/><path d="M16.5 8.5a5 5 0 0 1 0 7"/><path d="M19 6a8.5 8.5 0 0 1 0 12"/></svg>';
  b.setAttribute('aria-label',D.mute?t('mute_on'):t('mute_off'));
  b.setAttribute('aria-pressed',D.mute?'true':'false');
}

function updateMiniTimer(){
  var mt=el('miniTimer');
  var activeTab=currentView();
  var shouldShow=activeTab!=='home'&&(T.run||(T.ph==='rest'&&T.cd===0)||(T.started&&T.ph!=='done'&&T.cd===0));
  mt.hidden=!shouldShow;
  if(!shouldShow)return;
  var left=getLeft();
  el('mtTime').textContent=fmtTime(left);
  el('mtDot').classList.toggle('paused',!T.run||T.cd>0);
  var phase=T.ph==='rest'?t('rest'):(T.easy?t('easy_start_session'):t('focus'));
  el('mtPhase').textContent=phase+' · '+T.i+'/'+D.cfg.c;
  var btn=el('mtBtn');
  btn.innerHTML=T.run
    ?'<svg viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><rect x="7" y="5" width="4" height="14" rx="1"/><rect x="13" y="5" width="4" height="14" rx="1"/></svg>'
    :'<svg viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M8 5.5 18 12 8 18.5z"/></svg>';
  btn.setAttribute('aria-label',T.run?t('pause'):t('continue'));
}

function renderModes(){
  var wrap=el('modeList');
  wrap.innerHTML=MODE_ORDER.map(function(k){
    var m=MODES[k];
    var act=D.cfg.mode===k?' active':'';
    return '<button class="modecard'+act+'" data-m="'+k+'">'
      +'<div class="mname">'+esc(t(m.n))+'</div>'
      +'<div class="mvals">'+m.w+' '+t('min')+' '+t('mode_work')+' · '+m.r+'/'+m.l+' '+t('mode_rest')+' · '+cycleStr(m.c)+'</div></button>';
  }).join('');
  syncCustom();
}
function syncCustom(){
  el('sw').value=D.cfg.w;el('sr').value=D.cfg.r;el('sl').value=D.cfg.l;el('sc').value=D.cfg.c;
  el('lw').textContent=D.cfg.w;el('lr').textContent=D.cfg.r;el('ll').textContent=D.cfg.l;el('lc').textContent=D.cfg.c;
  el('tgAuto').checked=!!D.cfg.auto;
  renderSummary();
}
function calcRestTotal(c,r,l){
  var total=0;
  for(var i=1;i<=c;i++){total+=((i>=c)||(i%4===0))?l:r;}
  return total;
}
function renderSummary(){
  var w=D.cfg.w,r=D.cfg.r,l=D.cfg.l,c=D.cfg.c;
  var workMin=w*c;var restMin=calcRestTotal(c,r,l);var totalMin=workMin+restMin;
  var h=Math.floor(totalMin/60),m=totalMin%60;
  var totalStr=(h?h+' '+t('hour_short')+' ':'')+m+' '+t('min');
  el('customSummary').innerHTML=t('total')+': <b>'+totalStr+'</b><br>'+t('work')+': <b>'+workMin+' '+t('min')+'</b> · '+t('rest')+': <b>'+restMin+' '+t('min')+'</b>';
}
function applyMode(k){
  var m=MODES[k];if(!m)return;
  if(T.started){resetSession(true);}
  D.cfg.mode=k;D.cfg.w=m.w;D.cfg.r=m.r;D.cfg.l=m.l;D.cfg.c=m.c;
  releaseWake();
  T=defaultT();T.left=D.cfg.w*60;T.cd=0;
  pauseReady=false;el('ovPause').hidden=true;
  save();renderModes();updateTimerUI();updateNavVisibility();
  switchTab('home');
}

function sumMins(arr){return arr.reduce(function(a,s){return a+(s.m||0);},0);}
function startOfToday(){var d=new Date();d.setHours(0,0,0,0);return d.getTime();}
function buildRecommendation(){
  var s=D.sess;
  if(!s.length)return t('rec_none');
  var t0=startOfToday();
  var todayMin=sumMins(s.filter(function(x){return x.t>=t0;}));
  var last10=s.slice(-10);var broken=last10.filter(function(x){return !x.ok;}).length;
  if(broken>last10.length/2)return t('rec_broken');
  if(todayMin>=150)return t('rec_today_long');
  var avg=last10.reduce(function(a,x){return a+x.m;},0)/last10.length;
  if(broken/last10.length<0.2&&avg<50)return t('rec_ready_deep');
  return t('rec_ok');
}
function renderStats(){
  var t0=startOfToday();
  el('statToday').textContent=sumMins(D.sess.filter(function(s){return s.t>=t0;}));
  el('statWeek').textContent=sumMins(D.sess.filter(function(s){return s.t>=t0-6*86400000;}));
  el('statTotal').textContent=D.sess.length;
  el('statRec').textContent=buildRecommendation();
  renderBars();renderHistory();
}
function renderBars(){
  var days=[];
  var base=new Date();base.setHours(0,0,0,0);
  for(var d=6;d>=0;d--){
    var st=base.getTime()-d*86400000,en=st+86400000;
    var mins=sumMins(D.sess.filter(function(s){return s.t>=st&&s.t<en;}));
    days.push({date:new Date(st),m:mins});
  }
  var max=Math.max(1,Math.max.apply(null,days.map(function(x){return x.m;})));
  var lang=D.lang||'ru';
  var names={'ru':['Вс','Пн','Вт','Ср','Чт','Пт','Сб'],'en':['Su','Mo','Tu','We','Th','Fr','Sa'],'es':['Do','Lu','Ma','Mi','Ju','Vi','Sá'],'zh':['日','一','二','三','四','五','六'],'ja':['日','月','火','水','木','金','土']}[lang]||['Su','Mo','Tu','We','Th','Fr','Sa'];
  el('bars').innerHTML=days.map(function(d){
    var h=d.m?Math.max(6,Math.round(d.m/max*100)):0;
    return '<div class="bar"><div class="btrack"><i style="height:'+h+'%"></i></div><span>'+names[d.date.getDay()]+'</span></div>';
  }).join('');
}
function renderHistory(){
  var list=D.sess.slice(-12).reverse();
  var wrap=el('history');
  if(!list.length){wrap.innerHTML='<p class="p" style="margin:0">'+esc(t('empty'))+'</p>';return;}
  wrap.innerHTML=list.map(function(s){
    var d=new Date(s.t);
    var ds=pad2(d.getDate())+'.'+pad2(d.getMonth()+1);
    var ts=pad2(d.getHours())+':'+pad2(d.getMinutes());
    return '<div class="hrow"><span class="hdate">'+ds+' '+ts+'</span><span class="hmode">'+esc(s.md)+'</span><span class="hmin">'+s.m+' '+t('min')+(s.ok?'':' <em>'+t('part')+'</em>')+'</span></div>';
  }).join('');
}

function renderProfile(){
  var nick=(D.nick&&D.nick.trim())?D.nick.trim():t('user');
  el('nickEl').textContent=nick;
  el('avatarEl').textContent=(nick.charAt(0)||'U').toUpperCase();

  el('langList').innerHTML=LANGS.map(function(l){
    var act=D.lang===l?' active':'';
    return '<button class="lang-btn'+act+'" data-lang="'+l+'">'
      +'<span class="flag">'+LANG_FLAGS[l]+'</span>'
      +'<span>'+esc(LANG_NAMES[l])+'</span></button>';
  }).join('');

  document.querySelectorAll('#segTheme button').forEach(function(b){b.classList.toggle('active',b.dataset.th===D.th);});
  el('themeList').innerHTML=Object.keys(THEMES).map(function(k){
    var th=THEMES[k];var act=D.tm===k?' active':'';
    return '<button class="theme'+act+'" data-tm="'+k+'"><i class="tswatch" style="background:linear-gradient(135deg,'+th.c1+','+th.c2+')"></i><span>'+esc(t(th.n))+'</span></button>';
  }).join('');
  el('tgBeep').checked=!!D.beep;
  el('tgVib').checked=!!D.vib;
  el('tgNotif').checked=!!D.notif;
  updateNotifRow();
}
function updateNotifRow(){
  var row=el('notifRow'),lbl=el('notifLbl'),inp=el('tgNotif');
  var supported=('Notification' in window);
  var denied=supported&&Notification.permission==='denied';
  if(!supported){row.classList.add('disabled');lbl.textContent=t('notifications_unsupported');inp.disabled=true;inp.checked=false;}
  else if(denied){row.classList.add('disabled');lbl.textContent=t('notifications_denied');inp.disabled=true;inp.checked=false;}
  else{row.classList.remove('disabled');lbl.textContent=t('notifications');inp.disabled=false;}
}

function startGuide(){
  guide={i:0,end:Date.now()+20000,done:false};
  el('ovGuide').hidden=false;
  el('guidePhase').textContent=t('rest');
  el('guideHint').textContent='';
  el('guideCount').textContent='20';
  beep(520,0.1);
}
function guideTick(now){
  if(!guide||guide.done)return;
  var rem=Math.max(0,Math.ceil((guide.end-now)/1000));
  el('guideCount').textContent=String(rem);
  if(rem<=0){guide.done=true;el('guidePhase').textContent=t('done');el('guideEnd').textContent=t('cancel');beep(660,0.3);}
}
function closeGuide(){guide=null;el('ovGuide').hidden=true;el('guideCount').textContent='';}

function updateSleepClock(){
  if(!sleepMode)return;
  var d=new Date();
  el('sleepClock').textContent=pad2(d.getHours())+':'+pad2(d.getMinutes());
  if(Date.now()>sleepMode.end){stopSleep();}
}
function startSleep(){
  sleepMode={end:Date.now()+30*60000};sleepGuard=Date.now()+900;
  el('ovSleep').hidden=false;playSound('brown');updateSleepClock();
}
function stopSleep(){sleepMode=null;el('ovSleep').hidden=true;stopAmbient();currentSound='none';markSoundButtons();}

function switchTab(name){
  blurActive();
  document.querySelectorAll('.view').forEach(function(v){v.classList.toggle('active',v.id==='v-'+name);});
  document.querySelectorAll('.navbtn').forEach(function(b){b.classList.toggle('active',b.dataset.tab===name);});
  try{sessionStorage.setItem(SS_TAB,name);}catch(e){}
  if(name==='stats')renderStats();
  if(name==='modes')renderModes();
  if(name==='profile')renderProfile();
  if(name==='home')navRevealUntil=0;
  window.scrollTo(0,0);
  updateMiniTimer();
  updateNavVisibility();
}

var onbStep=0;
var ONB_STEPS=[
  {t:'onb1_t',b:'onb1_b'},
  {t:'onb2_t',b:'onb2_b'},
  {t:'onb3_t',b:'onb3_b'},
  {t:'onb4_t',b:'onb4_b'}
];
function showOnboarding(){onbStep=0;renderOnb();el('onb').hidden=false;}
function renderOnb(){
  var s=ONB_STEPS[onbStep];
  el('onbTitle').textContent=t(s.t);
  el('onbText').textContent=t(s.b);
  document.querySelectorAll('#onbDots i').forEach(function(d,i){d.className=i===onbStep?'on':'';});
  el('onbNext').textContent=(onbStep===ONB_STEPS.length-1)?t('onb_start'):t('next');
  el('onbSkip').textContent=t('onb_skip');
}
function closeOnb(){el('onb').hidden=true;D.onboarded=true;save();try{localStorage.setItem(LS_ONB,'1');}catch(e){}}

function exportData(){
  try{
    var payload={D:D,T:T,exported:new Date().toISOString()};
    var blob=new Blob([JSON.stringify(payload,null,2)],{type:'application/json'});
    var url=URL.createObjectURL(blob);
    var a=document.createElement('a');
    a.href=url;a.download='flow-backup-'+new Date().toISOString().slice(0,10)+'.json';
    document.body.appendChild(a);a.click();a.remove();
    setTimeout(function(){URL.revokeObjectURL(url);},2000);
  }catch(e){}
}
function importData(file){
  var r=new FileReader();
  r.onload=function(){
    try{
      var o=JSON.parse(r.result);
      if(o.D&&typeof o.D==='object'){
        var base=defaultD();
        var dd=Object.assign(base,o.D);
        dd.cfg=Object.assign(defaultD().cfg,o.D.cfg||{});
        if(!Array.isArray(dd.sess))dd.sess=[];
        if(!Array.isArray(dd.steps))dd.steps=[];
        if(!Array.isArray(dd.park))dd.park=[];
        if(LANGS.indexOf(dd.lang)<0)dd.lang=detectLang();
        if(typeof dd.nick!=='string')dd.nick='';
        D=dd;
      }
      if(o.T&&typeof o.T==='object')T=Object.assign(defaultT(),o.T);
      D.onboarded=true;save();
      try{localStorage.setItem(LS_ONB,'1');}catch(e){}
      location.reload();
    }catch(err){}
  };
  r.readAsText(file);
}

var swipeStart=null;
var INTERACTIVE_SEL='input,textarea,[type=range],.sw,.snd,.sbtn,.modecard,.theme,.lang-btn,.navbtn,.mt-btn,.bigbtn,.ctl,.linkbtn,.cathead,.seg button,.rest-go,.rest-skip,.ghost,.sheet-panel,.section-btn,.profile-edit';

document.addEventListener('touchstart',function(e){
  var tt=e.touches[0];if(!tt)return;
  if(e.target.closest(INTERACTIVE_SEL)){swipeStart=null;return;}
  swipeStart={x:tt.clientX,y:tt.clientY,time:Date.now()};
},{passive:true});
document.addEventListener('touchend',function(e){
  if(!swipeStart)return;
  var tt=e.changedTouches[0];if(!tt){swipeStart=null;return;}
  var dx=tt.clientX-swipeStart.x,dy=tt.clientY-swipeStart.y,dt=Date.now()-swipeStart.time;
  swipeStart=null;
  if(dt>900)return;
  if(Math.abs(dy)<50)return;
  if(Math.abs(dy)<Math.abs(dx)*1.2)return;
  var nav=document.querySelector('.nav');
  if(nav&&nav.classList.contains('hide')){revealNav(5000);vib(15);}
},{passive:true});

function init(){
  load();applyLang();applyTheme();
  try{window.matchMedia('(prefers-color-scheme: dark)').addEventListener('change',function(){if(D.th==='auto')applyTheme();});}catch(e){}

  if(T.run&&T.end&&T.end<Date.now()-60000){
    T.run=false;T.end=0;T.left=0;
    setTimeout(function(){if(T.ph==='work')endWork('timer');else if(T.ph==='rest')endRest(false);},200);
  }

  if(T.cd>0){
    if(!T.cdSkip||T.cdSkip<Date.now()-120000)T.cdSkip=Date.now()+5000;
    showPause();
    if(Date.now()>=T.cd){
      pauseReady=true;
      el('pauseCount').hidden=true;
      el('pauseGo').hidden=false;
      el('pauseTitle').textContent=t('can_open');
      el('pauseSub').textContent=t('slowly_open');
    }else if(T.cdSkip&&Date.now()>=T.cdSkip){
      el('pauseSkip').hidden=false;
    }
  }
  if(T.ph==='rest')pickRestIdea();

  el('volRange').value=Math.round((D.vol||0)*100);
  updateTimerUI();markSoundButtons();

  try{var lastTab=sessionStorage.getItem(SS_TAB);if(lastTab&&el('v-'+lastTab))switchTab(lastTab);}catch(e){}

  document.querySelectorAll('.navbtn').forEach(function(b){b.addEventListener('click',function(){switchTab(b.dataset.tab);});});
  el('btnModes').addEventListener('click',function(){switchTab('modes');});

  el('timerwrap').addEventListener('click',function(){
    var nav=document.querySelector('.nav');
    if(nav&&nav.classList.contains('hide')){revealNav(5000);vib(15);}
  });

  el('miniTimer').addEventListener('click',function(e){
    if(e.target.closest('#mtBtn'))return;
    switchTab('home');
  });
  el('mtBtn').addEventListener('click',function(e){
    e.stopPropagation();
    if(T.cd>0)return;
    if(T.run)pauseTimer();else startTimer();
  });

  el('btnStart').addEventListener('click',function(){
    if(T.cd>0)return;
    if(T.ph==='done'){resetSession(true);return;}
    if(T.run)pauseTimer();else startTimer();
  });
  el('btnReset').addEventListener('click',function(){if(T.cd>0)return;resetSession(false);});
  el('btnSkip').addEventListener('click',function(){
    if(T.cd>0)return;
    if(T.ph==='work')endWork('skip');
    else if(T.ph==='rest')endRest(false);
  });
  el('btnEasy').addEventListener('click',function(){
    if(T.cd>0)return;
    if(D.notif===false && 'Notification' in window && Notification.permission==='default'){
      requestNotifPermission().then(function(p){
        if(p==='granted'){D.notif=true;save();updateNotifRow();}
      });
    }
    T.easy=true;T.ph='work';T.left=120;T.run=false;T.end=0;T.i=1;
    startTimer();
  });
  el('btnEndSess').addEventListener('click',function(){
    if(T.cd>0)return;
    if(T.ph==='work')endWork('end');
    else if(T.ph==='rest'){
      T.ph='done';T.run=false;T.end=0;T.left=0;T.started=false;
      save();updateTimerUI();updateNavVisibility();
      notify(t('session_end_title'),t('session_end_body'));
    }
  });
  el('btnMute').addEventListener('click',function(){D.mute=!D.mute;save();setAmbientVolume();updateMuteBtn();});

  el('modeList').addEventListener('click',function(e){
    var b=e.target.closest('.modecard');
    if(b)applyMode(b.dataset.m);
  });
  function onSlider(){
    D.cfg.mode='custom';
    D.cfg.w=parseInt(el('sw').value,10);
    D.cfg.r=parseInt(el('sr').value,10);
    D.cfg.l=parseInt(el('sl').value,10);
    D.cfg.c=parseInt(el('sc').value,10);
    el('lw').textContent=D.cfg.w;el('lr').textContent=D.cfg.r;
    el('ll').textContent=D.cfg.l;el('lc').textContent=D.cfg.c;
    renderSummary();save();
    if(!T.started&&T.ph==='work'&&T.cd===0&&!T.easy){
      T.left=D.cfg.w*60;T.i=1;T.run=false;T.end=0;
    }
    renderModes();updateTimerUI();
  }
  ['sw','sr','sl','sc'].forEach(function(id){el(id).addEventListener('input',onSlider);});
  el('tgAuto').addEventListener('change',function(){D.cfg.auto=el('tgAuto').checked;save();});

  document.querySelectorAll('.cathead').forEach(function(h){h.addEventListener('click',function(){h.parentElement.classList.toggle('open');});});
  el('sounds').addEventListener('click',function(e){
    var b=e.target.closest('.snd');if(b)playSound(b.dataset.s);
  });
  el('volRange').addEventListener('input',function(){
    D.vol=parseInt(el('volRange').value,10)/100;
    setAmbientVolume();save();
  });

  el('pauseGo').addEventListener('click',resumePause);
  el('pauseSkip').addEventListener('click',skipPause);
  el('guideEnd').addEventListener('click',function(){if(guide)closeGuide();});
  el('ovSleep').addEventListener('click',function(){if(Date.now()<sleepGuard)return;stopSleep();});

  document.querySelectorAll('.section-btn').forEach(function(btn){
    btn.addEventListener('click',function(){
      var target=el(btn.dataset.target);
      if(!target)return;
      var isOpen=!target.hidden;
      if(isOpen){target.hidden=true;btn.classList.remove('open');}
      else{target.hidden=false;btn.classList.add('open');}
    });
  });

  el('langList').addEventListener('click',function(e){
    var b=e.target.closest('.lang-btn');
    if(!b)return;
    var newLang=b.dataset.lang;
    if(newLang===D.lang)return;
    D.lang=newLang;save();
    applyLang();
    renderProfile();
    updateNotifRow();
  });

  function openNick(){
    el('nickInput').value=(D.nick&&D.nick.trim())?D.nick:'';
    el('nickSheet').hidden=false;
  }
  function closeNick(){blurActive();el('nickSheet').hidden=true;}
  el('btnEditNick').addEventListener('click',openNick);
  el('nickBg').addEventListener('click',closeNick);
  el('nickCancel').addEventListener('click',closeNick);
  el('nickSave').addEventListener('click',function(){
    var v=el('nickInput').value.trim();
    D.nick=v||'';
    save();renderProfile();closeNick();
  });
  el('nickInput').addEventListener('keydown',function(e){if(e.key==='Enter'){e.preventDefault();el('nickSave').click();}});

  el('segTheme').addEventListener('click',function(e){
    var b=e.target.closest('button');if(!b)return;
    D.th=b.dataset.th;save();applyTheme();renderProfile();
  });
  el('themeList').addEventListener('click',function(e){
    var b=e.target.closest('.theme');if(!b)return;
    D.tm=b.dataset.tm;save();lastPhaseKey='';applyAccent(true);renderProfile();
  });
  el('tgBeep').addEventListener('change',function(){D.beep=el('tgBeep').checked;save();if(D.beep)beep(620,0.14);});
  el('tgVib').addEventListener('change',function(){D.vib=el('tgVib').checked;save();if(D.vib)vib(40);});
  el('tgNotif').addEventListener('change',function(){
    var want=el('tgNotif').checked;
    if(want){
      requestNotifPermission().then(function(p){
        if(p==='granted'){D.notif=true;save();}
        else{D.notif=false;el('tgNotif').checked=false;save();}
        updateNotifRow();
      });
    }else{D.notif=false;save();}
    updateNotifRow();
  });

  el('btnExport').addEventListener('click',exportData);
  el('btnImport').addEventListener('click',function(){el('importFile').click();});
  el('importFile').addEventListener('change',function(e){
    var f=e.target.files&&e.target.files[0];
    if(f)importData(f);
    e.target.value='';
  });

  var delArm=0,delTimer=null;
  el('btnDel').addEventListener('click',function(){
    var btn=el('btnDel');
    if(delArm&&Date.now()<delArm){
      D.sess=[];save();renderStats();
      delArm=0;clearTimeout(delTimer);
      btn.textContent=t('delete_history');btn.classList.remove('armed');
      return;
    }
    delArm=Date.now()+4000;
    btn.textContent=t('delete_confirm');
    btn.classList.add('armed');
    clearTimeout(delTimer);
    delTimer=setTimeout(function(){delArm=0;btn.textContent=t('delete_history');btn.classList.remove('armed');},4000);
  });

  document.addEventListener('visibilitychange',function(){
    if(!document.hidden){tick();if(T.run)requestWake();}
    save();
  });
  window.addEventListener('pagehide',save);
  window.addEventListener('beforeunload',save);
  if(bc){
    bc.onmessage=function(e){
      if(e.data&&e.data.type==='sync'){
        load();applyLang();updateTimerUI();updateNavVisibility();
        var active=document.querySelector('.view.active');
        if(active&&active.id==='v-stats')renderStats();
        if(active&&active.id==='v-profile')renderProfile();
      }
    };
  }

  document.addEventListener('keydown',function(e){
    if(e.target&&/INPUT|TEXTAREA/.test(e.target.tagName))return;
    if(e.key===' '){e.preventDefault();el('btnStart').click();return;}
    var k=e.key.toLowerCase();
    if(k==='s')el('btnSkip').click();
    if(k==='r')el('btnReset').click();
    if(k==='e')el('btnEndSess').click();
    if(k==='m')el('btnMute').click();
  });

  el('onbNext').addEventListener('click',function(){
    if(onbStep>=ONB_STEPS.length-1){closeOnb();return;}
    onbStep++;renderOnb();
  });
  el('onbSkip').addEventListener('click',closeOnb);

  var onboarded=!!D.onboarded;
  if(!onboarded){try{onboarded=localStorage.getItem(LS_ONB)==='1';}catch(e){}}
  if(!onboarded)setTimeout(showOnboarding,400);

  setInterval(tick,250);
  tick();
  updateNavVisibility();
  if(T.run)requestWake();
}

document.addEventListener('DOMContentLoaded',init);
})();
</script>
</body>
</html>
