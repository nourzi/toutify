<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Toutify</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Sans:opsz,wght@9..40,300;9..40,400;9..40,500&display=swap" rel="stylesheet"/>
<style>
:root{
  --bg:#08080c;--s1:#111118;--s2:#18181f;--s3:#22222c;--s4:#2a2a38;
  --border:rgba(255,255,255,0.07);--border2:rgba(255,255,255,0.13);
  --text:#eeeef5;--muted:#7a7a9a;--dim:#44445a;
  --acc:#6c5fff;--acc2:#9b8fff;--acc-glow:rgba(108,95,255,0.2);
  --green:#22d98a;--amber:#f0a500;--red:#ff4d4d;--pink:#ff5fa0;--teal:#00d4cc;--blue:#3b9eff;
  --fh:'Syne',sans-serif;--fb:'DM Sans',sans-serif;
  --r:14px;--rs:8px;
}
*{box-sizing:border-box;margin:0;padding:0;}
body{background:var(--bg);color:var(--text);font-family:var(--fb);min-height:100vh;overflow-x:hidden;}
button{cursor:pointer;font-family:var(--fb);border:none;outline:none;}
input,textarea,select{font-family:var(--fb);outline:none;}
a{color:inherit;text-decoration:none;}

/* SCROLLBAR */
::-webkit-scrollbar{width:4px;height:4px;}
::-webkit-scrollbar-thumb{background:var(--s4);border-radius:4px;}

/* ── LAYOUT ── */
.root{display:flex;min-height:100vh;}
.sidebar{width:220px;background:var(--s1);border-right:1px solid var(--border);display:flex;flex-direction:column;padding:0;flex-shrink:0;position:sticky;top:0;height:100vh;overflow-y:auto;}
.main{flex:1;min-width:0;padding:2rem 2rem 4rem;max-width:980px;}

/* SIDEBAR */
.sb-logo{padding:1.4rem 1.2rem 1rem;border-bottom:1px solid var(--border);}
.sb-logo h1{font-family:var(--fh);font-size:20px;font-weight:800;letter-spacing:-.5px;}
.sb-logo h1 span{color:var(--acc2);}
.sb-logo .sb-user{font-size:11px;color:var(--muted);margin-top:3px;}
.sb-xp{padding:.8rem 1.2rem;border-bottom:1px solid var(--border);}
.sb-lvl-row{display:flex;align-items:center;justify-content:space-between;margin-bottom:5px;}
.sb-lvl{font-family:var(--fh);font-size:11px;font-weight:700;background:var(--acc);color:#fff;border-radius:999px;padding:2px 8px;}
.sb-xp-track{height:5px;background:var(--s3);border-radius:999px;overflow:hidden;}
.sb-xp-fill{height:100%;background:linear-gradient(90deg,var(--acc),var(--teal));border-radius:999px;transition:width .6s ease;}
.sb-xp-txt{font-size:10px;color:var(--muted);margin-top:3px;}
.sb-nav{padding:.6rem 0;flex:1;}
.sb-section{font-size:10px;font-weight:700;color:var(--dim);letter-spacing:.08em;padding:.6rem 1.2rem .3rem;font-family:var(--fh);}
.nav-item{display:flex;align-items:center;gap:9px;padding:.55rem 1.2rem;font-size:13px;color:var(--muted);cursor:pointer;transition:all .15s;border-left:2px solid transparent;}
.nav-item:hover{color:var(--text);background:var(--s2);}
.nav-item.active{color:var(--text);background:var(--s2);border-left-color:var(--acc);}
.nav-item .ni{font-size:15px;width:18px;text-align:center;}
.sb-bottom{padding:.8rem 1.2rem;border-top:1px solid var(--border);}
.sb-streak{display:flex;align-items:center;gap:6px;font-size:12px;color:var(--muted);}
.sb-streak-fire{color:var(--amber);font-size:16px;}

/* SCREENS */
.screen{display:none;animation:fadeUp .25s ease;}
.screen.active{display:block;}
@keyframes fadeUp{from{opacity:0;transform:translateY(8px);}to{opacity:1;transform:translateY(0);}}

/* COMMON */
.page-title{font-family:var(--fh);font-size:24px;font-weight:800;margin-bottom:4px;}
.page-sub{font-size:13px;color:var(--muted);margin-bottom:1.5rem;}
.sec-head{font-family:var(--fh);font-size:14px;font-weight:700;margin-bottom:.7rem;}
.card{background:var(--s1);border:1px solid var(--border);border-radius:var(--r);padding:1.2rem 1.4rem;}
.card2{background:var(--s2);border:1px solid var(--border);border-radius:var(--rs);padding:.9rem 1.1rem;}
.grid2{display:grid;grid-template-columns:repeat(auto-fit,minmax(200px,1fr));gap:12px;}
.grid3{display:grid;grid-template-columns:repeat(auto-fit,minmax(150px,1fr));gap:10px;}
.grid4{display:grid;grid-template-columns:repeat(auto-fit,minmax(120px,1fr));gap:10px;}
.stat-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:10px;margin-bottom:1.5rem;}
.stat-box{background:var(--s1);border:1px solid var(--border);border-radius:var(--rs);padding:.9rem 1rem;text-align:center;}
.stat-n{font-family:var(--fh);font-size:26px;font-weight:800;}
.stat-l{font-size:11px;color:var(--muted);margin-top:2px;}
.divider{border:none;border-top:1px solid var(--border);margin:1.2rem 0;}
.badge-pill{display:inline-flex;align-items:center;gap:4px;font-size:11px;font-weight:700;padding:3px 9px;border-radius:999px;font-family:var(--fh);}
.prog-bar{height:5px;background:var(--s3);border-radius:999px;overflow:hidden;}
.prog-fill{height:100%;border-radius:999px;transition:width .5s ease;}
.btn{display:inline-flex;align-items:center;gap:6px;padding:9px 18px;font-size:13px;font-weight:600;border-radius:var(--rs);border:1px solid var(--border2);background:var(--s2);color:var(--text);transition:all .2s;font-family:var(--fh);}
.btn:hover{background:var(--s3);border-color:rgba(255,255,255,.2);}
.btn-acc{background:var(--acc);border-color:var(--acc);color:#fff;}
.btn-acc:hover{background:var(--acc2);border-color:var(--acc2);}
.btn-sm{padding:6px 13px;font-size:12px;}
.btn-xs{padding:4px 10px;font-size:11px;}
.btn-danger{background:rgba(255,77,77,.15);border-color:var(--red);color:var(--red);}
.btn-danger:hover{background:rgba(255,77,77,.25);}
.inp{background:var(--s2);border:1px solid var(--border2);border-radius:var(--rs);padding:9px 13px;color:var(--text);font-size:13px;width:100%;transition:border-color .2s;}
.inp:focus{border-color:var(--acc);}
textarea.inp{resize:vertical;min-height:80px;line-height:1.6;}
.tag{font-size:11px;font-weight:700;padding:2px 8px;border-radius:999px;font-family:var(--fh);}
.row{display:flex;align-items:center;gap:8px;flex-wrap:wrap;}
.col{display:flex;flex-direction:column;gap:8px;}
.lbl{font-size:12px;color:var(--muted);margin-bottom:4px;display:block;}
.toast{position:fixed;bottom:24px;right:24px;background:var(--s2);border:1px solid var(--border2);border-radius:var(--rs);padding:10px 16px;font-size:13px;z-index:9999;transform:translateY(80px);opacity:0;transition:all .3s;pointer-events:none;max-width:300px;}
.toast.show{transform:translateY(0);opacity:1;}
.modal-bg{display:none;position:fixed;inset:0;background:rgba(0,0,0,.75);z-index:500;align-items:center;justify-content:center;padding:1rem;}
.modal-bg.open{display:flex;}
.modal{background:var(--s1);border:1px solid var(--border2);border-radius:var(--r);padding:1.5rem;width:100%;max-width:460px;max-height:90vh;overflow-y:auto;}
.modal-title{font-family:var(--fh);font-size:18px;font-weight:700;margin-bottom:1rem;}
.close-btn{background:none;border:none;color:var(--muted);font-size:20px;cursor:pointer;margin-left:auto;display:block;}

/* ── ONBOARDING / AUTH ── */
#screen-auth{display:flex;align-items:center;justify-content:center;min-height:100vh;background:var(--bg);}
.auth-box{width:100%;max-width:400px;text-align:center;}
.auth-logo{font-family:var(--fh);font-size:36px;font-weight:800;margin-bottom:4px;}
.auth-logo span{color:var(--acc2);}
.auth-sub{font-size:14px;color:var(--muted);margin-bottom:2rem;}
.auth-tabs{display:flex;background:var(--s2);border-radius:var(--rs);padding:4px;margin-bottom:1.5rem;}
.auth-tab{flex:1;padding:8px;font-size:13px;font-weight:600;border-radius:6px;background:none;color:var(--muted);transition:all .2s;font-family:var(--fh);}
.auth-tab.active{background:var(--acc);color:#fff;}
.auth-form{display:flex;flex-direction:column;gap:10px;}
.auth-divider{text-align:center;font-size:12px;color:var(--muted);margin:.5rem 0;}

/* ── HOME ── */
.subjects-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(155px,1fr));gap:10px;margin-bottom:1.5rem;}
.subj-card{background:var(--s1);border:1px solid var(--border);border-radius:var(--r);padding:1rem;cursor:pointer;transition:all .2s;position:relative;overflow:hidden;}
.subj-card::after{content:'';position:absolute;top:0;left:0;right:0;height:3px;}
.subj-card:hover{transform:translateY(-2px);border-color:var(--border2);}
.subj-card.sel{border-color:var(--acc);}
.subj-icon{font-size:24px;margin-bottom:8px;}
.subj-name{font-family:var(--fh);font-size:13px;font-weight:700;margin-bottom:4px;}
.subj-meta{font-size:11px;color:var(--muted);margin-bottom:7px;}
.add-subj{background:none;border:1px dashed var(--border2);border-radius:var(--r);padding:1rem;cursor:pointer;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:6px;color:var(--muted);transition:all .2s;min-height:110px;}
.add-subj:hover{border-color:var(--acc);color:var(--acc);}

/* ── FLASHCARDS ── */
.fc-wrap{display:flex;flex-direction:column;align-items:center;gap:1rem;}
.flashcard{width:100%;max-width:540px;min-height:230px;perspective:1000px;cursor:pointer;}
.fc-inner{position:relative;width:100%;min-height:230px;transform-style:preserve-3d;transition:transform .5s ease;border-radius:var(--r);}
.fc-inner.flipped{transform:rotateY(180deg);}
.fc-face{position:absolute;width:100%;min-height:230px;backface-visibility:hidden;border-radius:var(--r);display:flex;flex-direction:column;align-items:center;justify-content:center;padding:2rem;text-align:center;border:1px solid var(--border2);}
.fc-front{background:var(--s1);}
.fc-back{background:var(--s2);transform:rotateY(180deg);}
.fc-lbl{font-size:10px;font-family:var(--fh);font-weight:700;letter-spacing:.08em;color:var(--muted);margin-bottom:12px;}
.fc-q{font-size:17px;font-weight:500;line-height:1.6;}
.fc-sub{font-size:12px;color:var(--muted);margin-top:8px;}
.fc-dots{display:flex;gap:5px;}
.fc-dot{width:7px;height:7px;border-radius:50%;background:var(--s4);}
.fc-dot.done{background:var(--green);}
.fc-dot.cur{background:var(--acc);}
.rate-btns{display:flex;gap:8px;}

/* ── QUIZ ── */
.q-card{background:var(--s1);border:1px solid var(--border2);border-radius:var(--r);padding:1.4rem 1.6rem;font-size:16px;font-weight:500;line-height:1.6;margin-bottom:1rem;}
.opts{display:grid;grid-template-columns:1fr 1fr;gap:8px;}
.opt{background:var(--s1);border:1px solid var(--border);border-radius:var(--rs);padding:12px 16px;color:var(--text);font-size:13px;text-align:left;transition:all .2s;}
.opt:hover:not(:disabled){border-color:var(--acc);background:var(--s2);}
.opt.correct{background:rgba(34,217,138,.1);border-color:var(--green);color:var(--green);}
.opt.wrong{background:rgba(255,77,77,.1);border-color:var(--red);color:var(--red);}
.opt:disabled{cursor:default;}
.timer-bar{height:4px;background:var(--acc);border-radius:999px;transition:width 1s linear;margin-bottom:12px;}
.res-score{font-family:var(--fh);font-size:60px;font-weight:800;text-align:center;}

/* ── LEADERBOARD ── */
.lb-row{display:flex;align-items:center;gap:12px;padding:.75rem 1rem;border-bottom:1px solid var(--border);transition:background .15s;}
.lb-row:hover{background:var(--s2);}
.lb-rank{font-family:var(--fh);font-size:14px;font-weight:800;min-width:28px;text-align:center;}
.lb-avatar{width:36px;height:36px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-family:var(--fh);font-size:13px;font-weight:700;flex-shrink:0;}
.lb-info{flex:1;}
.lb-name{font-size:13px;font-weight:600;}
.lb-sub{font-size:11px;color:var(--muted);}
.lb-xp{font-family:var(--fh);font-size:14px;font-weight:700;color:var(--acc2);}
.lb-me{background:var(--acc-glow);border-radius:var(--rs);}

/* ── BATTLE ── */
.battle-search{display:flex;gap:8px;margin-bottom:1rem;}
.player-result{display:flex;align-items:center;gap:10px;padding:.8rem 1rem;background:var(--s2);border-radius:var(--rs);margin-bottom:8px;cursor:pointer;transition:all .2s;border:1px solid var(--border);}
.player-result:hover{border-color:var(--acc);}
.battle-arena{display:grid;grid-template-columns:1fr auto 1fr;gap:1rem;align-items:start;}
.battle-player{background:var(--s1);border:1px solid var(--border);border-radius:var(--r);padding:1rem;text-align:center;}
.battle-vs{font-family:var(--fh);font-size:20px;font-weight:800;color:var(--muted);align-self:center;text-align:center;}
.battle-score{font-family:var(--fh);font-size:32px;font-weight:800;}
.battle-prog{height:8px;border-radius:999px;overflow:hidden;background:var(--s3);margin-top:6px;}

/* ── AI TUTOR ── */
.chat-box{background:var(--s1);border:1px solid var(--border);border-radius:var(--r) var(--r) 0 0;min-height:320px;max-height:420px;overflow-y:auto;padding:1rem;display:flex;flex-direction:column;gap:10px;}
.msg{display:flex;gap:8px;max-width:85%;}
.msg.user{align-self:flex-end;flex-direction:row-reverse;}
.msg-av{width:28px;height:28px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:11px;font-weight:700;flex-shrink:0;font-family:var(--fh);}
.msg.msg-ai .msg-av{background:var(--acc);color:#fff;}
.msg.msg-user .msg-av{background:var(--s3);color:var(--muted);}
.msg-bub{padding:9px 13px;border-radius:12px;font-size:13px;line-height:1.6;}
.msg.msg-ai .msg-bub{background:var(--s2);border:1px solid var(--border);border-radius:4px 12px 12px 12px;}
.msg.msg-user .msg-bub{background:var(--acc);color:#fff;border-radius:12px 4px 12px 12px;}
.chat-input-bar{display:flex;gap:8px;padding:10px;background:var(--s2);border:1px solid var(--border);border-top:none;border-radius:0 0 var(--r) var(--r);}
.chat-input-bar input{flex:1;background:var(--s3);border:1px solid var(--border);border-radius:var(--rs);padding:9px 13px;color:var(--text);font-size:13px;}
.chat-input-bar input:focus{border-color:var(--acc);}
.typing-dots{display:flex;gap:4px;align-items:center;}
.tdot{width:6px;height:6px;border-radius:50%;background:var(--muted);animation:td 1.2s infinite;}
.tdot:nth-child(2){animation-delay:.2s;}.tdot:nth-child(3){animation-delay:.4s;}
@keyframes td{0%,60%,100%{transform:translateY(0);}30%{transform:translateY(-6px);}}

/* ── UPLOAD ── */
.upload-zone{border:2px dashed var(--border2);border-radius:var(--r);padding:2.5rem;text-align:center;cursor:pointer;transition:all .2s;}
.upload-zone:hover,.upload-zone.drag{border-color:var(--acc);background:var(--acc-glow);}
.yt-form{display:flex;gap:8px;margin-top:1rem;}
.gen-item{background:var(--s1);border:1px solid var(--border);border-radius:var(--rs);padding:.8rem 1rem;display:flex;gap:10px;align-items:flex-start;}
.gen-q{font-size:13px;font-weight:500;flex:1;}
.gen-a{font-size:12px;color:var(--muted);flex:1;}

/* ── STUDY MODES ── */
.mode-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(180px,1fr));gap:12px;}
.mode-card{background:var(--s1);border:1px solid var(--border);border-radius:var(--r);padding:1.2rem;cursor:pointer;transition:all .2s;text-align:center;}
.mode-card:hover{border-color:var(--border2);transform:translateY(-2px);}
.mode-icon{font-size:30px;margin-bottom:10px;}
.mode-name{font-family:var(--fh);font-size:14px;font-weight:700;margin-bottom:4px;}
.mode-desc{font-size:12px;color:var(--muted);line-height:1.5;}

/* Pomodoro timer */
.pomo-ring{position:relative;width:180px;height:180px;margin:0 auto 1.5rem;}
.pomo-svg{transform:rotate(-90deg);}
.pomo-track{fill:none;stroke:var(--s3);stroke-width:10;}
.pomo-prog{fill:none;stroke:var(--acc);stroke-width:10;stroke-linecap:round;transition:stroke-dashoffset .9s ease;}
.pomo-time{position:absolute;inset:0;display:flex;align-items:center;justify-content:center;font-family:var(--fh);font-size:32px;font-weight:800;}
.pomo-phase{text-align:center;font-size:12px;color:var(--muted);margin-bottom:1rem;font-family:var(--fh);letter-spacing:.06em;text-transform:uppercase;}
.pomo-btns{display:flex;justify-content:center;gap:8px;}

/* ── MAPS ── */
.map-canvas{background:var(--s1);border:1px solid var(--border);border-radius:var(--r);position:relative;height:360px;overflow:hidden;}
.mnode{position:absolute;border-radius:var(--rs);padding:7px 13px;font-size:12px;font-weight:700;font-family:var(--fh);cursor:pointer;transition:all .2s;z-index:2;white-space:nowrap;}
.mnode:hover{transform:scale(1.06);}
.mnode.center{background:var(--acc);color:#fff;font-size:13px;padding:9px 16px;}
.mnode.leaf{background:var(--s2);border:1px solid var(--border2);color:var(--text);}
.mnode.leaf:hover{border-color:var(--acc);color:var(--acc);}
.map-svg-layer{position:absolute;top:0;left:0;width:100%;height:100%;pointer-events:none;z-index:1;}

/* ── PROGRESS ── */
.prog-subj{background:var(--s1);border:1px solid var(--border);border-radius:var(--r);padding:1.1rem 1.3rem;}
.prog-header{display:flex;align-items:center;gap:8px;margin-bottom:10px;}
.week-bars{display:flex;align-items:flex-end;gap:5px;height:70px;}
.wbar-wrap{flex:1;display:flex;flex-direction:column;align-items:center;gap:4px;height:100%;justify-content:flex-end;}
.wbar{width:100%;border-radius:3px 3px 0 0;min-height:3px;}
.wlbl{font-size:9px;color:var(--muted);font-family:var(--fh);}
.streak-days{display:flex;gap:4px;align-items:flex-start;}
.sday{width:32px;height:32px;border-radius:7px;display:flex;align-items:center;justify-content:center;font-size:10px;font-weight:700;font-family:var(--fh);}
.sday.done{background:var(--green);color:#fff;}
.sday.today{background:var(--acc);color:#fff;}
.sday.miss{background:var(--s3);color:var(--muted);}

/* ── LEVELS / BADGES ── */
.lvl-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(120px,1fr));gap:10px;}
.lvl-card{background:var(--s1);border:1px solid var(--border);border-radius:var(--r);padding:.9rem;text-align:center;}
.lvl-card.unlocked{border-color:var(--acc);}
.lvl-card.current{border-color:var(--green);background:rgba(34,217,138,.04);}
.lvl-card.locked{opacity:.4;}
.lvl-n{font-family:var(--fh);font-size:28px;font-weight:800;}
.lvl-name{font-size:10px;font-family:var(--fh);font-weight:700;color:var(--muted);margin-top:2px;}
.lvl-req{font-size:9px;color:var(--muted);margin-top:3px;}
.badge-wrap{display:flex;flex-wrap:wrap;gap:8px;}
.bdg{background:var(--s2);border:1px solid var(--border);border-radius:var(--rs);padding:8px 12px;display:flex;align-items:center;gap:8px;}
.bdg.locked{opacity:.35;}
.bdg-icon{font-size:20px;}
.bdg-name{font-size:12px;font-weight:700;font-family:var(--fh);}
.bdg-desc{font-size:10px;color:var(--muted);}

/* ── ADMIN ── */
.admin-stats{display:grid;grid-template-columns:repeat(4,1fr);gap:10px;margin-bottom:1.5rem;}
.admin-stat{background:var(--s1);border:1px solid var(--border);border-radius:var(--rs);padding:.9rem;text-align:center;}
.admin-n{font-family:var(--fh);font-size:22px;font-weight:800;}
.admin-l{font-size:11px;color:var(--muted);}
.users-table{background:var(--s1);border:1px solid var(--border);border-radius:var(--r);overflow:hidden;}
.ut-head{display:grid;grid-template-columns:2fr 1fr 1fr 1fr 1fr auto;gap:8px;padding:.7rem 1rem;background:var(--s2);font-size:11px;font-weight:700;color:var(--muted);font-family:var(--fh);letter-spacing:.04em;}
.ut-row{display:grid;grid-template-columns:2fr 1fr 1fr 1fr 1fr auto;gap:8px;padding:.7rem 1rem;border-top:1px solid var(--border);align-items:center;font-size:13px;transition:background .15s;}
.ut-row:hover{background:var(--s2);}
.ut-name{display:flex;align-items:center;gap:8px;}
.ut-av{width:28px;height:28px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:11px;font-weight:700;font-family:var(--fh);}
.ut-status{font-size:11px;padding:2px 7px;border-radius:999px;font-family:var(--fh);font-weight:700;}
.ut-status.active{background:rgba(34,217,138,.15);color:var(--green);}
.ut-status.inactive{background:var(--s3);color:var(--muted);}
.admin-pass{font-size:12px;color:var(--muted);margin-top:6px;}
.admin-locked{display:flex;flex-direction:column;align-items:center;justify-content:center;min-height:400px;gap:1rem;text-align:center;}

/* SPINNER */
.spin{display:inline-block;width:14px;height:14px;border:2px solid rgba(255,255,255,.2);border-top-color:#fff;border-radius:50%;animation:sp .7s linear infinite;}
@keyframes sp{to{transform:rotate(360deg);}}

/* RESPONSIVE */
@media(max-width:700px){
  .sidebar{display:none;}
  .main{padding:1rem 1rem 4rem;}
  .opts{grid-template-columns:1fr;}
  .stat-grid{grid-template-columns:repeat(2,1fr);}
  .admin-stats{grid-template-columns:repeat(2,1fr);}
  .battle-arena{grid-template-columns:1fr;}
  .ut-head,.ut-row{grid-template-columns:2fr 1fr 1fr auto;}
  .ut-row .ut-lv,.ut-row .ut-subj,.ut-head .ut-lhd:nth-child(3),.ut-head .ut-lhd:nth-child(4){display:none;}
  .mobile-nav{display:flex;}
}
.mobile-nav{display:none;position:fixed;bottom:0;left:0;right:0;background:var(--s1);border-top:1px solid var(--border);z-index:200;padding:.4rem;}
.mob-btn{flex:1;display:flex;flex-direction:column;align-items:center;gap:2px;padding:.4rem;font-size:9px;color:var(--muted);background:none;border:none;font-family:var(--fh);font-weight:700;transition:color .15s;}
.mob-btn.active{color:var(--acc2);}
.mob-icon{font-size:18px;}
</style>
</head>
<body>

<!-- AUTH SCREEN -->
<div id="screen-auth">
  <div class="auth-box">
    <div class="auth-logo">Tout<span>ify</span></div>
    <p class="auth-sub">Study anything. Beat everyone.</p>

    <div class="auth-tabs">
      <button class="auth-tab active" onclick="switchAuthTab('login',this)">Sign in</button>
      <button class="auth-tab" onclick="switchAuthTab('register',this)">Create account</button>
    </div>

    <div class="auth-form" id="login-form">
      <input class="inp" id="li-user" placeholder="Username" onkeydown="if(event.key==='Enter')doLogin()"/>
      <div style="position:relative;display:flex;align-items:center;">
        <input class="inp" id="li-pass" placeholder="Password" type="password" style="padding-right:40px;" onkeydown="if(event.key==='Enter')doLogin()"/>
        <button onclick="toggleVis('li-pass',this)" style="position:absolute;right:10px;background:none;border:none;color:var(--muted);font-size:15px;cursor:pointer;">👁</button>
      </div>
      <button class="btn btn-acc" style="justify-content:center;" onclick="doLogin()">Sign in →</button>
    </div>

    <div class="auth-form" id="register-form" style="display:none;">
      <input class="inp" id="reg-user" placeholder="Choose a username (3+ chars)" onkeydown="if(event.key==='Enter')doRegister()"/>
      <input class="inp" id="reg-email" placeholder="Email address" onkeydown="if(event.key==='Enter')doRegister()"/>
      <div style="position:relative;display:flex;align-items:center;">
        <input class="inp" id="reg-pass" placeholder="Password" type="password" style="padding-right:40px;" onkeydown="if(event.key==='Enter')doRegister()"/>
        <button onclick="toggleVis('reg-pass',this)" style="position:absolute;right:10px;background:none;border:none;color:var(--muted);font-size:15px;cursor:pointer;">👁</button>
      </div>
      <button class="btn btn-acc" style="justify-content:center;" onclick="doRegister()">Create account →</button>
    </div>

    <div id="auth-error" style="display:none;margin-top:10px;padding:8px 12px;background:rgba(255,77,77,0.12);border:1px solid var(--red);border-radius:var(--rs);font-size:12px;color:var(--red);text-align:left;"></div>
  </div>
</div>

<!-- MAIN APP -->
<div id="app" style="display:none;" class="root">
  <!-- SIDEBAR -->
  <div class="sidebar">
    <div class="sb-logo">
      <h1>Tout<span>ify</span></h1>
      <div class="sb-user" id="sb-username">Loading...</div>
    </div>
    <div class="sb-xp">
      <div class="sb-lvl-row">
        <span id="sb-lvl-label" class="sb-lvl">Lv 1</span>
        <span style="font-size:11px;color:var(--muted);" id="sb-lvl-name">Novice</span>
      </div>
      <div class="sb-xp-track"><div class="sb-xp-fill" id="sb-xp-fill" style="width:0%"></div></div>
      <div class="sb-xp-txt" id="sb-xp-txt">0 / 300 XP</div>
    </div>
    <nav class="sb-nav">
      <div class="sb-section">STUDY</div>
      <div class="nav-item active" onclick="nav('home')"><span class="ni">🏠</span>Home</div>
      <div class="nav-item" onclick="nav('flashcards')"><span class="ni">🃏</span>Flashcards</div>
      <div class="nav-item" onclick="nav('quiz')"><span class="ni">📝</span>Quiz</div>
      <div class="nav-item" onclick="nav('tutor')"><span class="ni">🤖</span>AI Tutor</div>
      <div class="nav-item" onclick="nav('maps')"><span class="ni">🗺️</span>Concept Maps</div>
      <div class="nav-item" onclick="nav('study')"><span class="ni">⏱️</span>Study Modes</div>
      <div class="nav-item" onclick="nav('upload')"><span class="ni">📤</span>Upload Notes</div>
      <div class="sb-section">SOCIAL</div>
      <div class="nav-item" onclick="nav('leaderboard')"><span class="ni">🏆</span>Leaderboard</div>
      <div class="nav-item" onclick="nav('battle')"><span class="ni">⚔️</span>Battle</div>
      <div class="sb-section">STATS</div>
      <div class="nav-item" onclick="nav('progress')"><span class="ni">📊</span>Progress</div>
      <div class="nav-item" onclick="nav('levels')"><span class="ni">⭐</span>Levels</div>
      <div class="nav-item" id="admin-nav-item" style="display:none;" onclick="nav('admin')"><span class="ni">🔧</span>Admin Panel</div>
    </nav>
    <div class="sb-bottom">
      <div class="sb-streak"><span class="sb-streak-fire">🔥</span><span id="sb-streak-txt">0 day streak</span></div>
      <button class="btn btn-sm btn-danger" style="width:100%;justify-content:center;margin-top:8px;" onclick="doLogout()">Sign out</button>
    </div>
  </div>

  <!-- MAIN CONTENT -->
  <div class="main">

    <!-- HOME -->
    <div class="screen active" id="scr-home">
      <p class="page-title" id="home-greeting">Welcome back!</p>
      <p class="page-sub">What are you studying today?</p>
      <div class="stat-grid">
        <div class="stat-box"><div class="stat-n" style="color:var(--acc)" id="h-streak">0</div><div class="stat-l">day streak 🔥</div></div>
        <div class="stat-box"><div class="stat-n" style="color:var(--green)" id="h-cards">0</div><div class="stat-l">cards studied</div></div>
        <div class="stat-box"><div class="stat-n" style="color:var(--amber)" id="h-quizzes">0</div><div class="stat-l">quizzes done</div></div>
        <div class="stat-box"><div class="stat-n" style="color:var(--teal)" id="h-acc">—</div><div class="stat-l">avg accuracy</div></div>
      </div>
      <p class="sec-head">Your subjects</p>
      <div class="subjects-grid" id="subj-grid">
        <button class="add-subj" onclick="openModal('add-subj-modal')">
          <span style="font-size:22px;">+</span>
          <span style="font-size:12px;font-family:var(--fh);font-weight:700;">Add subject</span>
        </button>
      </div>
      <p class="sec-head">Quick start</p>
      <div class="row">
        <button class="btn btn-acc btn-sm" onclick="nav('flashcards')">Study flashcards</button>
        <button class="btn btn-sm" onclick="nav('quiz')">Take a quiz</button>
        <button class="btn btn-sm" onclick="nav('battle')">Challenge someone ⚔️</button>
        <button class="btn btn-sm" onclick="nav('study')">Study modes ⏱️</button>
      </div>
      <div id="ai-status-bar" style="margin-top:1rem;padding:10px 14px;border-radius:var(--rs);font-size:12px;display:none;"></div>
    </div>

    <!-- FLASHCARDS -->
    <div class="screen" id="scr-flashcards">
      <p class="page-title">Flashcards</p>
      <p class="page-sub">Tap to flip. Rate yourself to track progress.</p>
      <div class="row" id="fc-subj-pick" style="margin-bottom:1rem;"></div>
      <div class="fc-wrap">
        <div class="row" style="width:100%;max-width:540px;justify-content:space-between;">
          <span style="font-size:13px;color:var(--muted);" id="fc-counter">Card 1 / 6</span>
          <div class="fc-dots" id="fc-dots"></div>
        </div>
        <div class="flashcard" onclick="flipCard()">
          <div class="fc-inner" id="fc-inner">
            <div class="fc-face fc-front">
              <div class="fc-lbl">QUESTION</div>
              <div class="fc-q" id="fc-q">Loading...</div>
              <div class="fc-sub">Tap to reveal answer</div>
            </div>
            <div class="fc-face fc-back">
              <div class="fc-lbl">ANSWER</div>
              <div class="fc-q" id="fc-a"></div>
            </div>
          </div>
        </div>
        <div class="rate-btns" id="rate-btns" style="display:none;">
          <button class="btn btn-sm" style="border-color:var(--red);color:var(--red);" onclick="rateCard(0)">Again</button>
          <button class="btn btn-sm" style="border-color:var(--amber);color:var(--amber);" onclick="rateCard(1)">Hard</button>
          <button class="btn btn-sm" style="border-color:var(--green);color:var(--green);" onclick="rateCard(2)">Good</button>
          <button class="btn btn-sm" style="border-color:var(--teal);color:var(--teal);" onclick="rateCard(3)">Easy</button>
        </div>
        <div class="row">
          <button class="btn btn-sm" onclick="prevCard()">← Prev</button>
          <button class="btn btn-sm btn-acc" onclick="nextCard()">Next →</button>
        </div>
      </div>
    </div>

    <!-- QUIZ -->
    <div class="screen" id="scr-quiz">
      <p class="page-title">Quiz</p>
      <p class="page-sub">Timed multiple choice questions.</p>
      <div id="quiz-setup">
        <div class="card" style="margin-bottom:1rem;">
          <p class="sec-head" style="margin-bottom:.6rem;">Subject</p>
          <div class="row" id="qz-subj-pick"></div>
        </div>
        <div class="card" style="margin-bottom:1rem;">
          <p class="sec-head" style="margin-bottom:.6rem;">Questions</p>
          <div class="row">
            <button class="btn btn-sm qz-n-btn btn-acc" data-n="5" onclick="setQN(5,this)">5</button>
            <button class="btn btn-sm qz-n-btn" data-n="10" onclick="setQN(10,this)">10</button>
            <button class="btn btn-sm qz-n-btn" data-n="20" onclick="setQN(20,this)">20</button>
          </div>
        </div>
        <button class="btn btn-acc" onclick="startQuiz()">Start quiz →</button>
      </div>
      <div id="quiz-game" style="display:none;">
        <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:6px;">
          <span style="font-size:12px;color:var(--muted);" id="q-ctr">Q 1/5</span>
          <span style="font-family:var(--fh);font-size:13px;font-weight:700;color:var(--acc);" id="q-score-live">0 pts</span>
        </div>
        <div class="timer-bar" id="timer-bar"></div>
        <div class="q-card" id="q-text"></div>
        <div class="opts" id="q-opts"></div>
        <div id="q-exp" style="display:none;font-size:13px;color:var(--muted);padding:10px 14px;background:var(--s1);border-radius:var(--rs);border:1px solid var(--border);line-height:1.6;margin-top:8px;"></div>
        <button class="btn btn-sm btn-acc" id="q-next" style="display:none;margin-top:10px;" onclick="nextQ()">Next →</button>
      </div>
      <div id="quiz-result" style="display:none;text-align:center;padding:2rem;">
        <div class="res-score" id="res-score"></div>
        <p style="font-size:15px;color:var(--muted);margin:8px 0 4px;" id="res-lbl"></p>
        <p style="font-size:12px;color:var(--acc2);margin-bottom:1.5rem;" id="res-xp"></p>
        <div class="row" style="justify-content:center;">
          <button class="btn btn-acc" onclick="resetQuiz()">Try again</button>
          <button class="btn" onclick="nav('leaderboard')">See leaderboard</button>
        </div>
      </div>
    </div>

    <!-- LEADERBOARD -->
    <div class="screen" id="scr-leaderboard">
      <p class="page-title">Leaderboard</p>
      <p class="page-sub">Global rankings — updated in real time.</p>
      <div class="row" style="margin-bottom:1rem;">
        <button class="btn btn-sm btn-acc" onclick="renderLB('global')">Global</button>
        <button class="btn btn-sm" onclick="renderLB('weekly')">This week</button>
        <button class="btn btn-sm" onclick="renderLB('friends')">Friends</button>
      </div>
      <div class="card" style="padding:0;overflow:hidden;" id="lb-table"></div>
    </div>

    <!-- BATTLE -->
    <div class="screen" id="scr-battle">
      <p class="page-title">Battle ⚔️</p>
      <p class="page-sub">Search for a player and challenge them to a quiz duel.</p>
      <div id="battle-lobby">
        <div class="battle-search">
          <input class="inp" id="battle-search-inp" placeholder="Search username..." oninput="searchPlayers()"/>
        </div>
        <div id="battle-results"></div>
        <div class="card" style="margin-top:1rem;">
          <p class="sec-head">Online now</p>
          <div id="online-players"></div>
        </div>
      </div>
      <div id="battle-game" style="display:none;">
        <div class="battle-arena" id="battle-arena"></div>
        <div style="margin-top:1rem;" id="battle-q-area"></div>
      </div>
      <div id="battle-result" style="display:none;text-align:center;padding:2rem;">
        <div id="battle-res-content"></div>
        <button class="btn btn-acc" style="margin-top:1rem;" onclick="resetBattle()">Play again</button>
      </div>
    </div>

    <!-- AI TUTOR -->
    <div class="screen" id="scr-tutor">
      <p class="page-title">AI Tutor</p>
      <p class="page-sub">Ask anything. Get clear, exam-ready explanations.</p>
      <div class="row" id="tutor-subj-pick" style="margin-bottom:.8rem;"></div>
      <div class="chat-box" id="chat-box">
        <div class="msg msg-ai">
          <div class="msg-av">T</div>
          <div class="msg-bub">Hey! I'm your Toutify AI tutor. Pick a subject and ask me anything — concepts, problem-solving, definitions, or exam tips. Let's get studying! 📚</div>
        </div>
      </div>
      <div class="chat-input-bar">
        <input type="text" id="chat-inp" placeholder="Ask a question..." onkeydown="if(event.key==='Enter')sendChat()"/>
        <button class="btn btn-acc btn-sm" id="chat-send" onclick="sendChat()">Send</button>
      </div>
      <div class="row" style="margin-top:.8rem;flex-wrap:wrap;" id="quick-qs"></div>
    </div>

    <!-- CONCEPT MAPS -->
    <div class="screen" id="scr-maps">
      <p class="page-title">Concept Maps</p>
      <p class="page-sub">Visual overviews. Click any node to ask the AI tutor about it.</p>
      <div class="row" id="map-subj-pick" style="margin-bottom:.8rem;"></div>
      <div class="row" id="map-topic-pick" style="margin-bottom:.8rem;"></div>
      <div class="map-canvas" id="map-canvas"></div>
    </div>

    <!-- STUDY MODES -->
    <div class="screen" id="scr-study">
      <p class="page-title">Study Modes</p>
      <p class="page-sub">Find the method that works best for you.</p>
      <div id="study-home">
        <div class="mode-grid">
          <div class="mode-card" onclick="openMode('pomodoro')">
            <div class="mode-icon">🍅</div>
            <div class="mode-name">Pomodoro</div>
            <div class="mode-desc">25 min focus + 5 min breaks. Classic productivity technique.</div>
          </div>
          <div class="mode-card" onclick="openMode('blurting')">
            <div class="mode-icon">✍️</div>
            <div class="mode-name">Blurting</div>
            <div class="mode-desc">Write down everything you know. Check what you missed.</div>
          </div>
          <div class="mode-card" onclick="openMode('feynman')">
            <div class="mode-icon">🧑‍🏫</div>
            <div class="mode-name">Feynman Method</div>
            <div class="mode-desc">Explain a concept simply. The AI checks your understanding.</div>
          </div>
          <div class="mode-card" onclick="openMode('spaced')">
            <div class="mode-icon">📅</div>
            <div class="mode-name">Spaced Repetition</div>
            <div class="mode-desc">Cards due today based on your last rating. Optimal retention.</div>
          </div>
          <div class="mode-card" onclick="openMode('sprint')">
            <div class="mode-icon">⚡</div>
            <div class="mode-name">Speed Sprint</div>
            <div class="mode-desc">Answer as many questions as possible in 60 seconds.</div>
          </div>
          <div class="mode-card" onclick="openMode('deepwork')">
            <div class="mode-icon">🧘</div>
            <div class="mode-name">Deep Work</div>
            <div class="mode-desc">No distractions. Timed session with ambient focus music.</div>
          </div>
        </div>
      </div>

      <!-- POMODORO -->
      <div id="mode-pomodoro" style="display:none;text-align:center;max-width:380px;margin:0 auto;">
        <button class="btn btn-sm" style="margin-bottom:1.5rem;" onclick="closeMode()">← Back</button>
        <div class="pomo-ring">
          <svg class="pomo-svg" width="180" height="180" viewBox="0 0 180 180">
            <circle class="pomo-track" cx="90" cy="90" r="80"/>
            <circle class="pomo-prog" id="pomo-circle" cx="90" cy="90" r="80" stroke-dasharray="502" stroke-dashoffset="0"/>
          </svg>
          <div class="pomo-time" id="pomo-time">25:00</div>
        </div>
        <div class="pomo-phase" id="pomo-phase">FOCUS</div>
        <div style="font-size:12px;color:var(--muted);margin-bottom:1rem;" id="pomo-session">Session 1 of 4</div>
        <div class="pomo-btns">
          <button class="btn btn-acc" id="pomo-start-btn" onclick="togglePomo()">Start</button>
          <button class="btn btn-sm" onclick="resetPomo()">Reset</button>
        </div>
        <div style="margin-top:1.5rem;text-align:left;" class="card">
          <p class="sec-head">Session log</p>
          <div id="pomo-log" style="font-size:12px;color:var(--muted);min-height:40px;"></div>
        </div>
      </div>

      <!-- BLURTING -->
      <div id="mode-blurting" style="display:none;max-width:600px;">
        <button class="btn btn-sm" style="margin-bottom:1.2rem;" onclick="closeMode()">← Back</button>
        <div class="card" style="margin-bottom:1rem;">
          <p class="sec-head">Choose a topic to blurt</p>
          <div class="row" id="blurt-subj" style="margin-bottom:.8rem;"></div>
          <textarea class="inp" id="blurt-input" placeholder="Write EVERYTHING you know about this topic from memory. Don't look at your notes! When done, click Check." rows="6"></textarea>
          <button class="btn btn-acc btn-sm" style="margin-top:8px;" onclick="checkBlurt()">Check my knowledge →</button>
        </div>
        <div id="blurt-result" style="display:none;" class="card">
          <p class="sec-head">AI Feedback</p>
          <div id="blurt-feedback" style="font-size:13px;line-height:1.7;color:var(--muted);"></div>
        </div>
      </div>

      <!-- FEYNMAN -->
      <div id="mode-feynman" style="display:none;max-width:600px;">
        <button class="btn btn-sm" style="margin-bottom:1.2rem;" onclick="closeMode()">← Back</button>
        <div class="card" style="margin-bottom:1rem;">
          <p class="sec-head">Explain it like I'm 10</p>
          <p style="font-size:13px;color:var(--muted);margin-bottom:.8rem;">Pick a concept and explain it in the simplest possible terms. The AI will identify gaps in your understanding.</p>
          <input class="inp" id="feynman-topic" placeholder="Topic (e.g. 'DNA replication')" style="margin-bottom:8px;"/>
          <textarea class="inp" id="feynman-input" placeholder="Explain the concept as simply as possible..." rows="5"></textarea>
          <button class="btn btn-acc btn-sm" style="margin-top:8px;" onclick="checkFeynman()">Analyze my explanation →</button>
        </div>
        <div id="feynman-result" style="display:none;" class="card">
          <p class="sec-head">Analysis</p>
          <div id="feynman-feedback" style="font-size:13px;line-height:1.7;color:var(--muted);"></div>
        </div>
      </div>

      <!-- SPEED SPRINT -->
      <div id="mode-sprint" style="display:none;max-width:580px;">
        <button class="btn btn-sm" style="margin-bottom:1.2rem;" onclick="closeMode()">← Back</button>
        <div id="sprint-setup">
          <p class="sec-head">Choose subject</p>
          <div class="row" id="sprint-subj" style="margin-bottom:1rem;"></div>
          <button class="btn btn-acc" onclick="startSprint()">Start 60s sprint ⚡</button>
        </div>
        <div id="sprint-game" style="display:none;">
          <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:8px;">
            <span style="font-family:var(--fh);font-size:22px;font-weight:800;color:var(--acc);" id="sprint-timer">60</span>
            <span style="font-family:var(--fh);font-size:15px;font-weight:700;" id="sprint-score">0 correct</span>
          </div>
          <div class="timer-bar" id="sprint-bar" style="margin-bottom:12px;"></div>
          <div class="q-card" id="sprint-q"></div>
          <div class="opts" id="sprint-opts"></div>
        </div>
        <div id="sprint-result" style="display:none;text-align:center;padding:1.5rem;">
          <div style="font-family:var(--fh);font-size:48px;font-weight:800;color:var(--acc);" id="sprint-final"></div>
          <p style="color:var(--muted);margin:6px 0 1rem;font-size:14px;">questions answered correctly in 60s</p>
          <button class="btn btn-acc" onclick="startSprint()">Play again</button>
        </div>
      </div>

      <!-- DEEP WORK -->
      <div id="mode-deepwork" style="display:none;max-width:460px;text-align:center;">
        <button class="btn btn-sm" style="margin-bottom:1.5rem;" onclick="closeMode()">← Back</button>
        <div class="card" style="margin-bottom:1rem;">
          <p class="sec-head">Deep work session</p>
          <p style="font-size:13px;color:var(--muted);margin-bottom:1rem;">Set your session length and intention. No interruptions.</p>
          <label class="lbl">Session duration</label>
          <div class="row" style="margin-bottom:.8rem;">
            <button class="btn btn-sm dw-dur btn-acc" data-m="30" onclick="setDW(30,this)">30 min</button>
            <button class="btn btn-sm dw-dur" data-m="60" onclick="setDW(60,this)">60 min</button>
            <button class="btn btn-sm dw-dur" data-m="90" onclick="setDW(90,this)">90 min</button>
          </div>
          <label class="lbl">Session intention</label>
          <input class="inp" id="dw-intention" placeholder="e.g. Master the Krebs cycle" style="margin-bottom:8px;"/>
          <button class="btn btn-acc" style="width:100%;justify-content:center;" onclick="startDW()">Enter deep work 🧘</button>
        </div>
        <div id="dw-active" style="display:none;">
          <div style="font-family:var(--fh);font-size:42px;font-weight:800;margin-bottom:4px;" id="dw-timer">60:00</div>
          <p style="font-size:12px;color:var(--muted);margin-bottom:1rem;" id="dw-intention-display"></p>
          <div class="prog-bar" style="height:8px;margin-bottom:1rem;"><div class="prog-fill" id="dw-bar" style="width:100%;background:var(--teal);"></div></div>
          <button class="btn btn-danger btn-sm" onclick="endDW()">End session</button>
        </div>
      </div>

      <!-- SPACED REP info -->
      <div id="mode-spaced" style="display:none;max-width:560px;">
        <button class="btn btn-sm" style="margin-bottom:1.2rem;" onclick="closeMode()">← Back</button>
        <div class="card">
          <p class="sec-head">Spaced repetition queue</p>
          <p style="font-size:13px;color:var(--muted);margin-bottom:1rem;">Cards due for review today based on your previous ratings. Rate each card honestly — the algorithm adapts.</p>
          <div id="spaced-cards"></div>
          <button class="btn btn-acc btn-sm" style="margin-top:.8rem;" onclick="nav('flashcards')">Go to Flashcards →</button>
        </div>
      </div>
    </div>

    <!-- UPLOAD -->
    <div class="screen" id="scr-upload">
      <p class="page-title">Upload Notes</p>
      <p class="page-sub">Upload a PDF or paste your notes — AI generates flashcards and quiz questions instantly.</p>

      <!-- STEP 1: Subject -->
      <div class="card" style="margin-bottom:1rem;">
        <p class="sec-head">Step 1 — Name your subject</p>
        <div class="row">
          <input class="inp" id="upload-subj-name" placeholder="e.g. Biochemistry, Physics, History..." style="flex:1;"/>
          <select class="inp" id="upload-subj-existing" style="max-width:200px;" onchange="if(this.value)document.getElementById('upload-subj-name').value=this.value">
            <option value="">Or pick existing…</option>
          </select>
        </div>
      </div>

      <!-- STEP 2: Content -->
      <div class="card" style="margin-bottom:1rem;">
        <p class="sec-head">Step 2 — Add your content</p>
        <div style="display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-bottom:1rem;">
          <div class="upload-zone" id="pdf-drop" onclick="document.getElementById('pdf-file').click()" ondragover="event.preventDefault();this.classList.add('drag')" ondragleave="this.classList.remove('drag')" ondrop="handleDrop(event)" style="padding:1.2rem;">
            <div style="font-size:26px;margin-bottom:6px;">📄</div>
            <p style="font-size:13px;font-weight:700;font-family:var(--fh);">Upload PDF</p>
            <p style="font-size:11px;color:var(--muted);">click or drag & drop</p>
          </div>
          <div style="display:flex;flex-direction:column;gap:8px;">
            <input class="inp" id="yt-url" placeholder="YouTube URL (optional)"/>
            <button class="btn btn-sm" style="justify-content:center;" onclick="handleYT()">Use YouTube URL</button>
          </div>
        </div>
        <input type="file" id="pdf-file" accept=".pdf" style="display:none;" onchange="handlePDF(event)"/>
        <div id="pdf-name" style="font-size:12px;margin-bottom:8px;min-height:18px;"></div>
        <textarea class="inp" id="notes-txt" placeholder="Or paste lecture notes, textbook text, anything here…" rows="6"></textarea>
      </div>

      <!-- STEP 3: Generate -->
      <div class="card" style="margin-bottom:1rem;">
        <p class="sec-head">Step 3 — Generate study material</p>
        <p style="font-size:12px;color:var(--muted);margin-bottom:10px;">AI will create flashcards and quiz questions from your content.</p>
        <button class="btn btn-acc" onclick="generateNotes()" id="gen-btn" style="width:100%;justify-content:center;">✨ Generate flashcards & quiz</button>
      </div>

      <!-- Results -->
      <div id="upload-results" style="display:none;">
        <div class="card">
          <p class="sec-head" id="gen-result-title">Generated material</p>
          <div class="col" id="gen-cards" style="margin-bottom:1rem;max-height:400px;overflow-y:auto;"></div>
          <div class="row">
            <button class="btn btn-acc btn-sm" onclick="addGenCards()">✅ Add to my deck</button>
            <button class="btn btn-sm" onclick="clearGen()">Clear</button>
          </div>
        </div>
      </div>
    </div>

    <!-- PROGRESS -->
    <div class="screen" id="scr-progress">
      <p class="page-title">Progress</p>
      <p class="page-sub">Your learning journey at a glance.</p>
      <div class="grid2" id="prog-subjs" style="margin-bottom:1.5rem;"></div>
      <hr class="divider"/>
      <p class="sec-head">Weekly activity</p>
      <div class="card" style="margin-bottom:1.5rem;"><div class="week-bars" id="week-bars"></div></div>
      <p class="sec-head">Study streak</p>
      <div class="streak-days" id="streak-days"></div>
    </div>

    <!-- LEVELS -->
    <div class="screen" id="scr-levels">
      <p class="page-title">Levels & Badges</p>
      <p class="page-sub">Every XP point counts.</p>
      <div class="card" style="display:flex;align-items:center;gap:1.2rem;margin-bottom:1.5rem;">
        <div style="font-family:var(--fh);font-size:52px;font-weight:800;color:var(--acc);" id="cur-lvl-num">1</div>
        <div style="flex:1;">
          <p style="font-family:var(--fh);font-size:16px;font-weight:700;margin-bottom:4px;" id="cur-lvl-name">Novice</p>
          <p style="font-size:12px;color:var(--muted);margin-bottom:8px;" id="cur-lvl-xp">0 / 300 XP to Level 2</p>
          <div class="prog-bar"><div class="prog-fill" id="cur-lvl-fill" style="width:0%;background:linear-gradient(90deg,var(--acc),var(--teal));"></div></div>
        </div>
      </div>

      <!-- HOW TO EARN XP -->
      <p class="sec-head">How to earn XP</p>
      <div style="display:grid;grid-template-columns:repeat(auto-fill,minmax(170px,1fr));gap:8px;margin-bottom:1.5rem;">
        <div class="card2" style="display:flex;align-items:center;gap:10px;">
          <div style="font-size:22px;">🃏</div>
          <div>
            <div style="font-size:13px;font-weight:600;font-family:var(--fh);">Flashcards</div>
            <div style="font-size:11px;color:var(--muted);">+5 Again · +10 Hard<br>+15 Good · +20 Easy</div>
          </div>
        </div>
        <div class="card2" style="display:flex;align-items:center;gap:10px;">
          <div style="font-size:22px;">📝</div>
          <div>
            <div style="font-size:13px;font-weight:600;font-family:var(--fh);">Quiz</div>
            <div style="font-size:11px;color:var(--muted);">+20 XP per correct answer</div>
          </div>
        </div>
        <div class="card2" style="display:flex;align-items:center;gap:10px;">
          <div style="font-size:22px;">⚔️</div>
          <div>
            <div style="font-size:13px;font-weight:600;font-family:var(--fh);">Battle</div>
            <div style="font-size:11px;color:var(--muted);">+100 Win · +50 Tie<br>+25 Loss · +15/correct</div>
          </div>
        </div>
        <div class="card2" style="display:flex;align-items:center;gap:10px;">
          <div style="font-size:22px;">🤖</div>
          <div>
            <div style="font-size:13px;font-weight:600;font-family:var(--fh);">AI Tutor</div>
            <div style="font-size:11px;color:var(--muted);">+5 XP per message sent</div>
          </div>
        </div>
        <div class="card2" style="display:flex;align-items:center;gap:10px;">
          <div style="font-size:22px;">📤</div>
          <div>
            <div style="font-size:13px;font-weight:600;font-family:var(--fh);">Upload notes</div>
            <div style="font-size:11px;color:var(--muted);">+30 XP per generation</div>
          </div>
        </div>
        <div class="card2" style="display:flex;align-items:center;gap:10px;">
          <div style="font-size:22px;">🍅</div>
          <div>
            <div style="font-size:13px;font-weight:600;font-family:var(--fh);">Pomodoro</div>
            <div style="font-size:11px;color:var(--muted);">+30 XP per focus session</div>
          </div>
        </div>
        <div class="card2" style="display:flex;align-items:center;gap:10px;">
          <div style="font-size:22px;">✍️</div>
          <div>
            <div style="font-size:13px;font-weight:600;font-family:var(--fh);">Blurting</div>
            <div style="font-size:11px;color:var(--muted);">+25 XP per check</div>
          </div>
        </div>
        <div class="card2" style="display:flex;align-items:center;gap:10px;">
          <div style="font-size:22px;">⚡</div>
          <div>
            <div style="font-size:13px;font-weight:600;font-family:var(--fh);">Speed Sprint</div>
            <div style="font-size:11px;color:var(--muted);">+5 XP per correct answer</div>
          </div>
        </div>
        <div class="card2" style="display:flex;align-items:center;gap:10px;">
          <div style="font-size:22px;">🧘</div>
          <div>
            <div style="font-size:13px;font-weight:600;font-family:var(--fh);">Deep Work</div>
            <div style="font-size:11px;color:var(--muted);">+60 XP full session</div>
          </div>
        </div>
      </div>

      <div class="lvl-grid" id="lvl-grid" style="margin-bottom:1.5rem;"></div>
      <hr class="divider"/>
      <p class="sec-head">Badges</p>
      <div class="badge-wrap" id="badge-wrap"></div>
    </div>

    <!-- ADMIN -->
    <div class="screen" id="scr-admin">
      <div id="admin-locked-view" class="admin-locked">
        <div style="font-size:40px;">🔒</div>
        <p style="font-family:var(--fh);font-size:18px;font-weight:700;">Admin area</p>
        <p style="font-size:13px;color:var(--muted);">Enter the admin password to access</p>
        <input class="inp" id="admin-pw-inp" type="password" placeholder="Admin password" style="max-width:280px;"/>
        <button class="btn btn-acc" onclick="unlockAdmin()">Unlock</button>
      </div>
      <div id="admin-panel" style="display:none;">
        <p class="page-title">Admin Panel 🔧</p>
        <p class="page-sub">Full visibility into all users and activity.</p>


        <div class="admin-stats" id="admin-stats-row"></div>
        <div class="row" style="margin-bottom:1rem;">
          <input class="inp" id="admin-search" placeholder="Search users..." oninput="filterAdminUsers()" style="max-width:260px;"/>
          <button class="btn btn-sm btn-acc" onclick="exportUsers()">Export CSV</button>
          <button class="btn btn-sm btn-danger" onclick="if(confirm('Reset ALL user data?'))resetAllUsers()">Reset all</button>
        </div>
        <div class="users-table" id="users-table"></div>
      </div>
    </div>

  </div><!-- /main -->
</div><!-- /app -->

<!-- MOBILE NAV -->
<nav class="mobile-nav" id="mob-nav">
  <button class="mob-btn active" onclick="nav('home')"><span class="mob-icon">🏠</span>Home</button>
  <button class="mob-btn" onclick="nav('flashcards')"><span class="mob-icon">🃏</span>Cards</button>
  <button class="mob-btn" onclick="nav('quiz')"><span class="mob-icon">📝</span>Quiz</button>
  <button class="mob-btn" onclick="nav('leaderboard')"><span class="mob-icon">🏆</span>Ranks</button>
  <button class="mob-btn" onclick="nav('battle')"><span class="mob-icon">⚔️</span>Battle</button>
</nav>

<!-- MODALS -->
<div class="modal-bg" id="add-subj-modal">
  <div class="modal">
    <p class="modal-title">Add a subject</p>
    <div style="margin-bottom:.8rem;"><label class="lbl">Name</label><input class="inp" id="ns-name" placeholder="e.g. Organic Chemistry"/></div>
    <div style="margin-bottom:.8rem;"><label class="lbl">Icon (emoji)</label><input class="inp" id="ns-icon" placeholder="🧪" style="width:80px;" maxlength="2"/></div>
    <div style="margin-bottom:1rem;">
      <label class="lbl">Color</label>
      <div class="row" id="ns-colors">
        <div style="width:22px;height:22px;border-radius:50%;background:#6c5fff;border:2px solid #fff;cursor:pointer;" data-c="#6c5fff" onclick="pickNSColor(this)"></div>
        <div style="width:22px;height:22px;border-radius:50%;background:#22d98a;border:2px solid transparent;cursor:pointer;" data-c="#22d98a" onclick="pickNSColor(this)"></div>
        <div style="width:22px;height:22px;border-radius:50%;background:#f0a500;border:2px solid transparent;cursor:pointer;" data-c="#f0a500" onclick="pickNSColor(this)"></div>
        <div style="width:22px;height:22px;border-radius:50%;background:#ff4d4d;border:2px solid transparent;cursor:pointer;" data-c="#ff4d4d" onclick="pickNSColor(this)"></div>
        <div style="width:22px;height:22px;border-radius:50%;background:#00d4cc;border:2px solid transparent;cursor:pointer;" data-c="#00d4cc" onclick="pickNSColor(this)"></div>
        <div style="width:22px;height:22px;border-radius:50%;background:#ff5fa0;border:2px solid transparent;cursor:pointer;" data-c="#ff5fa0" onclick="pickNSColor(this)"></div>
        <div style="width:22px;height:22px;border-radius:50%;background:#3b9eff;border:2px solid transparent;cursor:pointer;" data-c="#3b9eff" onclick="pickNSColor(this)"></div>
      </div>
    </div>
    <div class="row">
      <button class="btn btn-acc btn-sm" onclick="addSubject()">Add subject</button>
      <button class="btn btn-sm" onclick="closeModal('add-subj-modal')">Cancel</button>
    </div>
  </div>
</div>

<div class="toast" id="toast"></div>

<script>
// Gemini models to try in order (v1 = stable, v1beta = experimental)
// AI via OpenRouter — free tier, works worldwide, no region restrictions
const OR_KEY = "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"; // get free key at openrouter.ai
const OR_API = "https://openrouter.ai/api/v1/chat/completions";
// openrouter/free auto-selects the best available free model
// fallbacks are current confirmed free models as of April 2026
const OR_MODELS = [
  "openrouter/auto",
  "meta-llama/llama-3.3-70b-instruct:free",
  "deepseek/deepseek-r1:free",
  "mistralai/mistral-small-3.1-24b-instruct:free",
  "qwen/qwq-32b:free",
  "google/gemma-3-27b-it:free",
  "nvidia/llama-3.1-nemotron-70b-instruct:free",
  "meta-llama/llama-3.1-8b-instruct:free"
];
const ADMIN_PASS = "toutify2024";
const LVL_NAMES = ["Novice","Apprentice","Scholar","Adept","Expert","Master","Professor","Genius","Sage","Legend"];
const LVL_XP = [300,600,1000,1500,2200,3000,4000,5200,6600,8200];

// ════════════════════════════════
//  AI via OpenRouter (free, worldwide)
// ════════════════════════════════
async function callAI(system, userMsg, maxTokens = 800) {
  let lastErr = null;
  const msgs = [
    ...(system ? [{ role: 'system', content: system }] : []),
    { role: 'user', content: userMsg }
  ];

  for (const model of OR_MODELS) {
    try {
      console.log('[Toutify AI] Trying model:', model);
      const res = await fetch(OR_API, {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
          'Authorization': 'Bearer ' + OR_KEY,
          'HTTP-Referer': 'https://toutify.app',
          'X-Title': 'Toutify'
        },
        body: JSON.stringify({ model, max_tokens: maxTokens, messages: msgs })
      });

      let data;
      try { data = await res.json(); }
      catch(e) { lastErr = 'Bad JSON response'; continue; }

      console.log('[Toutify AI] Response status:', res.status, 'model:', model);

      if (!res.ok) {
        lastErr = data?.error?.message || data?.message || ('HTTP ' + res.status);
        console.warn('[Toutify AI] Model', model, 'failed:', lastErr);
        continue;
      }

      const text = data.choices?.[0]?.message?.content?.trim() || '';
      if (!text) {
        lastErr = 'Empty response from ' + model;
        console.warn('[Toutify AI]', lastErr);
        continue;
      }

      console.log('[Toutify AI] Success with model:', model);
      return text;

    } catch(e) {
      lastErr = e.message;
      console.warn('[Toutify AI] Network error with', model, ':', e.message);
      continue;
    }
  }
  throw new Error(lastErr || 'All AI models failed. Check browser console for details.');
}

async function testAIConnection() {
  const bar = document.getElementById('ai-status-bar');
  if (!bar) return;
  bar.style.cssText = 'display:block;padding:10px 14px;border-radius:8px;font-size:12px;background:var(--s2);color:var(--muted);border:1px solid var(--border);margin-top:1rem;';
  bar.innerHTML = '🔄 Checking AI connection...';
  try {
    const reply = await callAI('You must reply with only the single word: ONLINE', 'ping', 10);
    bar.style.background = 'rgba(34,217,138,0.1)';
    bar.style.border = '1px solid #22d98a';
    bar.style.color = '#22d98a';
    bar.innerHTML = '✅ AI is online and ready — upload a PDF to start studying!';
    setTimeout(() => { bar.style.display = 'none'; }, 5000);
  } catch(e) {
    bar.style.background = 'rgba(255,77,77,0.1)';
    bar.style.border = '1px solid #ff4d4d';
    bar.style.color = '#ff4d4d';
    bar.innerHTML = '❌ AI error: ' + e.message + ' (check browser console F12 for details)';
  }
}

function toggleVis(inputId, btn) {
  const inp = document.getElementById(inputId);
  if (!inp) return;
  inp.type = inp.type === 'password' ? 'text' : 'password';
  btn.textContent = inp.type === 'password' ? '👁' : '🙈';
}

function showAuthError(msg) {
  const el = document.getElementById('auth-error');
  if (!el) return;
  el.textContent = msg;
  el.style.display = 'block';
  setTimeout(() => { el.style.display = 'none'; }, 4000);
}

// ════════════════════════════════
//  DATA STORE
// ════════════════════════════════
function loadDB() {
  try { return JSON.parse(localStorage.getItem('toutify_db') || '{}'); }
  catch { return {}; }
}
function saveDB(db) {
  try { localStorage.setItem('toutify_db', JSON.stringify(db)); }
  catch(e) { console.warn('saveDB failed:', e); }
}
function getUser(un) { const db = loadDB(); return db[un.toLowerCase()] || null; }
function saveUser(u) { const db = loadDB(); db[u.username.toLowerCase()] = u; saveDB(db); }
function getAllUsers() { return Object.values(loadDB()); }

function createUser(username, email, password) {
  return {
    username, email,
    password,
    created: Date.now(),
    lastSeen: Date.now(),
    xp: 0, level: 1, streak: 0,
    cardsStudied: 0, quizzesDone: 0,
    quizHistory: [],
    subjects: [],
    extraCards: [],
    badges: [],
    weeklyXP: [0,0,0,0,0,0,0],
    streakDays: Array(7).fill(false),
    totalAccuracy: 0, accuracyCount: 0,
    qzDB: {}
  };
}

// ════════════════════════════════
//  AUTH
// ════════════════════════════════
let CU = null;

function switchAuthTab(tab, el) {
  document.querySelectorAll('.auth-tab').forEach(b => b.classList.remove('active'));
  el.classList.add('active');
  document.getElementById('login-form').style.display = tab === 'login' ? 'flex' : 'none';
  document.getElementById('register-form').style.display = tab === 'register' ? 'flex' : 'none';
  document.getElementById('auth-error').style.display = 'none';
}

function doLogin() {
  const un = document.getElementById('li-user').value.trim();
  const pw = document.getElementById('li-pass').value;
  if (!un) { showAuthError('Enter your username.'); return; }
  if (!pw) { showAuthError('Enter your password.'); return; }

  if (un.toLowerCase() === 'admin' && pw === ADMIN_PASS) {
    CU = createUser('admin', 'admin@toutify.com', ADMIN_PASS);
    CU.isAdmin = true; CU.xp = 0; CU.level = 1;
    bootApp(); return;
  }

  const u = getUser(un);
  if (!u) { showAuthError('Username not found. Check spelling or create an account.'); return; }
  if (u.password !== pw) { showAuthError('Wrong password. Try again.'); return; }

  CU = u;
  CU.lastSeen = Date.now();
  if (CU.qzDB) Object.assign(qzDB, CU.qzDB);
  saveUser(CU);
  bootApp();
}

function doRegister() {
  const un = document.getElementById('reg-user').value.trim();
  const em = document.getElementById('reg-email').value.trim();
  const pw = document.getElementById('reg-pass').value;

  if (!un) { showAuthError('Enter a username.'); return; }
  if (un.length < 3) { showAuthError('Username must be at least 3 characters.'); return; }
  if (!/^[a-zA-Z0-9_]+$/.test(un)) { showAuthError('Username can only contain letters, numbers and underscores.'); return; }
  if (!em || !em.includes('@')) { showAuthError('Enter a valid email address.'); return; }
  if (!pw || pw.length < 4) { showAuthError('Password must be at least 4 characters.'); return; }
  if (getUser(un)) { showAuthError('Username already taken. Choose another.'); return; }

  CU = createUser(un, em, pw);
  saveUser(CU);
  bootApp();
}

function doLogout() {
  if (CU && !CU.isAdmin) persistUser();
  CU = null;
  qzDB = {};
  document.getElementById('app').style.display = 'none';
  document.getElementById('screen-auth').style.display = 'flex';
  document.getElementById('mob-nav').style.display = 'none';
}

function saveAdminKey() {
  const inp = document.getElementById('admin-api-key');
  if (!inp) return;
  const key = inp.value.trim();
  if (!key || !key.startsWith('sk-')) {
    toast('Invalid key — must start with sk-'); return;
  }
  localStorage.setItem('toutify_apikey', key);
  updateKeyStatus();
  toast('✅ API key saved! AI features are now active for all users.');
}

async function testApiKey() {
  const key = "";
  if (!key) { toast('No key saved yet.'); return; }
  const btn = document.querySelector('#admin-panel .btn[onclick="testApiKey()"]');
  if (btn) { btn.disabled = true; btn.textContent = 'Testing...'; }
  try {
    const reply = await callAI('Reply with exactly: OK', 'ping', 10);
    toast('✅ API key works! AI is live.');
    updateKeyStatus(true);
  } catch(e) {
    toast('❌ Key error: ' + e.message);
    updateKeyStatus(false);
  }
  if (btn) { btn.disabled = false; btn.textContent = 'Test'; }
}

function updateKeyStatus(working) {
  const el = document.getElementById('key-status-txt');
  if (!el) return;
  const key = "";
  if (!key) { el.textContent = 'not set'; el.style.color = 'var(--red)'; return; }
  const masked = key.slice(0, 10) + '••••••••••••••' + key.slice(-4);
  if (working === true) { el.textContent = `✅ working — ${masked}`; el.style.color = 'var(--green)'; }
  else if (working === false) { el.textContent = `❌ invalid — ${masked}`; el.style.color = 'var(--red)'; }
  else { el.textContent = `set — ${masked}`; el.style.color = 'var(--muted)'; }
}

function bootApp() {
  // Purge any stale demo accounts that were seeded in v1
  const demoNames = ['Sarah_K','Omar_M','Lena_R','Alex_T','Mia_W'];
  const db = loadDB();
  let changed = false;
  demoNames.forEach(n => { if (db[n]) { delete db[n]; changed = true; } });
  if (changed) saveDB(db);

  document.getElementById('screen-auth').style.display = 'none';
  document.getElementById('app').style.display = 'flex';
  document.getElementById('mob-nav').style.display = 'flex';
  if (CU.isAdmin) document.getElementById('admin-nav-item').style.display = 'flex';
  updateSidebar();
  renderHome();
  renderSubjPickers();
  renderProgress();
  renderWeeklyBars();
  renderStreak();
  renderLevels();
  renderBadges();
  loadFC();
  renderQZSubj();
  renderLB('global');
  renderOnlinePlayers();
  renderSprintSubj();
  renderBlurtSubj();
  renderMapSubj();
  renderMapTopics();
  drawMap();
  toast(`Welcome back, ${CU.username}! 👋`);
  // Silently test AI connection on login
  setTimeout(testAIConnection, 1500);
  setTimeout(populateExistingSubjects, 100);
}

// ════════════════════════════════
//  NAVIGATION
// ════════════════════════════════
let currentScreen = 'home';
function nav(id) {
  document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
  document.getElementById('scr-'+id).classList.add('active');
  document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
  document.querySelectorAll('.mob-btn').forEach(b => b.classList.remove('active'));
  const navMap = {home:0,flashcards:1,quiz:2,tutor:3,maps:4,study:5,upload:6,leaderboard:8,battle:9,progress:11,levels:12,admin:13};
  const ni = document.querySelectorAll('.nav-item');
  if (navMap[id] !== undefined) ni[navMap[id]]?.classList.add('active');
  currentScreen = id;
  if (id === 'maps') { setTimeout(()=>{ renderMapTopics(); drawMap(); }, 60); }
  if (id === 'upload') { populateExistingSubjects(); }
  if (id === 'leaderboard') renderLB('global');
  if (id === 'admin') { renderAdminPanel(); }
}

// ════════════════════════════════
//  SIDEBAR / XP
// ════════════════════════════════
function updateSidebar() {
  document.getElementById('sb-username').textContent = CU.username;
  const lvlXP = LVL_XP[CU.level - 1] || 300;
  const pct = Math.round((CU.xp / lvlXP) * 100);
  document.getElementById('sb-xp-fill').style.width = pct + '%';
  document.getElementById('sb-xp-txt').textContent = `${CU.xp} / ${lvlXP} XP`;
  document.getElementById('sb-lvl-label').textContent = 'Lv ' + CU.level;
  document.getElementById('sb-lvl-name').textContent = LVL_NAMES[CU.level - 1] || 'Legend';
  document.getElementById('sb-streak-txt').textContent = CU.streak + ' day streak';
}

function gainXP(amount) {
  CU.xp += amount;
  const needed = LVL_XP[CU.level - 1] || 300;
  if (CU.xp >= needed) {
    CU.xp -= needed;
    CU.level = Math.min(CU.level + 1, 10);
    toast(`🎉 Level up! You're now Level ${CU.level} — ${LVL_NAMES[CU.level-1]}!`);
    renderLevels();
  }
  CU.weeklyXP = CU.weeklyXP || [0,0,0,0,0,0,0];
  const dayIdx = new Date().getDay();
  CU.weeklyXP[dayIdx] = (CU.weeklyXP[dayIdx] || 0) + amount;
  persistUser();
  updateSidebar();
  updateLevelScreen();
}

function persistUser() {
  if (!CU || CU.isAdmin) return;
  CU.qzDB = qzDB;
  persistUser();
}

function updateLevelScreen() {
  const lvlXP = LVL_XP[CU.level - 1] || 300;
  const pct = Math.round((CU.xp / lvlXP) * 100);
  const el1 = document.getElementById('cur-lvl-num');
  const el2 = document.getElementById('cur-lvl-name');
  const el3 = document.getElementById('cur-lvl-xp');
  const el4 = document.getElementById('cur-lvl-fill');
  if (el1) el1.textContent = CU.level;
  if (el2) el2.textContent = LVL_NAMES[CU.level - 1];
  if (el3) el3.textContent = `${CU.xp} / ${lvlXP} XP to Level ${CU.level + 1}`;
  if (el4) el4.style.width = pct + '%';
}

// ════════════════════════════════
//  HOME
// ════════════════════════════════
function renderHome() {
  const hr = new Date().getHours();
  const greet = hr < 12 ? 'Good morning' : hr < 17 ? 'Good afternoon' : 'Good evening';
  document.getElementById('home-greeting').textContent = `${greet}, ${CU.username}! 👋`;
  document.getElementById('h-streak').textContent = CU.streak;
  document.getElementById('h-cards').textContent = CU.cardsStudied;
  document.getElementById('h-quizzes').textContent = CU.quizzesDone;
  const acc = CU.accuracyCount > 0 ? Math.round(CU.totalAccuracy / CU.accuracyCount) + '%' : '—';
  document.getElementById('h-acc').textContent = acc;
  renderSubjGrid();
}

function renderSubjGrid() {
  const grid = document.getElementById('subj-grid');
  const addBtn = grid.querySelector('.add-subj');
  grid.innerHTML = '';
  CU.subjects.forEach((s, i) => {
    const card = document.createElement('div');
    card.className = 'subj-card';
    card.innerHTML = `<style>.subj-card:nth-child(${i+1})::after{background:${s.color};}</style>
      <div class="subj-icon">${s.icon}</div>
      <div class="subj-name">${s.name}</div>
      <div class="subj-meta" style="color:${s.color}">${s.progress || 0}% mastery</div>
      <div class="prog-bar"><div class="prog-fill" style="width:${s.progress||0}%;background:${s.color};"></div></div>`;
    card.onclick = () => { subjState.active = i; renderSubjPickers(); toast('Switched to ' + s.name); };
    grid.appendChild(card);
  });
  const ab = document.createElement('button');
  ab.className = 'add-subj';
  ab.innerHTML = '<span style="font-size:22px;">+</span><span style="font-size:12px;font-family:var(--fh);font-weight:700;">Add subject</span>';
  ab.onclick = () => openModal('add-subj-modal');
  grid.appendChild(ab);
}

// ════════════════════════════════
//  SUBJECT MANAGEMENT
// ════════════════════════════════
let subjState = { active: 0, nsColor: '#6c5fff' };
let fcDB = {}, qzDB = {};

let nsColor = '#6c5fff';
function pickNSColor(el) {
  document.querySelectorAll('#ns-colors > div').forEach(d => d.style.borderColor = 'transparent');
  el.style.borderColor = '#fff';
  nsColor = el.dataset.c;
}

function addSubject() {
  const name = document.getElementById('ns-name').value.trim();
  const icon = document.getElementById('ns-icon').value.trim() || '📖';
  if (!name) { toast('Enter a subject name'); return; }
  CU.subjects.push({ name, icon, color: nsColor, progress: 0, cards: 0, quizzes: 0 });
  if (!fcDB[name]) fcDB[name] = [];
  if (!qzDB[name]) qzDB[name] = [];
  persistUser();
  closeModal('add-subj-modal');
  renderHome();
  renderSubjPickers();
  renderProgress();
  document.getElementById('ns-name').value = '';
  document.getElementById('ns-icon').value = '';
  toast(`${icon} ${name} added!`);
}

// ── Only show user-uploaded content in flashcards ──
function getFC(subj) {
  const extras = (CU.extraCards||[]).filter(c => c.subject === subj);
  return extras;
}
function getQZ(subj) {
  return [...(qzDB[subj]||[])];
}
function getAllUserSubjects() {
  // subjects the user has uploaded PDFs for (has cards or quiz questions)
  const fromCards = [...new Set((CU.extraCards||[]).map(c=>c.subject))];
  const fromQZ = Object.keys(qzDB).filter(k => (qzDB[k]||[]).length > 0);
  return [...new Set([...fromCards, ...fromQZ])];
}

function renderSubjPickers() {
  const pickers = [
    {id:'fc-subj-pick', stateProp:'fcSubj'},
    {id:'qz-subj-pick', stateProp:'qzSubj'},
    {id:'tutor-subj-pick', stateProp:'tutorSubj'},
    {id:'map-subj-pick', stateProp:'mapSubj'},
    {id:'upload-subj-pick', stateProp:'uploadSubj'},
  ];
  // For upload picker: use all user-added subjects
  const uploadSubjs = CU.subjects.map(s=>s.name);
  // For study pickers: only subjects that have uploaded content
  const studySubjs = getAllUserSubjects();

  pickers.forEach(({id, stateProp}) => {
    const el = document.getElementById(id);
    if (!el) return;
    if (!subjState[stateProp]) subjState[stateProp] = 0;
    el.innerHTML = '';
    const list = stateProp === 'uploadSubj' ? uploadSubjs : studySubjs;
    if (!list.length) {
      if (stateProp !== 'uploadSubj') {
        el.innerHTML = '<span style="font-size:12px;color:var(--muted);">Upload a PDF first to study</span>';
      }
      return;
    }
    list.forEach((s, i) => {
      const btn = document.createElement('button');
      btn.className = 'btn btn-sm' + (i === subjState[stateProp] ? ' btn-acc' : '');
      btn.textContent = s;
      btn.onclick = () => {
        subjState[stateProp] = i;
        renderSubjPickers();
        if (stateProp === 'fcSubj') { fcState.idx = 0; fcState.flipped = false; loadFC(); }
        if (stateProp === 'mapSubj') { subjState.mapTopic = 0; renderMapTopics(); drawMap(); }
        if (stateProp === 'tutorSubj') renderQuickQs();
      };
      el.appendChild(btn);
    });
  });
  renderQuickQs();
}

function activeSubjName(prop) {
  if (prop === 'uploadSubj') {
    const list = CU.subjects.map(s=>s.name);
    return list[subjState[prop] || 0] || '';
  }
  const list = getAllUserSubjects();
  return list[subjState[prop] || 0] || '';
}

// ════════════════════════════════
//  FLASHCARDS
// ════════════════════════════════
let fcState = { idx: 0, flipped: false };

function loadFC() {
  const sub = activeSubjName('fcSubj');
  const cards = sub ? getFC(sub) : [];
  if (!sub || !cards.length) {
    document.getElementById('fc-q').textContent = '📤 No flashcards yet! Go to Upload Notes, upload a PDF or paste text, then click "Add to deck".';
    document.getElementById('fc-a').textContent = '';
    document.getElementById('fc-counter').textContent = 'No cards';
    document.getElementById('fc-dots').innerHTML = '';
    document.getElementById('rate-btns').style.display = 'none';
    return;
  }
  const i = fcState.idx % cards.length;
  const card = cards[i];
  document.getElementById('fc-q').textContent = card.q;
  document.getElementById('fc-a').textContent = card.a;
  document.getElementById('fc-counter').textContent = `Card ${i+1} / ${cards.length}`;
  fcState.flipped = false;
  document.getElementById('fc-inner').classList.remove('flipped');
  document.getElementById('rate-btns').style.display = 'none';
  // dots
  const dotsEl = document.getElementById('fc-dots');
  dotsEl.innerHTML = '';
  const total = Math.min(cards.length, 8);
  for (let d = 0; d < total; d++) {
    const dot = document.createElement('div');
    dot.className = 'fc-dot' + (d < i ? ' done' : d === i ? ' cur' : '');
    dotsEl.appendChild(dot);
  }
}

function flipCard() {
  if (!fcState.flipped) {
    fcState.flipped = true;
    document.getElementById('fc-inner').classList.add('flipped');
    document.getElementById('rate-btns').style.display = 'flex';
  }
}

function rateCard(r) {
  gainXP([5,10,15,20][r]);
  CU.cardsStudied++;
  persistUser();
  renderHome();
  document.getElementById('h-cards').textContent = CU.cardsStudied;
  toast(['Reviewing again soon...','Hard — noted','Good job! +15XP','Easy! +20XP'][r]);
  nextCard();
}

function nextCard() {
  const sub = activeSubjName('fcSubj');
  const cards = getFC(sub);
  fcState.idx = (fcState.idx + 1) % (cards.length || 1);
  loadFC();
}
function prevCard() {
  const sub = activeSubjName('fcSubj');
  const cards = getFC(sub);
  fcState.idx = (fcState.idx - 1 + (cards.length||1)) % (cards.length||1);
  loadFC();
}

// ════════════════════════════════
//  QUIZ
// ════════════════════════════════
let qzState = { n: 5, questions: [], idx: 0, score: 0, answered: false, timerInt: null };

function renderQZSubj() { renderSubjPickers(); }

function setQN(n, el) {
  qzState.n = n;
  document.querySelectorAll('.qz-n-btn').forEach(b => { b.classList.remove('btn-acc'); });
  el.classList.add('btn-acc');
}

function startQuiz() {
  const sub = activeSubjName('qzSubj');
  if (!sub) { toast('📤 Upload a PDF first to unlock quizzes!'); return; }
  const pool = getQZ(sub);
  if (!pool.length) { toast('No quiz questions for "' + sub + '" yet. Upload a PDF and generate study material first!'); return; }
  const shuffled = [...pool].sort(() => Math.random() - .5);
  qzState.questions = shuffled.slice(0, Math.min(qzState.n, shuffled.length));
  qzState.idx = 0; qzState.score = 0; qzState.answered = false;
  document.getElementById('quiz-setup').style.display = 'none';
  document.getElementById('quiz-game').style.display = 'block';
  document.getElementById('quiz-result').style.display = 'none';
  loadQ();
}

let timerVal = 20;
function loadQ() {
  if (qzState.idx >= qzState.questions.length) { showQResult(); return; }
  const q = qzState.questions[qzState.idx];
  qzState.answered = false;
  document.getElementById('q-ctr').textContent = `Q ${qzState.idx+1}/${qzState.questions.length}`;
  document.getElementById('q-score-live').textContent = qzState.score + ' pts';
  document.getElementById('q-text').textContent = q.q;
  document.getElementById('q-exp').style.display = 'none';
  document.getElementById('q-next').style.display = 'none';
  const optsEl = document.getElementById('q-opts');
  optsEl.innerHTML = '';
  q.opts.forEach((o, i) => {
    const btn = document.createElement('button');
    btn.className = 'opt'; btn.textContent = o;
    btn.onclick = () => answerQ(i);
    optsEl.appendChild(btn);
  });
  clearInterval(qzState.timerInt);
  timerVal = 20;
  document.getElementById('timer-bar').style.width = '100%';
  document.getElementById('timer-bar').style.background = 'var(--acc)';
  qzState.timerInt = setInterval(() => {
    timerVal--;
    const pct = Math.round((timerVal/20)*100);
    document.getElementById('timer-bar').style.width = pct + '%';
    document.getElementById('timer-bar').style.background = timerVal > 10 ? 'var(--acc)' : timerVal > 5 ? 'var(--amber)' : 'var(--red)';
    if (timerVal <= 0) { clearInterval(qzState.timerInt); if (!qzState.answered) answerQ(-1); }
  }, 1000);
}

function answerQ(chosen) {
  if (qzState.answered) return;
  qzState.answered = true;
  clearInterval(qzState.timerInt);
  const q = qzState.questions[qzState.idx];
  document.querySelectorAll('.opt').forEach((b, i) => {
    b.disabled = true;
    if (i === q.c) b.classList.add('correct');
    else if (i === chosen && chosen !== q.c) b.classList.add('wrong');
  });
  const correct = chosen === q.c;
  if (correct) { qzState.score += 10; gainXP(20); }
  document.getElementById('q-exp').textContent = '💡 ' + q.e;
  document.getElementById('q-exp').style.display = 'block';
  document.getElementById('q-next').style.display = 'inline-flex';
}

function nextQ() { qzState.idx++; loadQ(); }

function showQResult() {
  document.getElementById('quiz-game').style.display = 'none';
  document.getElementById('quiz-result').style.display = 'block';
  const total = qzState.questions.length;
  const correct = qzState.score / 10;
  const pct = Math.round((correct / total) * 100);
  document.getElementById('res-score').textContent = pct + '%';
  document.getElementById('res-score').style.color = pct >= 80 ? 'var(--green)' : pct >= 60 ? 'var(--amber)' : 'var(--red)';
  document.getElementById('res-lbl').textContent = `${correct}/${total} correct — ${pct >= 80 ? '🎉 Excellent!' : pct >= 60 ? '👍 Good job!' : '📚 Keep practicing!'}`;
  document.getElementById('res-xp').textContent = `+${correct * 20} XP earned`;
  CU.quizzesDone++;
  CU.totalAccuracy = (CU.totalAccuracy || 0) + pct;
  CU.accuracyCount = (CU.accuracyCount || 0) + 1;
  CU.quizHistory = CU.quizHistory || [];
  CU.quizHistory.push({ score: correct, total, subject: activeSubjName('qzSubj'), ts: Date.now() });
  persistUser();
  renderHome();
  renderLB('global');
}

function resetQuiz() {
  document.getElementById('quiz-game').style.display = 'none';
  document.getElementById('quiz-result').style.display = 'none';
  document.getElementById('quiz-setup').style.display = 'block';
}

// ════════════════════════════════
//  LEADERBOARD
// ════════════════════════════════
function renderLB(mode) {
  const lb = document.getElementById('lb-table');
  let users = getAllUsers().filter(u => u.username !== 'admin' && u.email !== '' && !u._demo);

  // Include current user always
  if (CU && !CU.isAdmin) {
    const found = users.find(u => u.username === CU.username);
    if (!found) users.push(CU);
  }

  if (mode === 'weekly') users.sort((a,b) => ((b.weeklyXP||[]).reduce((s,v)=>s+v,0)) - ((a.weeklyXP||[]).reduce((s,v)=>s+v,0)));
  else users.sort((a,b) => (b.xp + (b.level-1)*1000) - (a.xp + (a.level-1)*1000));

  const colors = ['#FFD700','#C0C0C0','#CD7F32'];
  lb.innerHTML = '';
  users.forEach((u, i) => {
    const isMe = CU && u.username === CU.username;
    const acc = u.accuracyCount > 0 ? Math.round(u.totalAccuracy / u.accuracyCount) + '%' : '—';
    const xpTotal = u.xp + (u.level - 1) * 500;
    const row = document.createElement('div');
    row.className = 'lb-row' + (isMe ? ' lb-me' : '');
    row.innerHTML = `
      <div class="lb-rank" style="color:${colors[i]||'var(--muted)'}">${i < 3 ? ['🥇','🥈','🥉'][i] : i+1}</div>
      <div class="lb-avatar" style="background:${stringToColor(u.username)}22;color:${stringToColor(u.username)}">${u.username.slice(0,2).toUpperCase()}</div>
      <div class="lb-info">
        <div class="lb-name">${u.username}${isMe ? ' <span style="font-size:10px;color:var(--acc2);">(you)</span>' : ''}</div>
        <div class="lb-sub">Lv ${u.level} · ${LVL_NAMES[(u.level||1)-1]} · ${u.streak||0}🔥 · ${acc} avg</div>
      </div>
      <div class="lb-xp">${xpTotal.toLocaleString()} XP</div>`;
    lb.appendChild(row);
  });
}

function stringToColor(str) {
  const colors = ['#6c5fff','#22d98a','#f0a500','#ff5fa0','#00d4cc','#3b9eff','#ff4d4d'];
  let hash = 0;
  for (let i = 0; i < str.length; i++) hash = str.charCodeAt(i) + ((hash << 5) - hash);
  return colors[Math.abs(hash) % colors.length];
}

// ════════════════════════════════
//  BATTLE
// ════════════════════════════════
let battleState = { opponent: null, myScore: 0, oppScore: 0, questions: [], idx: 0, total: 5 };

function renderOnlinePlayers() {
  const el = document.getElementById('online-players');
  if (!el) return;
  const users = getAllUsers().filter(u => u.username !== 'admin' && u.email && u.email !== '' && (!CU || u.username !== CU.username)).slice(0,8);
  if (!users.length) {
    el.innerHTML = '<p style="font-size:13px;color:var(--muted);padding:.5rem 0;">No other players yet — share Toutify so your friends can register and appear here!</p>';
    return;
  }
  el.innerHTML = '';
  users.forEach(u => {
    const active = Date.now() - (u.lastSeen||0) < 3600000;
    const div = document.createElement('div');
    div.className = 'player-result';
    div.innerHTML = `
      <div style="position:relative;">
        <div class="lb-avatar" style="width:36px;height:36px;background:${stringToColor(u.username)}22;color:${stringToColor(u.username)};font-size:12px;font-family:var(--fh);font-weight:700;border-radius:50%;display:flex;align-items:center;justify-content:center;">${u.username.slice(0,2).toUpperCase()}</div>
        ${active ? '<div style="position:absolute;bottom:0;right:0;width:9px;height:9px;background:var(--green);border-radius:50%;border:2px solid var(--s1);"></div>' : ''}
      </div>
      <div style="flex:1;">
        <div style="font-size:13px;font-weight:600;">${u.username}</div>
        <div style="font-size:11px;color:var(--muted);">Lv ${u.level||1} · ${u.quizzesDone||0} quizzes · ${active?'<span style="color:var(--green)">online</span>':'offline'}</div>
      </div>
      <button class="btn btn-sm btn-acc" onclick="challengePlayer('${u.username}')">Challenge ⚔️</button>`;
    el.appendChild(div);
  });
}

function searchPlayers() {
  const q = document.getElementById('battle-search-inp').value.trim().toLowerCase();
  const el = document.getElementById('battle-results');
  if (!q) { el.innerHTML = ''; return; }
  const users = getAllUsers().filter(u =>
    u.username !== 'admin' &&
    u.email && u.email !== '' &&
    (!CU || u.username !== CU.username) &&
    u.username.toLowerCase().includes(q)
  );
  el.innerHTML = '';
  if (!users.length) {
    el.innerHTML = '<p style="font-size:13px;color:var(--muted);padding:.5rem 0;">No registered users found with that name.</p>';
    return;
  }
  users.forEach(u => {
    const div = document.createElement('div');
    div.className = 'player-result';
    div.innerHTML = `
      <div class="lb-avatar" style="width:34px;height:34px;background:${stringToColor(u.username)}22;color:${stringToColor(u.username)};font-size:11px;font-family:var(--fh);font-weight:700;border-radius:50%;display:flex;align-items:center;justify-content:center;">${u.username.slice(0,2).toUpperCase()}</div>
      <div style="flex:1;"><div style="font-size:13px;font-weight:600;">${u.username}</div><div style="font-size:11px;color:var(--muted);">Lv ${u.level||1} · ${u.quizzesDone||0} quizzes done</div></div>
      <button class="btn btn-sm btn-acc" onclick="challengePlayer('${u.username}')">Challenge ⚔️</button>`;
    el.appendChild(div);
  });
}

function challengePlayer(username) {
  const opp = getUser(username);
  if (!opp) { toast('Player not found'); return; }

  // Get quiz questions from MY uploaded PDFs
  const mySubjs = getAllUserSubjects();
  // Get quiz questions from OPPONENT's uploaded PDFs (stored in their qzDB)
  const oppQzDB = opp.qzDB || {};
  const oppSubjs = Object.keys(oppQzDB).filter(k => (oppQzDB[k]||[]).length > 0);

  // Find shared subjects (both have uploaded for)
  const shared = mySubjs.filter(s => oppSubjs.includes(s));

  let pool = [];
  let battleSubject = '';

  if (shared.length > 0) {
    // Use questions from a shared subject
    battleSubject = shared[Math.floor(Math.random() * shared.length)];
    const myQs = qzDB[battleSubject] || [];
    const oppQs = oppQzDB[battleSubject] || [];
    // Mix questions from both users
    pool = [...myQs, ...oppQs].sort(() => Math.random() - .5);
  } else if (mySubjs.length > 0) {
    // Fallback: use my uploaded questions
    battleSubject = mySubjs[Math.floor(Math.random() * mySubjs.length)];
    pool = [...(qzDB[battleSubject] || [])].sort(() => Math.random() - .5);
  }

  if (!pool.length) {
    toast('No quiz questions found! Upload a PDF and generate study material first.');
    return;
  }

  battleState.opponent = opp;
  battleState.myScore = 0;
  battleState.oppScore = 0;
  battleState.idx = 0;
  battleState.subject = battleSubject;
  battleState.questions = pool.slice(0, battleState.total);

  document.getElementById('battle-lobby').style.display = 'none';
  document.getElementById('battle-game').style.display = 'block';
  document.getElementById('battle-result').style.display = 'none';

  // Show subject banner
  const subjectBanner = document.createElement('div');
  subjectBanner.style.cssText = 'text-align:center;font-size:12px;color:var(--muted);margin-bottom:10px;font-family:var(--fh);';
  subjectBanner.textContent = shared.length > 0
    ? `⚔️ Battling on shared subject: ${battleSubject}`
    : `⚔️ Battling on: ${battleSubject} (your questions)`;
  const gameEl = document.getElementById('battle-game');
  const existing = gameEl.querySelector('.battle-banner');
  if (existing) existing.remove();
  subjectBanner.className = 'battle-banner';
  gameEl.insertBefore(subjectBanner, gameEl.firstChild);

  renderBattleArena();
  loadBattleQ();
}

function renderBattleArena() {
  const opp = battleState.opponent;
  const myPct = Math.round((battleState.myScore / battleState.total) * 100);
  const oppPct = Math.round((battleState.oppScore / battleState.total) * 100);
  document.getElementById('battle-arena').innerHTML = `
    <div class="battle-player">
      <div style="font-family:var(--fh);font-size:13px;font-weight:700;margin-bottom:8px;">${CU.username}</div>
      <div class="battle-score" style="color:var(--acc)">${battleState.myScore}</div>
      <div class="battle-prog"><div style="height:100%;border-radius:999px;background:var(--acc);width:${myPct}%;transition:width .3s;"></div></div>
    </div>
    <div class="battle-vs">VS</div>
    <div class="battle-player">
      <div style="font-family:var(--fh);font-size:13px;font-weight:700;margin-bottom:8px;">${opp.username}</div>
      <div class="battle-score" style="color:var(--pink)">${battleState.oppScore}</div>
      <div class="battle-prog"><div style="height:100%;border-radius:999px;background:var(--pink);width:${oppPct}%;transition:width .3s;"></div></div>
    </div>`;
}

function loadBattleQ() {
  if (battleState.idx >= battleState.questions.length) { showBattleResult(); return; }
  const q = battleState.questions[battleState.idx];
  const el = document.getElementById('battle-q-area');
  el.innerHTML = `
    <div class="q-card">${q.q}</div>
    <div class="opts" id="battle-opts"></div>`;
  const optsEl = document.getElementById('battle-opts');
  q.opts.forEach((o, i) => {
    const btn = document.createElement('button');
    btn.className = 'opt'; btn.textContent = o;
    btn.onclick = () => answerBattle(i);
    optsEl.appendChild(btn);
  });
}

function answerBattle(chosen) {
  const q = battleState.questions[battleState.idx];
  const correct = chosen === q.c;
  document.querySelectorAll('#battle-opts .opt').forEach((b, i) => {
    b.disabled = true;
    if (i === q.c) b.classList.add('correct');
    else if (i === chosen && !correct) b.classList.add('wrong');
  });
  if (correct) { battleState.myScore++; gainXP(15); }
  // Simulate opponent: 60% chance to get it right
  if (Math.random() < 0.6) battleState.oppScore++;
  renderBattleArena();
  setTimeout(() => { battleState.idx++; loadBattleQ(); }, 1000);
}

function showBattleResult() {
  document.getElementById('battle-game').style.display = 'none';
  document.getElementById('battle-result').style.display = 'block';
  const win = battleState.myScore > battleState.oppScore;
  const tie = battleState.myScore === battleState.oppScore;
  const xpGain = win ? 100 : tie ? 50 : 25;
  gainXP(xpGain);
  document.getElementById('battle-res-content').innerHTML = `
    <div style="font-size:52px;margin-bottom:8px;">${win ? '🏆' : tie ? '🤝' : '😤'}</div>
    <div style="font-family:var(--fh);font-size:28px;font-weight:800;color:${win?'var(--green)':tie?'var(--amber)':'var(--red)'};">${win ? 'Victory!' : tie ? 'Tie!' : 'Defeat'}</div>
    <p style="color:var(--muted);margin:8px 0;font-size:14px;">${CU.username}: ${battleState.myScore} · ${battleState.opponent.username}: ${battleState.oppScore}</p>
    <p style="color:var(--acc2);font-size:13px;">+${xpGain} XP earned</p>`;
}

function resetBattle() {
  battleState = { opponent: null, myScore: 0, oppScore: 0, questions: [], idx: 0, total: 5 };
  document.getElementById('battle-lobby').style.display = 'block';
  document.getElementById('battle-game').style.display = 'none';
  document.getElementById('battle-result').style.display = 'none';
  document.getElementById('battle-search-inp').value = '';
  document.getElementById('battle-results').innerHTML = '';
  renderOnlinePlayers();
}

// ════════════════════════════════
//  AI TUTOR
// ════════════════════════════════
let chatHistory = [];

function renderQuickQs() {
  const sub = activeSubjName('tutorSubj');
  const qs = {
    "Biochemistry":["Explain the Krebs cycle","What is enzyme inhibition?","How does DNA replication work?","Summarize glycolysis"],
    "Physics":["Explain Newton's laws","What is quantum mechanics?","How do electromagnetic waves work?","Explain entropy"],
    "History":["Key causes of WWI","French Revolution summary","What was the Cold War?","Effects of colonialism"],
    "Mathematics":["Explain derivatives simply","What is a limit?","How to integrate by parts?","What is Euler's identity?"],
  };
  const el = document.getElementById('quick-qs');
  if (!el) return;
  const list = qs[sub] || [`Ask me anything about ${sub}`];
  el.innerHTML = '';
  list.forEach(q => {
    const btn = document.createElement('button');
    btn.className = 'btn btn-xs';
    btn.style.fontSize = '11px';
    btn.textContent = q;
    btn.onclick = () => { document.getElementById('chat-inp').value = q; sendChat(); };
    el.appendChild(btn);
  });
}

async function sendChat() {
  const inp = document.getElementById('chat-inp');
  const msg = inp.value.trim();
  if (!msg) return;
  inp.value = '';
  const sub = activeSubjName('tutorSubj') || 'general study topics';
  const uploadedCards = getFC(sub);
  const ctx = uploadedCards.length
    ? '\n\nContext from student notes on "' + sub + '":\n' + uploadedCards.slice(0,4).map(c=>`Q: ${c.q} → A: ${c.a}`).join('\n')
    : '';
  appendMsg('user', msg);
  chatHistory.push({ role:'user', content: msg });
  const tid = appendTyping();
  document.getElementById('chat-send').disabled = true;
  try {
    const sysPrompt = `You are Toutify, a friendly study tutor for "${sub}". Help students understand their material clearly. Keep answers under 150 words. Use bullet points when listing. Be warm and encouraging.${ctx}`;
    const historyStr = chatHistory.slice(-6).map(m => m.role.toUpperCase() + ': ' + m.content).join('\n');
    const reply = await callAI(sysPrompt, historyStr, 400);
    removeTyping(tid);
    chatHistory.push({ role:'assistant', content: reply });
    appendMsg('ai', reply);
    gainXP(5);
  } catch(e) {
    removeTyping(tid);
    appendMsg('ai', '⚠️ ' + e.message);
  }
  document.getElementById('chat-send').disabled = false;
}

function appendMsg(role, text) {
  const box = document.getElementById('chat-box');
  const div = document.createElement('div');
  div.className = `msg msg-${role}`;
  div.innerHTML = `<div class="msg-av">${role==='ai'?'T':'U'}</div><div class="msg-bub">${text.replace(/\n/g,'<br/>')}</div>`;
  box.appendChild(div);
  box.scrollTop = box.scrollHeight;
}

function appendTyping() {
  const box = document.getElementById('chat-box');
  const id = 'td-' + Date.now();
  const div = document.createElement('div');
  div.className = 'msg msg-ai'; div.id = id;
  div.innerHTML = `<div class="msg-av">T</div><div class="msg-bub"><div class="typing-dots"><div class="tdot"></div><div class="tdot"></div><div class="tdot"></div></div></div>`;
  box.appendChild(div);
  box.scrollTop = box.scrollHeight;
  return id;
}
function removeTyping(id) { const el = document.getElementById(id); if(el) el.remove(); }

// ════════════════════════════════
//  CONCEPT MAPS
// ════════════════════════════════
let mapState = { subj: 0, topic: 0 };

function renderMapTopics() {
  const el = document.getElementById('map-topic-pick');
  if (!el) return;
  const subjs = getAllUserSubjects();
  el.innerHTML = '';
  if (!subjs.length) return;
  subjs.forEach((s, i) => {
    const btn = document.createElement('button');
    btn.className = 'btn btn-sm' + (i === (subjState.mapSubj||0) ? ' btn-acc' : '');
    btn.textContent = s;
    btn.onclick = () => { subjState.mapSubj = i; renderMapTopics(); drawMap(); };
    el.appendChild(btn);
  });
}

function drawMap() {
  const canvas = document.getElementById('map-canvas');
  if (!canvas) return;
  const subjs = getAllUserSubjects();
  if (!subjs.length) {
    canvas.innerHTML = '<p style="padding:2rem;color:var(--muted);text-align:center;font-size:14px;">📤 Upload a PDF first — your concept map will be generated from your study material.</p>';
    return;
  }
  const sub = subjs[subjState.mapSubj || 0];
  const cards = getFC(sub);
  if (!cards.length) {
    canvas.innerHTML = '<p style="padding:2rem;color:var(--muted);text-align:center;">No cards for this subject yet.</p>';
    return;
  }
  canvas.innerHTML = '';
  const w = canvas.clientWidth || 600;
  const h = canvas.clientHeight || 360;
  const cx = Math.round(w / 2), cy = Math.round(h / 2 - 10);

  // Build nodes from card questions (up to 8)
  const nodeCards = cards.slice(0, 8);
  const angleStep = (2 * Math.PI) / nodeCards.length;
  const radius = Math.min(w, h) * 0.34;

  const svg = document.createElementNS('http://www.w3.org/2000/svg','svg');
  svg.className = 'map-svg-layer';
  svg.setAttribute('viewBox', `0 0 ${w} ${h}`);

  nodeCards.forEach((card, i) => {
    const angle = i * angleStep - Math.PI / 2;
    const nx = cx + Math.round(radius * Math.cos(angle));
    const ny = cy + Math.round(radius * Math.sin(angle));
    const line = document.createElementNS('http://www.w3.org/2000/svg','line');
    line.setAttribute('x1', cx); line.setAttribute('y1', cy);
    line.setAttribute('x2', nx); line.setAttribute('y2', ny);
    line.setAttribute('stroke','rgba(255,255,255,0.1)');
    line.setAttribute('stroke-width','1.5');
    svg.appendChild(line);
  });
  canvas.appendChild(svg);

  // Center node
  const cNode = document.createElement('div');
  cNode.className = 'mnode center';
  const cLabel = sub.length > 16 ? sub.slice(0,14) + '…' : sub;
  cNode.style.cssText = `left:${cx - 55}px;top:${cy - 18}px;`;
  cNode.textContent = cLabel;
  canvas.appendChild(cNode);

  // Surrounding nodes
  nodeCards.forEach((card, i) => {
    const angle = i * angleStep - Math.PI / 2;
    const nx = cx + Math.round(radius * Math.cos(angle));
    const ny = cy + Math.round(radius * Math.sin(angle));
    const node = document.createElement('div');
    node.className = 'mnode leaf';
    // Trim long labels
    const short = card.q.length > 28 ? card.q.slice(0, 26) + '…' : card.q;
    node.textContent = short;
    node.style.cssText = `left:${nx - 55}px;top:${ny - 14}px;max-width:120px;white-space:normal;text-align:center;line-height:1.3;font-size:11px;`;
    node.title = card.q + '\n→ ' + card.a;
    node.onclick = () => {
      nav('tutor');
      document.getElementById('chat-inp').value = `Explain: ${card.q}`;
      sendChat();
    };
    canvas.appendChild(node);
  });
}

// ════════════════════════════════
//  STUDY MODES
// ════════════════════════════════
let currentMode = null;
let pomoState = { running:false, phase:'focus', session:1, timeLeft:25*60, interval:null };
let dwState = { duration:30, interval:null, start:0 };
let sprintState = { interval:null, timeLeft:60, score:0, subj:'Biochemistry' };

function openMode(id) {
  document.getElementById('study-home').style.display = 'none';
  document.querySelectorAll('[id^="mode-"]').forEach(el => el.style.display = 'none');
  document.getElementById('mode-'+id).style.display = 'block';
  currentMode = id;
  if (id === 'spaced') renderSpacedCards();
  if (id === 'sprint') renderSprintSubj();
  if (id === 'blurting') renderBlurtSubj();
}

function closeMode() {
  document.querySelectorAll('[id^="mode-"]').forEach(el => el.style.display = 'none');
  document.getElementById('study-home').style.display = 'block';
  clearInterval(pomoState.interval);
  clearInterval(dwState.interval);
  clearInterval(sprintState.interval);
  currentMode = null;
}

// POMODORO
const POMO_PHASES = [{name:'FOCUS',mins:25},{name:'BREAK',mins:5},{name:'FOCUS',mins:25},{name:'BREAK',mins:5},{name:'FOCUS',mins:25},{name:'BREAK',mins:5},{name:'FOCUS',mins:25},{name:'LONG BREAK',mins:15}];
let pomoPhaseIdx = 0;

function resetPomo() {
  clearInterval(pomoState.interval);
  pomoState = {running:false,phase:'focus',session:1,timeLeft:25*60,interval:null};
  pomoPhaseIdx = 0;
  updatePomoUI();
  document.getElementById('pomo-start-btn').textContent = 'Start';
  document.getElementById('pomo-log').innerHTML = '';
}

function togglePomo() {
  if (pomoState.running) {
    clearInterval(pomoState.interval);
    pomoState.running = false;
    document.getElementById('pomo-start-btn').textContent = 'Resume';
  } else {
    pomoState.running = true;
    document.getElementById('pomo-start-btn').textContent = 'Pause';
    pomoState.interval = setInterval(() => {
      pomoState.timeLeft--;
      if (pomoState.timeLeft <= 0) {
        const phase = POMO_PHASES[pomoPhaseIdx];
        const log = document.getElementById('pomo-log');
        log.innerHTML += `<div style="margin-bottom:4px;">✓ ${phase.name} session complete</div>`;
        if (phase.name === 'FOCUS') { gainXP(30); }
        pomoPhaseIdx = (pomoPhaseIdx + 1) % POMO_PHASES.length;
        const next = POMO_PHASES[pomoPhaseIdx];
        pomoState.timeLeft = next.mins * 60;
        pomoState.session = Math.floor(pomoPhaseIdx / 2) + 1;
      }
      updatePomoUI();
    }, 1000);
  }
}

function updatePomoUI() {
  const phase = POMO_PHASES[pomoPhaseIdx];
  const m = Math.floor(pomoState.timeLeft / 60).toString().padStart(2,'0');
  const s = (pomoState.timeLeft % 60).toString().padStart(2,'0');
  document.getElementById('pomo-time').textContent = `${m}:${s}`;
  document.getElementById('pomo-phase').textContent = phase.name;
  document.getElementById('pomo-session').textContent = `Session ${Math.floor(pomoPhaseIdx/2)+1} of 4`;
  const totalSecs = phase.mins * 60;
  const prog = (pomoState.timeLeft / totalSecs);
  const circ = 2 * Math.PI * 80;
  const offset = circ * (1 - prog);
  const circle = document.getElementById('pomo-circle');
  if (circle) {
    circle.setAttribute('stroke-dasharray', circ);
    circle.setAttribute('stroke-dashoffset', offset);
    circle.setAttribute('stroke', phase.name === 'FOCUS' ? 'var(--acc)' : 'var(--green)');
  }
}

// BLURTING
function renderBlurtSubj() {
  const el = document.getElementById('blurt-subj');
  if (!el) return;
  const subjs = getAllUserSubjects();
  el.innerHTML = '';
  if (!subjs.length) {
    el.innerHTML = '<span style="font-size:12px;color:var(--muted);">Upload a PDF first to use this mode</span>';
    return;
  }
  subjs.forEach((s,i) => {
    const btn = document.createElement('button');
    btn.className = 'btn btn-sm' + (i===0?' btn-acc':'');
    btn.textContent = s;
    btn.onclick = () => {
      document.querySelectorAll('#blurt-subj .btn').forEach(b=>b.classList.remove('btn-acc'));
      btn.classList.add('btn-acc');
    };
    el.appendChild(btn);
  });
}

async function checkBlurt() {
  const text = document.getElementById('blurt-input').value.trim();
  const activeBtn = document.querySelector('#blurt-subj .btn-acc');
  const sub = activeBtn ? activeBtn.textContent.trim() : (getAllUserSubjects()[0] || 'your subject');
  if (!text || text.length < 20) { toast('Write at least a sentence before checking!'); return; }
  document.getElementById('blurt-result').style.display = 'none';
  const cards = getFC(sub);
  const cardCtx = cards.length ? '\nReference from uploaded notes:\n' + cards.slice(0,6).map(c=>`- ${c.q}: ${c.a}`).join('\n') : '';
  const checkBtn = document.querySelector('#mode-blurting .btn-acc');
  if (checkBtn) { checkBtn.disabled = true; checkBtn.innerHTML = '<span class="spin"></span> Checking...'; }
  try {
    const reply = await callAI(
      `You are a study coach evaluating a blurting attempt on "${sub}".${cardCtx}\nFeedback format:\n✅ Got right: ...\n❌ Missed: ...\n💡 Tip: ...\nBe encouraging and specific. Under 150 words.`,
      `My blurt about ${sub}:\n\n${text}`
    );
    document.getElementById('blurt-feedback').innerHTML = reply.replace(/\n/g,'<br/>');
    document.getElementById('blurt-result').style.display = 'block';
    gainXP(25);
  } catch(e) { toast('Error: ' + e.message); }
  if (checkBtn) { checkBtn.disabled = false; checkBtn.textContent = 'Check my knowledge →'; }
}

// FEYNMAN
async function checkFeynman() {
  const topic = document.getElementById('feynman-topic').value.trim();
  const explanation = document.getElementById('feynman-input').value.trim();
  if (!topic) { toast('Enter a topic first'); return; }
  if (!explanation || explanation.length < 20) { toast('Write your explanation first'); return; }
  document.getElementById('feynman-result').style.display = 'none';
  const analyzeBtn = document.querySelector('#mode-feynman .btn-acc');
  if (analyzeBtn) { analyzeBtn.disabled = true; analyzeBtn.innerHTML = '<span class="spin"></span> Analyzing...'; }
  try {
    const reply = await callAI(
      `You are a Feynman method coach. Evaluate the student's simple explanation of "${topic}".\n🎯 Simplicity: is it actually simple?\n✅ Accuracy: any errors?\n❓ Gaps: what's missing?\n💡 One improvement tip.\nBe warm and constructive. Under 150 words.`,
      `My simple explanation of "${topic}":\n\n${explanation}`
    );
    document.getElementById('feynman-feedback').innerHTML = reply.replace(/\n/g,'<br/>');
    document.getElementById('feynman-result').style.display = 'block';
    gainXP(25);
  } catch(e) { toast('Error: ' + e.message); }
  if (analyzeBtn) { analyzeBtn.disabled = false; analyzeBtn.textContent = 'Analyze my explanation →'; }
}

// SPEED SPRINT
let sprintSubjName = 'Biochemistry';

function renderSprintSubj() {
  const el = document.getElementById('sprint-subj');
  if (!el) return;
  const subjs = getAllUserSubjects();
  el.innerHTML = '';
  if (!subjs.length) {
    el.innerHTML = '<span style="font-size:12px;color:var(--muted);">Upload a PDF first to unlock Sprint mode</span>';
    return;
  }
  subjs.forEach((s,i) => {
    const btn = document.createElement('button');
    btn.className = 'btn btn-sm' + (i===0?' btn-acc':'');
    btn.textContent = s;
    btn.onclick = () => {
      document.querySelectorAll('#sprint-subj .btn').forEach(b=>b.classList.remove('btn-acc'));
      btn.classList.add('btn-acc');
      sprintSubjName = s;
    };
    el.appendChild(btn);
  });
  sprintSubjName = subjs[0] || '';
}

let sprintPool = [], sprintIdx = 0, sprintCorrect = 0, sprintTimerVal = 60;

function startSprint() {
  const pool = getQZ(sprintSubjName);
  if (!pool.length) { toast('No questions for this subject!'); return; }
  sprintPool = [...pool].sort(()=>Math.random()-.5);
  sprintIdx = 0; sprintCorrect = 0; sprintTimerVal = 60;
  document.getElementById('sprint-setup').style.display = 'none';
  document.getElementById('sprint-result').style.display = 'none';
  document.getElementById('sprint-game').style.display = 'block';
  document.getElementById('sprint-timer').textContent = '60';
  document.getElementById('sprint-score').textContent = '0 correct';
  document.getElementById('sprint-bar').style.width = '100%';
  clearInterval(sprintState.interval);
  sprintState.interval = setInterval(() => {
    sprintTimerVal--;
    document.getElementById('sprint-timer').textContent = sprintTimerVal;
    const pct = Math.round((sprintTimerVal/60)*100);
    document.getElementById('sprint-bar').style.width = pct+'%';
    document.getElementById('sprint-bar').style.background = sprintTimerVal > 20 ? 'var(--acc)' : 'var(--red)';
    if (sprintTimerVal <= 0) {
      clearInterval(sprintState.interval);
      document.getElementById('sprint-game').style.display = 'none';
      document.getElementById('sprint-result').style.display = 'block';
      document.getElementById('sprint-final').textContent = sprintCorrect;
      gainXP(sprintCorrect * 5);
      toast(`Sprint done! ${sprintCorrect} correct · +${sprintCorrect*5} XP`);
    }
  }, 1000);
  loadSprintQ();
}

function loadSprintQ() {
  const q = sprintPool[sprintIdx % sprintPool.length];
  document.getElementById('sprint-q').textContent = q.q;
  const el = document.getElementById('sprint-opts');
  el.innerHTML = '';
  q.opts.forEach((o,i) => {
    const btn = document.createElement('button');
    btn.className = 'opt'; btn.textContent = o;
    btn.onclick = () => {
      if (i === q.c) { sprintCorrect++; document.getElementById('sprint-score').textContent = sprintCorrect + ' correct'; }
      sprintIdx++;
      loadSprintQ();
    };
    el.appendChild(btn);
  });
}

// DEEP WORK
let dwDuration = 30;
function setDW(m, el) {
  dwDuration = m;
  document.querySelectorAll('.dw-dur').forEach(b => b.classList.remove('btn-acc'));
  el.classList.add('btn-acc');
}

function startDW() {
  const intention = document.getElementById('dw-intention').value.trim() || 'Deep work session';
  document.getElementById('dw-intention-display').textContent = '🎯 ' + intention;
  document.getElementById('dw-active').style.display = 'block';
  dwState.start = Date.now();
  dwState.total = dwDuration * 60;
  clearInterval(dwState.interval);
  dwState.interval = setInterval(() => {
    const elapsed = Math.floor((Date.now() - dwState.start) / 1000);
    const left = Math.max(0, dwState.total - elapsed);
    const m = Math.floor(left/60).toString().padStart(2,'0');
    const s = (left%60).toString().padStart(2,'0');
    document.getElementById('dw-timer').textContent = `${m}:${s}`;
    const pct = Math.round((left/dwState.total)*100);
    document.getElementById('dw-bar').style.width = pct + '%';
    if (left <= 0) { clearInterval(dwState.interval); gainXP(60); toast('Deep work session complete! +60 XP 🧘'); }
  }, 1000);
}

function endDW() {
  clearInterval(dwState.interval);
  document.getElementById('dw-active').style.display = 'none';
  const elapsed = Math.floor((Date.now() - dwState.start) / 1000);
  const xp = Math.round((elapsed / dwState.total) * 60);
  gainXP(xp);
  toast(`Session ended. +${xp} XP earned`);
}

// SPACED REP
function renderSpacedCards() {
  const el = document.getElementById('spaced-cards');
  if (!el) return;
  const sub = activeSubjName('fcSubj');
  const cards = getFC(sub).slice(0, 5);
  el.innerHTML = '';
  if (!cards.length) { el.innerHTML = '<p style="font-size:13px;color:var(--muted);">No cards yet for this subject.</p>'; return; }
  cards.forEach(c => {
    const div = document.createElement('div');
    div.className = 'card2';
    div.style.marginBottom = '8px';
    div.innerHTML = `<div style="font-size:13px;font-weight:500;margin-bottom:4px;">${c.q}</div><div style="font-size:12px;color:var(--muted);">${c.a}</div>`;
    el.appendChild(div);
  });
}

// ════════════════════════════════
//  UPLOAD
// ════════════════════════════════
let genCards = [];
let genQuizQ = [];

function handleDrop(e) {
  e.preventDefault();
  document.getElementById('pdf-drop').classList.remove('drag');
  const file = e.dataTransfer.files[0];
  if (file && file.type === 'application/pdf') processPDFFile(file);
  else toast('Please drop a PDF file.');
}

function handlePDF(e) {
  const file = e.target.files[0];
  if (file) processPDFFile(file);
}

async function loadPDFJS() {
  if (window.pdfjsLib) return true;
  const versions = ['3.4.120','2.16.105','2.14.305'];
  for (const ver of versions) {
    try {
      await new Promise((res, rej) => {
        const s = document.createElement('script');
        s.src = `https://cdnjs.cloudflare.com/ajax/libs/pdf.js/${ver}/pdf.min.js`;
        s.onload = res; s.onerror = rej;
        document.head.appendChild(s);
      });
      if (window.pdfjsLib) {
        // Disable worker to avoid CORS issues with local files
        window.pdfjsLib.GlobalWorkerOptions.workerSrc = '';
        window.pdfjsLib.GlobalWorkerOptions.disableWorker = true;
        return true;
      }
    } catch(e) { continue; }
  }
  return false;
}

async function processPDFFile(file) {
  const nameEl = document.getElementById('pdf-name');
  const textEl = document.getElementById('notes-txt');
  nameEl.textContent = `📄 Reading ${file.name}...`;
  nameEl.style.color = 'var(--muted)';
  toast('Reading PDF — please wait...');

  try {
    const loaded = await loadPDFJS();
    if (!loaded) throw new Error('PDF.js library could not be loaded. Check your internet connection.');

    const arrayBuffer = await file.arrayBuffer();
    const pdf = await window.pdfjsLib.getDocument({
      data: arrayBuffer,
      disableWorker: true,
      disableRange: true,
      disableStream: true,
    }).promise;

    const totalPages = pdf.numPages;
    const maxPages = Math.min(totalPages, 20); // read up to 20 pages
    let pages = [];

    for (let i = 1; i <= maxPages; i++) {
      nameEl.textContent = `📄 Reading page ${i}/${maxPages}...`;
      const page = await pdf.getPage(i);
      const textContent = await page.getTextContent({ normalizeWhitespace: true });

      // Reconstruct text with proper spacing by tracking x/y positions
      let lastY = null;
      let pageText = '';
      for (const item of textContent.items) {
        if (!item.str) continue;
        const y = item.transform ? Math.round(item.transform[5]) : 0;
        // New line if Y position changed significantly
        if (lastY !== null && Math.abs(y - lastY) > 5) {
          pageText += '\n';
        } else if (pageText && !pageText.endsWith(' ') && !item.str.startsWith(' ')) {
          pageText += ' ';
        }
        pageText += item.str;
        lastY = y;
      }
      pages.push(pageText.trim());
    }

    // Join pages with clear separators
    let fullText = pages
      .filter(p => p.length > 0)
      .join('\n\n--- Page Break ---\n\n');

    // Clean up common PDF artifacts
    fullText = fullText
      .replace(/([a-z])([A-Z])/g, '$1 $2')   // fix merged words like "theKrebs" -> "the Krebs"
      .replace(/[ \t]{2,}/g, ' ')             // collapse multiple spaces
      .replace(/\n{3,}/g, '\n\n')            // max 2 newlines
      .trim();

    if (!fullText || fullText.length < 50) {
      textEl.value = `This appears to be a scanned/image PDF: "${file.name}". The document has no readable text layer. Please generate study material based on what the subject is likely about from the filename.`;
      nameEl.textContent = `⚠️ ${file.name} — scanned PDF (${totalPages} pages, no text layer)`;
      nameEl.style.color = 'var(--amber)';
      toast('⚠️ Scanned PDF — no text could be extracted. You can still generate from the filename.');
    } else {
      // Trim to fit — keep first 6000 chars for best AI results
      const trimmed = fullText.length > 6000 ? fullText.slice(0, 6000) + '\n[... truncated]' : fullText;
      textEl.value = trimmed;
      nameEl.textContent = `✅ ${file.name} — ${totalPages} pages, ${fullText.length.toLocaleString()} chars read`;
      nameEl.style.color = 'var(--green)';
      toast(`✅ PDF read! ${maxPages}/${totalPages} pages extracted. Select a subject and click Generate.`);
    }
  } catch (err) {
    console.error('PDF error:', err);
    textEl.value = `PDF: "${file.name}"\nCould not extract text automatically. Please paste the content manually in this box, then click Generate.`;
    nameEl.textContent = `❌ ${file.name} — ${err.message}`;
    nameEl.style.color = 'var(--red)';
    toast('PDF read failed — paste your notes manually in the text box instead.');
  }
}

function handleYT() {
  const url = document.getElementById('yt-url').value.trim();
  if (!url || !url.includes('youtu')) { toast('Please enter a valid YouTube URL'); return; }
  const videoId = url.match(/[?&]v=([^&]+)/)?.[1] || url.match(/youtu\.be\/([^?]+)/)?.[1] || url.match(/embed\/([^?]+)/)?.[1];
  if (videoId) {
    document.getElementById('notes-txt').value = `[YouTube video: ${videoId}]\nURL: ${url}\nPlease generate comprehensive university-level flashcards and quiz questions about the key concepts that would typically be covered in a lecture video with this URL. Infer the subject matter from the video ID and URL context.`;
    toast('YouTube video linked! Click Generate to create study material.');
  } else {
    toast('Could not parse video ID from URL.');
  }
}

async function generateNotes() {
  const text = document.getElementById('notes-txt').value.trim();
  const subInput = document.getElementById('upload-subj-name');
  const sub = subInput ? subInput.value.trim() : '';

  if (!sub) { toast('Enter a subject name in Step 1 first!'); subInput && subInput.focus(); return; }
  if (!text || text.length < 20) { toast('Add some content in Step 2 first!'); return; }

  const btn = document.getElementById('gen-btn');
  btn.disabled = true;
  btn.innerHTML = '<span class="spin"></span> Generating…';

  try {
    const raw = await callAI(
      `You are a study material generator. Generate flashcards and quiz questions from the content provided.
IMPORTANT: Output ONLY valid JSON. No markdown, no code blocks, no explanation. Start your response with { and end with }.
Format:
{"flashcards":[{"q":"question text","a":"answer text"}],"quiz":[{"q":"question text","opts":["option A","option B","option C","option D"],"c":0,"e":"brief explanation"}]}
Rules:
- Generate exactly 6 flashcards and 4 quiz questions
- "c" is the index (0, 1, 2, or 3) of the correct option
- Make questions specific and educational, not generic
- Base everything on the provided content about "${sub}"`,
      `Generate study material for the subject "${sub}" from this content:\n\n${text.slice(0, 4000)}`,
      2000
    );

    // Very robust JSON extraction — handles markdown fences, extra text, etc.
    let parsed = null;
    const attempts = [
      () => JSON.parse(raw),
      () => JSON.parse(raw.replace(/```json|```/g, '').trim()),
      () => { const m = raw.match(/\{[\s\S]*\}/); return m ? JSON.parse(m[0]) : null; },
      () => { const m = raw.match(/\{[\s\S]*"flashcards"[\s\S]*\}/); return m ? JSON.parse(m[0]) : null; },
    ];
    for (const attempt of attempts) {
      try { parsed = attempt(); if (parsed) break; } catch(e) {}
    }
    if (!parsed) throw new Error('Could not parse AI response. Try again.');

    genCards = (parsed.flashcards || []).map(c => ({ q: c.q, a: c.a, subject: sub }));
    genQuizQ = (parsed.quiz || []).map(q => ({ q: q.q, opts: q.opts, c: Number(q.c), e: q.e, subject: sub }));

    if (!genCards.length && !genQuizQ.length) throw new Error('AI returned no content. Try with more text.');

    // Auto-create subject if it doesn't exist yet
    if (!CU.subjects.find(s => s.name === sub)) {
      const colors = ['#6c5fff','#22d98a','#f0a500','#00d4cc','#ff5fa0','#3b9eff','#ff4d4d'];
      const icons = ['📖','🔬','⚡','📜','∑','🌍','💊','🧪','📐'];
      CU.subjects.push({
        name: sub,
        icon: icons[CU.subjects.length % icons.length],
        color: colors[CU.subjects.length % colors.length],
        progress: 0, cards: 0, quizzes: 0
      });
    }

    renderGenCards();
    gainXP(30);
    document.getElementById('gen-result-title').textContent =
      `Generated for "${sub}" — ${genCards.length} flashcards + ${genQuizQ.length} quiz questions`;
    toast(`✅ Generated ${genCards.length} flashcards + ${genQuizQ.length} quiz Qs for "${sub}"! +30 XP`);

  } catch(e) {
    console.error('Generate error:', e);
    toast('❌ ' + e.message);
  }

  btn.disabled = false;
  btn.innerHTML = '✨ Generate flashcards & quiz';
}

function renderGenCards() {
  const el = document.getElementById('gen-cards');
  el.innerHTML = '';

  if (genCards.length) {
    const fcHead = document.createElement('div');
    fcHead.style.cssText = 'font-family:var(--fh);font-size:12px;font-weight:700;color:var(--acc2);margin-bottom:8px;letter-spacing:.04em;';
    fcHead.textContent = `🃏 ${genCards.length} FLASHCARDS`;
    el.appendChild(fcHead);

    genCards.forEach((c, i) => {
      const div = document.createElement('div');
      div.className = 'gen-item';
      div.style.cssText = 'flex-direction:column;gap:6px;align-items:flex-start;';
      div.innerHTML = `
        <div style="font-size:13px;font-weight:500;color:var(--text);">Q${i+1}: ${c.q}</div>
        <div class="reveal-wrap" style="width:100%;">
          <button class="btn btn-xs" style="font-size:11px;" onclick="revealAnswer(this)">👁 Reveal answer</button>
          <div class="reveal-ans" style="display:none;font-size:12px;color:var(--green);padding:6px 10px;background:rgba(34,217,138,0.08);border-radius:6px;border-left:3px solid var(--green);margin-top:4px;">
            ${c.a}
          </div>
        </div>`;
      el.appendChild(div);
    });
  }

  if (genQuizQ.length) {
    const sep = document.createElement('div');
    sep.style.cssText = 'font-family:var(--fh);font-size:12px;font-weight:700;color:var(--acc2);margin:1rem 0 8px;letter-spacing:.04em;';
    sep.textContent = `📝 ${genQuizQ.length} QUIZ QUESTIONS`;
    el.appendChild(sep);

    genQuizQ.forEach((q, i) => {
      const div = document.createElement('div');
      div.className = 'gen-item';
      div.style.cssText = 'flex-direction:column;gap:6px;align-items:flex-start;';
      div.innerHTML = `
        <div style="font-size:13px;font-weight:500;color:var(--text);">Q${i+1}: ${q.q}</div>
        <div style="display:flex;flex-wrap:wrap;gap:5px;">
          ${q.opts.map((opt, j) => `
            <span style="font-size:11px;padding:3px 8px;border-radius:5px;border:1px solid var(--border2);color:var(--muted);">
              ${String.fromCharCode(65+j)}) ${opt}
            </span>`).join('')}
        </div>
        <div class="reveal-wrap" style="width:100%;">
          <button class="btn btn-xs" style="font-size:11px;" onclick="revealAnswer(this)">👁 Reveal answer</button>
          <div class="reveal-ans" style="display:none;font-size:12px;color:var(--green);padding:6px 10px;background:rgba(34,217,138,0.08);border-radius:6px;border-left:3px solid var(--green);margin-top:4px;">
            ✅ ${q.opts[q.c]} &nbsp;·&nbsp; <span style="color:var(--muted);">${q.e}</span>
          </div>
        </div>`;
      el.appendChild(div);
    });
  }

  // Subject links at bottom
  const sub = genCards[0]?.subject || genQuizQ[0]?.subject || '';
  if (sub) {
    const links = document.createElement('div');
    links.style.cssText = 'margin-top:1rem;padding-top:1rem;border-top:1px solid var(--border);display:flex;gap:8px;flex-wrap:wrap;align-items:center;';
    links.innerHTML = `
      <span style="font-size:12px;color:var(--muted);">After saving, study with:</span>
      <button class="btn btn-xs btn-acc" onclick="addGenCards();nav('flashcards')">🃏 Flashcards</button>
      <button class="btn btn-xs" onclick="addGenCards();nav('quiz')">📝 Quiz</button>
      <button class="btn btn-xs" onclick="addGenCards();nav('maps')">🗺️ Map</button>`;
    el.appendChild(links);
  }

  document.getElementById('upload-results').style.display = 'block';
}

function revealAnswer(btn) {
  const wrap = btn.parentElement;
  const ans = wrap.querySelector('.reveal-ans');
  if (ans.style.display === 'none') {
    ans.style.display = 'block';
    btn.textContent = '🙈 Hide answer';
  } else {
    ans.style.display = 'none';
    btn.textContent = '👁 Reveal answer';
  }
}

function addGenCards() {
  if (!genCards.length && !genQuizQ.length) { toast('Nothing to add — generate first.'); return; }
  const sub = genCards[0]?.subject || genQuizQ[0]?.subject || '';
  if (!sub) { toast('Subject missing — regenerate.'); return; }

  CU.extraCards = CU.extraCards || [];
  CU.extraCards.push(...genCards);

  if (!qzDB[sub]) qzDB[sub] = [];
  qzDB[sub].push(...genQuizQ.map(q => ({ q: q.q, opts: q.opts, c: q.c, e: q.e })));

  let subjObj = CU.subjects.find(s => s.name === sub);
  if (!subjObj) {
    const colors = ['#6c5fff','#22d98a','#f0a500','#00d4cc','#ff5fa0','#3b9eff'];
    const icons = ['📖','🔬','⚡','📜','∑','🌍','💊','🧪'];
    subjObj = { name: sub, icon: icons[CU.subjects.length % icons.length], color: colors[CU.subjects.length % colors.length], progress: 0, cards: 0, quizzes: 0 };
    CU.subjects.push(subjObj);
  }
  subjObj.cards = (subjObj.cards || 0) + genCards.length;

  persistUser();
  renderSubjPickers();
  renderHome();
  loadFC();
  populateExistingSubjects();

  toast('✅ Added ' + genCards.length + ' flashcards + ' + genQuizQ.length + ' quiz Qs to "' + sub + '"!');
  clearGen();
}

function populateExistingSubjects() {
  const sel = document.getElementById('upload-subj-existing');
  if (!sel) return;
  sel.innerHTML = '<option value="">Or pick existing…</option>';
  const allSubjs = [...new Set([...CU.subjects.map(s=>s.name), ...Object.keys(qzDB)])];
  allSubjs.forEach(name => {
    const s = CU.subjects.find(x=>x.name===name);
    const cardCount = (CU.extraCards||[]).filter(c=>c.subject===name).length;
    const opt = document.createElement('option');
    opt.value = name;
    opt.textContent = (s ? s.icon+' ' : '📖 ') + name + ' (' + cardCount + ' cards)';
    sel.appendChild(opt);
  });
}

function clearGen() {
  genCards = []; genQuizQ = [];
  document.getElementById('upload-results').style.display = 'none';
  document.getElementById('notes-txt').value = '';
  const ytEl = document.getElementById('yt-url'); if (ytEl) ytEl.value = '';
  const nameEl = document.getElementById('pdf-name'); if (nameEl) { nameEl.textContent = ''; nameEl.style.color = 'var(--muted)'; }
  const fi = document.getElementById('pdf-file'); if (fi) fi.value = '';
}

// ════════════════════════════════
//  PROGRESS
// ════════════════════════════════
function renderProgress() {
  const el = document.getElementById('prog-subjs');
  if (!el) return;
  el.innerHTML = '';
  const allSubjs = [...new Set([...getAllUserSubjects(), ...CU.subjects.map(s=>s.name)])];
  if (!allSubjs.length) {
    el.innerHTML = '<p style="color:var(--muted);font-size:13px;grid-column:1/-1;">No subjects yet — upload a PDF to start tracking progress.</p>';
    return;
  }
  allSubjs.forEach(name => {
    const subj = CU.subjects.find(s=>s.name===name) || {name,icon:'📖',color:'var(--acc)',progress:0,cards:0,quizzes:0};
    const cardCount = (CU.extraCards||[]).filter(c=>c.subject===name).length;
    const quizCount = (qzDB[name]||[]).length;
    const card = document.createElement('div');
    card.className = 'prog-subj';
    card.innerHTML = `
      <div class="prog-header">
        <span style="font-size:18px;">${subj.icon||'📖'}</span>
        <span style="font-family:var(--fh);font-size:14px;font-weight:700;">${name}</span>
        <span style="margin-left:auto;font-family:var(--fh);font-size:13px;font-weight:700;color:${subj.color||'var(--acc)'};">${subj.progress||0}%</span>
      </div>
      <div class="prog-bar" style="margin-bottom:8px;"><div class="prog-fill" style="width:${subj.progress||0}%;background:${subj.color||'var(--acc)'};"></div></div>
      <div style="font-size:11px;color:var(--muted);">${cardCount} flashcards · ${quizCount} quiz questions</div>`;
    el.appendChild(card);
  });
}

function renderWeeklyBars() {
  const el = document.getElementById('week-bars');
  if (!el) return;
  const days = ['M','T','W','T','F','S','S'];
  const vals = CU.weeklyXP || [0,0,0,0,0,0,0];
  const max = Math.max(...vals, 1);
  el.innerHTML = '';
  days.forEach((d,i) => {
    const wrap = document.createElement('div');
    wrap.className = 'wbar-wrap';
    const bar = document.createElement('div');
    bar.className = 'wbar';
    const h = Math.max(3, Math.round((vals[i]/max)*60));
    bar.style.cssText = `height:${h}px;background:${i===6?'var(--acc)':'var(--s4)'};`;
    const lbl = document.createElement('div');
    lbl.className = 'wlbl'; lbl.textContent = d;
    wrap.appendChild(bar); wrap.appendChild(lbl);
    el.appendChild(wrap);
  });
}

function renderStreak() {
  const el = document.getElementById('streak-days');
  if (!el) return;
  const dayNames = ['Sun','Mon','Tue','Wed','Thu','Fri','Sat'];
  const today = new Date().getDay();
  const statuses = CU.streakDays || Array(7).fill(false);
  el.innerHTML = '';
  // Show last 7 days, ending today
  for (let offset = 6; offset >= 0; offset--) {
    const dayIdx = (today - offset + 7) % 7;
    const isToday = offset === 0;
    const done = isToday || statuses[dayIdx];
    const xp = (CU.weeklyXP || [])[dayIdx] || 0;
    const div = document.createElement('div');
    div.style.cssText = 'display:flex;flex-direction:column;align-items:center;gap:4px;flex:1;';
    const circle = document.createElement('div');
    circle.className = `sday ${isToday ? 'today' : done ? 'done' : 'miss'}`;
    circle.style.cssText = 'width:38px;height:38px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:11px;font-weight:700;font-family:var(--fh);';
    circle.textContent = isToday ? '🔥' : done ? '✓' : '–';
    const lbl = document.createElement('div');
    lbl.style.cssText = 'font-size:10px;color:var(--muted);font-family:var(--fh);font-weight:600;';
    lbl.textContent = dayNames[dayIdx];
    const xpLbl = document.createElement('div');
    xpLbl.style.cssText = `font-size:9px;color:${xp>0?'var(--acc2)':'var(--dim)'};font-family:var(--fh);`;
    xpLbl.textContent = xp > 0 ? `+${xp}` : '0';
    div.appendChild(circle);
    div.appendChild(lbl);
    div.appendChild(xpLbl);
    el.appendChild(div);
  }
}

// ════════════════════════════════
//  LEVELS & BADGES
// ════════════════════════════════
const BADGES_DEF = [
  {icon:'🔥',name:'First flame',desc:'Study for the first time',cond:u=>u.cardsStudied>=1},
  {icon:'📚',name:'Bookworm',desc:'Study 50 cards',cond:u=>u.cardsStudied>=50},
  {icon:'🧠',name:'Brain power',desc:'Study 200 cards',cond:u=>u.cardsStudied>=200},
  {icon:'🏆',name:'Quiz champion',desc:'Complete 10 quizzes',cond:u=>u.quizzesDone>=10},
  {icon:'⚡',name:'Speed demon',desc:'Finish a 60s sprint',cond:u=>u.quizzesDone>=5},
  {icon:'🔢',name:'Scholar',desc:'Reach Level 3',cond:u=>u.level>=3},
  {icon:'⭐',name:'Expert',desc:'Reach Level 5',cond:u=>u.level>=5},
  {icon:'💎',name:'Legend',desc:'Reach Level 8',cond:u=>u.level>=8},
];

function renderLevels() {
  const grid = document.getElementById('lvl-grid');
  if (!grid) return;
  grid.innerHTML = '';
  for (let i = 1; i <= 10; i++) {
    const card = document.createElement('div');
    const unlocked = i <= CU.level;
    const current = i === CU.level;
    card.className = `lvl-card ${current?'current':unlocked?'unlocked':'locked'}`;
    card.innerHTML = `<div class="lvl-n" style="color:${current?'var(--green)':unlocked?'var(--acc)':'var(--dim)'}">${i}</div>
      <div class="lvl-name">${LVL_NAMES[i-1]}</div>
      <div class="lvl-req">${current?'Current':unlocked?'✓':LVL_XP[i-1].toLocaleString()+' XP'}</div>`;
    grid.appendChild(card);
  }
  updateLevelScreen();
}

function renderBadges() {
  const el = document.getElementById('badge-wrap');
  if (!el) return;
  el.innerHTML = '';
  BADGES_DEF.forEach(b => {
    const earned = b.cond(CU);
    const div = document.createElement('div');
    div.className = 'bdg' + (earned ? '' : ' locked');
    div.innerHTML = `<span class="bdg-icon">${b.icon}</span><div><div class="bdg-name">${b.name}</div><div class="bdg-desc">${b.desc}</div></div>`;
    el.appendChild(div);
  });
}

// ════════════════════════════════
//  ADMIN
// ════════════════════════════════
let adminUnlocked = false;

function unlockAdmin() {
  const pw = document.getElementById('admin-pw-inp').value;
  if (pw === ADMIN_PASS) {
    adminUnlocked = true;
    document.getElementById('admin-locked-view').style.display = 'none';
    document.getElementById('admin-panel').style.display = 'block';
    renderAdminPanel();
  } else { toast('Wrong password'); }
}

function renderAdminPanel() {
  if (!adminUnlocked && !CU?.isAdmin) return;
  if (!adminUnlocked) adminUnlocked = true;

  // Pre-fill API key field
  const keyInp = document.getElementById('admin-api-key');
  if (keyInp) {
    const saved = "";
    if (saved) keyInp.value = saved;
  }
  updateKeyStatus();

  const users = getAllUsers().filter(u => u.username !== 'admin');
  const active = users.filter(u => Date.now() - (u.lastSeen||0) < 86400000);
  const totalCards = users.reduce((a,u) => a+(u.cardsStudied||0), 0);
  const totalQuizzes = users.reduce((a,u) => a+(u.quizzesDone||0), 0);

  const statsEl = document.getElementById('admin-stats-row');
  if (statsEl) statsEl.innerHTML = `
    <div class="admin-stat"><div class="admin-n" style="color:var(--acc)">${users.length}</div><div class="admin-l">total users</div></div>
    <div class="admin-stat"><div class="admin-n" style="color:var(--green)">${active.length}</div><div class="admin-l">active today</div></div>
    <div class="admin-stat"><div class="admin-n" style="color:var(--amber)">${totalCards}</div><div class="admin-l">cards studied</div></div>
    <div class="admin-stat"><div class="admin-n" style="color:var(--teal)">${totalQuizzes}</div><div class="admin-l">quizzes done</div></div>`;

  renderUsersTable(users);
}

function renderUsersTable(users) {
  const el = document.getElementById('users-table');
  if (!el) return;
  el.innerHTML = `<div class="ut-head">
    <div class="ut-lhd">User</div>
    <div class="ut-lhd">Level</div>
    <div class="ut-lhd ut-subj">XP</div>
    <div class="ut-lhd ut-lv">Quizzes</div>
    <div class="ut-lhd">Status</div>
    <div class="ut-lhd">Actions</div>
  </div>`;
  users.forEach(u => {
    const active = Date.now() - (u.lastSeen||0) < 86400000;
    const row = document.createElement('div');
    row.className = 'ut-row';
    row.innerHTML = `
      <div class="ut-name"><div class="ut-av" style="background:${stringToColor(u.username)}22;color:${stringToColor(u.username)}">${u.username.slice(0,2).toUpperCase()}</div>${u.username}<span style="font-size:10px;color:var(--muted);margin-left:4px;">${u.email||''}</span></div>
      <div>Lv ${u.level||1}</div>
      <div class="ut-subj">${(u.xp||0).toLocaleString()}</div>
      <div class="ut-lv">${u.quizzesDone||0}</div>
      <div><span class="ut-status ${active?'active':'inactive'}">${active?'Active':'Inactive'}</span></div>
      <div style="display:flex;gap:6px;">
        <button class="btn btn-xs" onclick="viewUser('${u.username}')">View</button>
        <button class="btn btn-xs btn-danger" onclick="deleteUser('${u.username}')">Delete</button>
      </div>`;
    el.appendChild(row);
  });
}

function filterAdminUsers() {
  const q = document.getElementById('admin-search').value.toLowerCase();
  const users = getAllUsers().filter(u => u.username !== 'admin' && u.username.toLowerCase().includes(q));
  renderUsersTable(users);
}

function viewUser(un) {
  const u = getUser(un);
  if (!u) return;
  const acc = u.accuracyCount > 0 ? Math.round(u.totalAccuracy/u.accuracyCount)+'%' : '—';
  toast(`${un}: Lv${u.level} · ${u.xp}XP · ${u.quizzesDone} quizzes · ${acc} acc · ${u.streak||0}🔥`);
}

function deleteUser(un) {
  if (!confirm(`Delete user "${un}"? This cannot be undone.`)) return;
  const db = loadDB();
  delete db[un];
  saveDB(db);
  renderAdminPanel();
  toast(`User ${un} deleted.`);
}

function resetAllUsers() {
  const db = loadDB();
  Object.keys(db).forEach(k => {
    if (k !== 'admin') delete db[k];
  });
  saveDB(db);
  renderAdminPanel();
  toast('All user data reset.');
}

function exportUsers() {
  const users = getAllUsers().filter(u => u.username !== 'admin');
  const csv = ['Username,Email,Level,XP,Streak,Cards,Quizzes,Accuracy,Last Seen',
    ...users.map(u => `${u.username},${u.email||''},${u.level||1},${u.xp||0},${u.streak||0},${u.cardsStudied||0},${u.quizzesDone||0},${u.accuracyCount>0?Math.round(u.totalAccuracy/u.accuracyCount)+'%':'—'},${new Date(u.lastSeen||0).toLocaleDateString()}`)
  ].join('\n');
  const blob = new Blob([csv], {type:'text/csv'});
  const a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  a.download = 'toutify_users.csv';
  a.click();
}

// ════════════════════════════════
//  UTILS
// ════════════════════════════════
function toast(msg) {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  clearTimeout(t._timeout);
  t._timeout = setTimeout(() => t.classList.remove('show'), 3000);
}

function openModal(id) { document.getElementById(id).classList.add('open'); }
function closeModal(id) { document.getElementById(id).classList.remove('open'); }

// Close modals on bg click
document.querySelectorAll('.modal-bg').forEach(bg => {
  bg.addEventListener('click', e => { if (e.target === bg) bg.classList.remove('open'); });
});

// ── PAGE INIT ──
(function() {
  // Load saved API key into memory silently — no UI shown to users
  const savedKey = localStorage.getItem('toutify_apikey');
  if (savedKey) API_KEY = savedKey;
})();
</script>
</body>
</html>
