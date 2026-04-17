<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Sparked — AI STEM Learning Platform</title>
<meta name="description" content="Master STEM with AI-powered lessons, daily challenges, and a smart tutor. Free forever.">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=Instrument+Serif:ital@0;1&family=JetBrains+Mono:wght@400;600&display=swap" rel="stylesheet">
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
:root{
  --bg:#060608;--s1:#0d0d14;--s2:#13131f;--s3:#1a1a2e;
  --border:rgba(255,255,255,0.07);--border2:rgba(255,255,255,0.12);
  --gold:#f5c842;--spark:#7c6af5;--spark2:#a593ff;
  --teal:#3ecfb2;--red:#ff5c5c;--green:#4ade80;
  --text:#eeedf8;--muted:rgba(238,237,248,0.45);--dim:rgba(238,237,248,0.25);
  --font:'Syne',sans-serif;--serif:'Instrument Serif',serif;--mono:'JetBrains Mono',monospace;
  --r:12px;--r2:20px;
}
html{scroll-behavior:smooth}
body{background:var(--bg);color:var(--text);font-family:var(--font);overflow-x:hidden;min-height:100vh}

/* ── SCROLLBAR ── */
::-webkit-scrollbar{width:4px}::-webkit-scrollbar-track{background:var(--s1)}::-webkit-scrollbar-thumb{background:var(--spark);border-radius:2px}

/* ── SCREENS ── */
.screen{display:none}.screen.active{display:block}

/* ══════════════════ NAV ══════════════════ */
nav{position:fixed;top:0;left:0;right:0;z-index:200;height:60px;
  display:flex;align-items:center;justify-content:space-between;padding:0 1.5rem;
  background:rgba(6,6,8,0.85);backdrop-filter:blur(16px);
  border-bottom:1px solid var(--border)}
.nav-logo{font-family:var(--serif);font-size:1.5rem;cursor:pointer;display:flex;align-items:center;gap:6px}
.nav-logo span{color:var(--spark2)}
.nav-center{display:flex;gap:4px}
.nav-tab{padding:0.35rem 0.9rem;border-radius:8px;font-size:0.82rem;font-family:var(--font);font-weight:600;cursor:pointer;border:none;background:transparent;color:var(--muted);transition:all .2s;letter-spacing:.03em}
.nav-tab:hover,.nav-tab.active{background:var(--s2);color:var(--text)}
.nav-right{display:flex;align-items:center;gap:0.6rem}
.xp-pill{display:flex;align-items:center;gap:5px;padding:0.3rem 0.7rem;background:rgba(245,200,66,0.1);border:1px solid rgba(245,200,66,0.2);border-radius:20px;font-size:0.78rem;font-weight:700;color:var(--gold)}
.streak-pill{display:flex;align-items:center;gap:4px;padding:0.3rem 0.7rem;background:rgba(255,92,92,0.1);border:1px solid rgba(255,92,92,0.2);border-radius:20px;font-size:0.78rem;font-weight:700;color:var(--red)}
.nav-avatar{width:32px;height:32px;border-radius:50%;background:linear-gradient(135deg,var(--spark),var(--teal));display:flex;align-items:center;justify-content:center;font-size:0.8rem;font-weight:700;cursor:pointer;flex-shrink:0}

/* ══════════════════ HERO ══════════════════ */
.hero{min-height:100vh;display:flex;flex-direction:column;align-items:center;justify-content:center;padding:5rem 1.5rem 3rem;text-align:center;position:relative;overflow:hidden}
.hero-bg{position:absolute;inset:0;z-index:0;overflow:hidden}
.hero-orb{position:absolute;border-radius:50%;filter:blur(80px);opacity:.18}
.hero-orb1{width:600px;height:600px;background:var(--spark);top:-200px;left:-150px}
.hero-orb2{width:500px;height:500px;background:var(--teal);bottom:-100px;right:-100px}
.hero-orb3{width:300px;height:300px;background:var(--gold);top:50%;left:50%;transform:translate(-50%,-50%)}
.hero-grid{position:absolute;inset:0;background-image:linear-gradient(var(--border) 1px,transparent 1px),linear-gradient(90deg,var(--border) 1px,transparent 1px);background-size:60px 60px;opacity:.4}
.hero-content{position:relative;z-index:1;max-width:860px}
.hero-badge{display:inline-flex;align-items:center;gap:6px;padding:.35rem 1rem;border:1px solid rgba(124,106,245,.35);border-radius:20px;font-size:.75rem;font-weight:700;color:var(--spark2);background:rgba(124,106,245,.08);letter-spacing:.08em;text-transform:uppercase;margin-bottom:1.8rem;animation:fadeUp .6s ease both}
@keyframes fadeUp{from{opacity:0;transform:translateY(16px)}to{opacity:1;transform:none}}
.hero h1{font-family:var(--serif);font-size:clamp(3rem,7vw,5.5rem);line-height:1.08;margin-bottom:1.4rem;animation:fadeUp .6s .1s ease both}
.hero h1 em{font-style:italic;color:var(--spark2)}
.hero h1 strong{color:var(--gold)}
.hero-sub{font-size:1.1rem;color:var(--muted);max-width:560px;margin:0 auto 2.5rem;line-height:1.75;animation:fadeUp .6s .2s ease both}
.hero-ctas{display:flex;gap:1rem;justify-content:center;flex-wrap:wrap;animation:fadeUp .6s .3s ease both}
.btn{padding:.7rem 1.8rem;border-radius:var(--r);font-family:var(--font);font-size:.95rem;font-weight:700;cursor:pointer;transition:all .2s;border:none;letter-spacing:.02em}
.btn-primary{background:var(--spark);color:#fff}
.btn-primary:hover{background:var(--spark2);transform:translateY(-2px);box-shadow:0 12px 32px rgba(124,106,245,.4)}
.btn-ghost{background:transparent;color:var(--text);border:1px solid var(--border2)}
.btn-ghost:hover{border-color:var(--spark2);color:var(--spark2)}
.btn-gold{background:var(--gold);color:#000}
.btn-gold:hover{opacity:.88;transform:translateY(-2px)}
.btn-teal{background:var(--teal);color:#000}
.hero-stats{display:flex;gap:2.5rem;justify-content:center;margin-top:3.5rem;animation:fadeUp .6s .4s ease both;flex-wrap:wrap}
.hero-stat{text-align:center}
.hero-stat-n{font-family:var(--serif);font-size:2rem;color:var(--spark2)}
.hero-stat-l{font-size:.75rem;color:var(--muted);text-transform:uppercase;letter-spacing:.08em;margin-top:2px}

/* ══════════════════ SECTION HELPERS ══════════════════ */
.section{max-width:1100px;margin:0 auto;padding:2rem 1.5rem}
.section-label{font-size:.75rem;text-transform:uppercase;letter-spacing:.1em;color:var(--muted);margin-bottom:1.2rem;font-weight:600}
.card{background:var(--s1);border:1px solid var(--border);border-radius:var(--r2);transition:all .2s}
.card:hover{border-color:var(--border2)}

/* ══════════════════ DASHBOARD ══════════════════ */
#screen-dashboard{padding-top:60px}
.dash-hero{background:linear-gradient(135deg,var(--s2),var(--s3));border-bottom:1px solid var(--border);padding:2.5rem 1.5rem}
.dash-hero-inner{max-width:1100px;margin:0 auto;display:flex;justify-content:space-between;align-items:center;flex-wrap:wrap;gap:1.5rem}
.dash-greeting{font-family:var(--serif);font-size:2rem}
.dash-greeting span{color:var(--spark2);font-style:italic}
.dash-stats{display:flex;gap:1rem;flex-wrap:wrap}
.dash-stat{background:var(--s1);border:1px solid var(--border);border-radius:var(--r);padding:.8rem 1.2rem;min-width:100px;text-align:center}
.dash-stat-n{font-size:1.5rem;font-weight:800;color:var(--gold)}
.dash-stat-l{font-size:.7rem;color:var(--muted);text-transform:uppercase;letter-spacing:.06em;margin-top:2px}
.dash-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(300px,1fr));gap:1.2rem;margin-top:2rem}
.dash-card{background:var(--s1);border:1px solid var(--border);border-radius:var(--r2);padding:1.4rem;cursor:pointer;transition:all .2s}
.dash-card:hover{border-color:var(--spark2);transform:translateY(-3px)}
.dash-card-icon{font-size:2rem;margin-bottom:.8rem}
.dash-card-title{font-size:1rem;font-weight:700;margin-bottom:.4rem}
.dash-card-sub{font-size:.82rem;color:var(--muted);line-height:1.6}
.dash-card-badge{display:inline-block;padding:.2rem .6rem;border-radius:6px;font-size:.7rem;font-weight:700;margin-top:.8rem}
.badge-new{background:rgba(124,106,245,.2);color:var(--spark2)}
.badge-hot{background:rgba(255,92,92,.2);color:var(--red)}
.badge-gold{background:rgba(245,200,66,.15);color:var(--gold)}
.daily-streak-bar{max-width:1100px;margin:1.5rem auto 0;display:flex;gap:.5rem;flex-wrap:wrap}
.streak-day{width:36px;height:36px;border-radius:8px;display:flex;align-items:center;justify-content:center;font-size:.7rem;font-weight:700;border:1px solid var(--border)}
.streak-day.done{background:linear-gradient(135deg,var(--spark),var(--teal));border-color:transparent;color:#fff}
.streak-day.today{border-color:var(--gold);color:var(--gold)}

/* ══════════════════ SUBJECTS / COURSES ══════════════════ */
#screen-learn{padding-top:80px}
.subject-tabs{display:flex;gap:.5rem;flex-wrap:wrap;margin-bottom:1.5rem}
.stab{padding:.4rem 1rem;border-radius:20px;font-size:.82rem;font-weight:600;cursor:pointer;border:1px solid var(--border);background:transparent;color:var(--muted);transition:all .2s;font-family:var(--font)}
.stab:hover,.stab.active{background:var(--spark);border-color:var(--spark);color:#fff}
.course-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(270px,1fr));gap:1.2rem}
.course-card{background:var(--s1);border:1px solid var(--border);border-radius:var(--r2);padding:1.4rem;cursor:pointer;transition:all .25s;position:relative;overflow:hidden}
.course-card::after{content:'';position:absolute;inset:0;opacity:0;transition:.2s;background:linear-gradient(135deg,rgba(124,106,245,.05),transparent)}
.course-card:hover{border-color:var(--spark2);transform:translateY(-3px)}
.course-card:hover::after{opacity:1}
.cc-level{font-size:.7rem;font-weight:700;text-transform:uppercase;letter-spacing:.08em;margin-bottom:.6rem}
.cc-lvl-b{color:var(--teal)}.cc-lvl-i{color:var(--gold)}.cc-lvl-a{color:var(--red)}
.cc-title{font-size:1rem;font-weight:700;margin-bottom:.5rem;line-height:1.3}
.cc-desc{font-size:.82rem;color:var(--muted);line-height:1.6;margin-bottom:1rem}
.cc-meta{display:flex;gap:.8rem;font-size:.76rem;color:var(--dim)}
.cc-progress{margin-top:.9rem;height:3px;background:var(--s3);border-radius:2px}
.cc-progress-fill{height:100%;border-radius:2px;background:linear-gradient(90deg,var(--spark),var(--teal));transition:width .5s}
.cc-start{width:100%;margin-top:1rem;padding:.55rem;border-radius:8px;font-family:var(--font);font-size:.84rem;font-weight:700;background:var(--spark);color:#fff;border:none;cursor:pointer;transition:.2s}
.cc-start:hover{background:var(--spark2)}

/* ══════════════════ LESSON VIEW ══════════════════ */
#screen-lesson{padding-top:60px}
.lesson-wrap{max-width:780px;margin:0 auto;padding:2.5rem 1.5rem}
.lesson-topbar{display:flex;align-items:center;gap:1rem;margin-bottom:2rem;flex-wrap:wrap}
.progress-track{flex:1;height:6px;background:var(--s2);border-radius:3px;min-width:100px}
.progress-fill{height:100%;border-radius:3px;background:linear-gradient(90deg,var(--spark),var(--teal));transition:width .6s}
.lesson-hdr{margin-bottom:2rem;padding-bottom:1.5rem;border-bottom:1px solid var(--border)}
.lesson-tag{font-size:.72rem;font-weight:700;text-transform:uppercase;letter-spacing:.1em;color:var(--spark2);margin-bottom:.5rem}
.lesson-title{font-family:var(--serif);font-size:2.2rem;line-height:1.15;margin-bottom:.8rem}
.lesson-meta{display:flex;gap:1.2rem;font-size:.8rem;color:var(--muted)}
.lesson-body{line-height:1.85;color:rgba(238,237,248,.88)}
.lesson-body h3{font-size:1.1rem;font-weight:700;margin:2rem 0 .7rem;color:var(--text)}
.lesson-body p{margin-bottom:1.2rem}
.lesson-body strong{color:var(--text);font-weight:700}
.formula-box{background:var(--s2);border:1px solid rgba(62,207,178,.2);border-radius:var(--r);padding:.9rem 1.2rem;font-family:var(--mono);font-size:.95rem;color:var(--teal);text-align:center;margin:1.2rem 0;letter-spacing:.02em}
.insight-box{background:var(--s2);border-left:3px solid var(--spark2);border-radius:0 var(--r) var(--r) 0;padding:1rem 1.2rem;margin:1.5rem 0;font-size:.9rem;color:var(--muted)}
.insight-box em{color:var(--spark2);font-style:normal;font-weight:700}
.quiz-block{background:var(--s2);border:1px solid var(--border);border-radius:var(--r2);padding:1.5rem;margin:2rem 0}
.quiz-label{font-size:.75rem;font-weight:700;text-transform:uppercase;letter-spacing:.1em;color:var(--spark2);margin-bottom:1rem}
.quiz-q{font-size:1rem;font-weight:700;margin-bottom:1rem;line-height:1.5}
.quiz-opts{display:flex;flex-direction:column;gap:.6rem}
.qopt{padding:.7rem 1rem;border:1px solid var(--border);border-radius:10px;cursor:pointer;font-size:.88rem;font-family:var(--font);background:var(--s3);color:var(--text);text-align:left;transition:.2s}
.qopt:hover:not(:disabled){border-color:var(--spark2);background:rgba(124,106,245,.08)}
.qopt.correct{border-color:var(--teal);background:rgba(62,207,178,.1);color:var(--teal)}
.qopt.wrong{border-color:var(--red);background:rgba(255,92,92,.08);color:var(--red)}
.quiz-fb{margin-top:1rem;padding:.8rem 1rem;border-radius:8px;font-size:.86rem;display:none}
.quiz-fb.show{display:block}
.xp-toast{position:fixed;bottom:2rem;right:2rem;background:var(--gold);color:#000;padding:.6rem 1.2rem;border-radius:20px;font-weight:700;font-size:.9rem;z-index:999;animation:toastIn .4s ease,toastOut .4s 2s ease forwards;pointer-events:none}
@keyframes toastIn{from{opacity:0;transform:translateY(20px)}to{opacity:1;transform:none}}
@keyframes toastOut{to{opacity:0;transform:translateY(-10px)}}
.lesson-nav{display:flex;justify-content:space-between;align-items:center;margin-top:3rem;padding-top:1.5rem;border-top:1px solid var(--border)}

/* ══════════════════ AI TUTOR CHATBOT ══════════════════ */
.chat-fab{position:fixed;bottom:1.5rem;right:1.5rem;z-index:300;width:54px;height:54px;border-radius:50%;background:linear-gradient(135deg,var(--spark),var(--teal));border:none;cursor:pointer;display:flex;align-items:center;justify-content:center;font-size:1.3rem;box-shadow:0 8px 24px rgba(124,106,245,.5);transition:.2s}
.chat-fab:hover{transform:scale(1.08)}
.chat-fab .notif{position:absolute;top:-2px;right:-2px;width:14px;height:14px;background:var(--red);border-radius:50%;border:2px solid var(--bg);font-size:.6rem;display:flex;align-items:center;justify-content:center;color:#fff;font-weight:700}
.chat-window{position:fixed;bottom:4.5rem;right:1.5rem;width:360px;max-height:520px;background:var(--s1);border:1px solid var(--border2);border-radius:var(--r2);z-index:299;display:none;flex-direction:column;box-shadow:0 24px 60px rgba(0,0,0,.6);overflow:hidden}
.chat-window.open{display:flex}
.chat-head{padding:1rem 1.2rem;border-bottom:1px solid var(--border);display:flex;align-items:center;gap:.8rem;background:var(--s2)}
.chat-avatar{width:36px;height:36px;border-radius:50%;background:linear-gradient(135deg,var(--spark),var(--teal));display:flex;align-items:center;justify-content:center;font-size:1rem;flex-shrink:0}
.chat-head-info h4{font-size:.9rem;font-weight:700}
.chat-head-info p{font-size:.72rem;color:var(--teal)}
.chat-close{margin-left:auto;background:none;border:none;color:var(--muted);font-size:1.1rem;cursor:pointer;padding:.2rem}
.chat-messages{flex:1;overflow-y:auto;padding:1rem;display:flex;flex-direction:column;gap:.8rem}
.msg{max-width:85%;padding:.65rem .9rem;border-radius:12px;font-size:.86rem;line-height:1.6}
.msg-ai{background:var(--s3);color:var(--text);align-self:flex-start;border-bottom-left-radius:4px}
.msg-user{background:var(--spark);color:#fff;align-self:flex-end;border-bottom-right-radius:4px}
.msg-typing{display:flex;gap:4px;padding:.65rem .9rem;background:var(--s3);border-radius:12px;border-bottom-left-radius:4px;width:50px;align-self:flex-start}
.msg-typing span{width:7px;height:7px;background:var(--muted);border-radius:50%;animation:bounce .8s infinite}
.msg-typing span:nth-child(2){animation-delay:.15s}
.msg-typing span:nth-child(3){animation-delay:.3s}
@keyframes bounce{0%,80%,100%{transform:translateY(0)}40%{transform:translateY(-6px)}}
.chat-input-row{padding:.8rem;border-top:1px solid var(--border);display:flex;gap:.6rem}
.chat-input{flex:1;padding:.55rem .9rem;background:var(--s2);border:1px solid var(--border);border-radius:8px;font-family:var(--font);font-size:.85rem;color:var(--text);outline:none;transition:.2s}
.chat-input:focus{border-color:var(--spark2)}
.chat-send{padding:.55rem .9rem;background:var(--spark);color:#fff;border:none;border-radius:8px;font-family:var(--font);font-size:.82rem;font-weight:700;cursor:pointer;transition:.2s}
.chat-send:hover{background:var(--spark2)}

/* ══════════════════ CHALLENGES ══════════════════ */
#screen-challenges{padding-top:80px}
.challenge-hero{background:linear-gradient(135deg,rgba(245,200,66,.08),rgba(124,106,245,.08));border:1px solid rgba(245,200,66,.15);border-radius:var(--r2);padding:2rem;margin-bottom:2rem;display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:1rem}
.ch-title{font-family:var(--serif);font-size:1.8rem;margin-bottom:.4rem}
.ch-sub{color:var(--muted);font-size:.9rem}
.timer-pill{font-family:var(--mono);font-size:1.2rem;font-weight:700;color:var(--gold);background:rgba(245,200,66,.1);padding:.5rem 1rem;border-radius:10px;border:1px solid rgba(245,200,66,.2)}
.challenge-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(280px,1fr));gap:1rem}
.chal-card{background:var(--s1);border:1px solid var(--border);border-radius:var(--r2);padding:1.3rem;cursor:pointer;transition:.2s}
.chal-card:hover{border-color:var(--gold);transform:translateY(-2px)}
.chal-xp{font-size:.72rem;font-weight:700;color:var(--gold);text-transform:uppercase;letter-spacing:.08em;margin-bottom:.5rem}
.chal-title{font-size:.95rem;font-weight:700;margin-bottom:.4rem;line-height:1.3}
.chal-desc{font-size:.8rem;color:var(--muted);line-height:1.5;margin-bottom:.8rem}
.chal-tags{display:flex;gap:.4rem;flex-wrap:wrap}
.tag{padding:.18rem .55rem;border-radius:5px;font-size:.68rem;font-weight:700;background:var(--s3);color:var(--dim)}

/* ══════════════════ LEADERBOARD ══════════════════ */
#screen-leaderboard{padding-top:80px}
.lb-podium{display:flex;justify-content:center;align-items:flex-end;gap:1rem;margin-bottom:2.5rem;flex-wrap:wrap}
.podium-item{text-align:center;flex:1;max-width:160px}
.podium-avatar{width:56px;height:56px;border-radius:50%;margin:0 auto .6rem;display:flex;align-items:center;justify-content:center;font-size:1.4rem;font-weight:800;font-family:var(--serif)}
.p1 .podium-avatar{width:68px;height:68px;background:linear-gradient(135deg,#f5c842,#ff9f43);font-size:1.6rem}
.p2 .podium-avatar{background:linear-gradient(135deg,#b0bec5,#78909c)}
.p3 .podium-avatar{background:linear-gradient(135deg,#cd7f32,#a0522d)}
.podium-name{font-size:.85rem;font-weight:700;margin-bottom:.2rem}
.podium-xp{font-size:.75rem;color:var(--gold);font-weight:700}
.podium-rank{font-size:.7rem;color:var(--muted)}
.podium-bar{margin-top:.6rem;border-radius:8px 8px 0 0}
.p1 .podium-bar{height:80px;background:linear-gradient(0deg,rgba(245,200,66,.3),rgba(245,200,66,.1))}
.p2 .podium-bar{height:60px;background:linear-gradient(0deg,rgba(176,190,197,.3),rgba(176,190,197,.1))}
.p3 .podium-bar{height:44px;background:linear-gradient(0deg,rgba(205,127,50,.3),rgba(205,127,50,.1))}
.lb-list{display:flex;flex-direction:column;gap:.6rem}
.lb-row{display:flex;align-items:center;gap:1rem;background:var(--s1);border:1px solid var(--border);border-radius:var(--r);padding:.9rem 1.2rem;transition:.2s}
.lb-row:hover{border-color:var(--border2)}
.lb-row.me{border-color:var(--spark2);background:rgba(124,106,245,.06)}
.lb-pos{font-size:.85rem;font-weight:800;color:var(--dim);width:24px;text-align:center;flex-shrink:0}
.lb-av{width:36px;height:36px;border-radius:50%;background:var(--s3);display:flex;align-items:center;justify-content:center;font-size:.9rem;font-weight:700;flex-shrink:0}
.lb-name{flex:1;font-size:.9rem;font-weight:600}
.lb-subject{font-size:.74rem;color:var(--muted)}
.lb-score{font-size:.9rem;font-weight:800;color:var(--gold)}

/* ══════════════════ PROFILE ══════════════════ */
#screen-profile{padding-top:80px}
.profile-hero{background:linear-gradient(135deg,var(--s2),var(--s3));border-bottom:1px solid var(--border);padding:2.5rem 1.5rem}
.profile-inner{max-width:1100px;margin:0 auto;display:flex;gap:2rem;align-items:center;flex-wrap:wrap}
.profile-av{width:80px;height:80px;border-radius:50%;background:linear-gradient(135deg,var(--spark),var(--teal));display:flex;align-items:center;justify-content:center;font-family:var(--serif);font-size:2rem;flex-shrink:0;border:3px solid var(--spark2)}
.profile-info h2{font-family:var(--serif);font-size:1.8rem;margin-bottom:.3rem}
.profile-info p{color:var(--muted);font-size:.88rem}
.badges-strip{display:flex;gap:.5rem;margin-top:.8rem;flex-wrap:wrap}
.badge-item{padding:.25rem .7rem;border-radius:20px;font-size:.72rem;font-weight:700;border:1px solid}
.badge-item.gold{color:var(--gold);border-color:rgba(245,200,66,.3);background:rgba(245,200,66,.08)}
.badge-item.teal{color:var(--teal);border-color:rgba(62,207,178,.3);background:rgba(62,207,178,.08)}
.badge-item.spark{color:var(--spark2);border-color:rgba(165,147,255,.3);background:rgba(165,147,255,.08)}
.level-bar-wrap{margin-top:1rem;max-width:300px}
.level-label{display:flex;justify-content:space-between;font-size:.75rem;color:var(--muted);margin-bottom:.4rem}
.level-bar{height:6px;background:var(--s3);border-radius:3px}
.level-fill{height:100%;background:linear-gradient(90deg,var(--spark),var(--teal));border-radius:3px}
.achievements-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(160px,1fr));gap:1rem;margin-top:1.5rem}
.ach-card{background:var(--s1);border:1px solid var(--border);border-radius:var(--r);padding:1.2rem;text-align:center}
.ach-card.earned{border-color:rgba(245,200,66,.3)}
.ach-icon{font-size:2rem;margin-bottom:.5rem}
.ach-name{font-size:.8rem;font-weight:700;margin-bottom:.2rem}
.ach-desc{font-size:.72rem;color:var(--muted);line-height:1.4}
.ach-card:not(.earned){opacity:.4;filter:grayscale(1)}

/* ══════════════════ LOADING / ERROR ══════════════════ */
.loading-box{display:flex;align-items:center;gap:.8rem;padding:1.2rem 1.4rem;background:var(--s1);border:1px solid var(--border);border-radius:var(--r);font-size:.9rem;color:var(--muted);margin:1.5rem 0}
.spin{width:18px;height:18px;border:2px solid var(--border2);border-top-color:var(--spark);border-radius:50%;animation:spin .7s linear infinite;flex-shrink:0}
@keyframes spin{to{transform:rotate(360deg)}}
.err-box{background:rgba(255,92,92,.07);border:1px solid rgba(255,92,92,.25);border-radius:var(--r);padding:1rem 1.2rem;color:var(--red);font-size:.86rem;margin:1rem 0}

/* ══════════════════ SETTINGS ══════════════════ */
#screen-settings{padding-top:80px}
.settings-wrap{max-width:700px;margin:0 auto;padding:2.5rem 1.5rem}
.settings-wrap h2{font-family:var(--serif);font-size:2rem;margin-bottom:.5rem}
.settings-wrap p{color:var(--muted);margin-bottom:2rem;line-height:1.6}
.settings-group{background:var(--s1);border:1px solid var(--border);border-radius:var(--r2);overflow:hidden;margin-bottom:1.5rem}
.settings-row{display:flex;align-items:center;gap:1rem;padding:1rem 1.4rem;border-bottom:1px solid var(--border)}
.settings-row:last-child{border-bottom:none}
.settings-label{flex:1}
.settings-label h4{font-size:.92rem;font-weight:600;margin-bottom:.2rem}
.settings-label p{font-size:.78rem;color:var(--muted);line-height:1.5}
.api-in{padding:.7rem 1rem;background:var(--s2);border:1px solid var(--border);border-radius:8px;font-family:var(--mono);font-size:.82rem;color:var(--text);width:100%;max-width:300px;transition:.2s}
.api-in:focus{outline:none;border-color:var(--spark2)}
.toggle{width:42px;height:24px;background:var(--s3);border-radius:12px;cursor:pointer;position:relative;transition:.2s;border:none;flex-shrink:0}
.toggle.on{background:var(--spark)}
.toggle::after{content:'';width:18px;height:18px;background:#fff;border-radius:50%;position:absolute;top:3px;left:3px;transition:.2s}
.toggle.on::after{left:21px}
.info-box{background:rgba(62,207,178,.06);border:1px solid rgba(62,207,178,.2);border-radius:var(--r);padding:1rem 1.2rem;font-size:.82rem;color:var(--muted);line-height:1.7;margin-top:.5rem}
.info-box strong{color:var(--teal)}

/* ══════════════════ RESPONSIVE ══════════════════ */
@media(max-width:640px){
  .nav-center{display:none}
  .hero h1{font-size:2.4rem}
  .chat-window{width:calc(100vw - 3rem);right:1.5rem}
  .lb-podium{flex-direction:row}
}
</style>
</head>
<body>

<!-- ══════════ NAV ══════════ -->
<nav>
  <div class="nav-logo" onclick="showScreen('home')"><span>⚡</span>Sparked</div>
  <div class="nav-center">
    <button class="nav-tab" onclick="showScreen('dashboard')">Dashboard</button>
    <button class="nav-tab" onclick="showScreen('learn')">Learn</button>
    <button class="nav-tab" onclick="showScreen('challenges')">Challenges</button>
    <button class="nav-tab" onclick="showScreen('leaderboard')">Leaderboard</button>
  </div>
  <div class="nav-right">
    <div class="xp-pill">⚡ <span id="nav-xp">0</span> XP</div>
    <div class="streak-pill">🔥 <span id="nav-streak">0</span></div>
    <div class="nav-avatar" onclick="showScreen('profile')" id="nav-av">?</div>
  </div>
</nav>

<!-- ══════════════════════════════════════════ -->
<!-- SCREEN: HOME                              -->
<!-- ══════════════════════════════════════════ -->
<div id="screen-home" class="screen active">
  <div class="hero">
    <div class="hero-bg">
      <div class="hero-grid"></div>
      <div class="hero-orb hero-orb1"></div>
      <div class="hero-orb hero-orb2"></div>
      <div class="hero-orb hero-orb3"></div>
    </div>
    <div class="hero-content">
      <div class="hero-badge">🚀 AI-Powered · Free Forever · No Ads</div>
      <h1>Learn STEM like<br>you were <em>born</em> for it.<br>Powered by <strong>AI.</strong></h1>
      <p class="hero-sub">Personalized lessons, daily challenges, live AI tutor, leaderboards, and streak rewards — all free. Built for students who want to become genuinely brilliant.</p>
      <div class="hero-ctas">
        <button class="btn btn-primary" onclick="onboard()">Start Learning Free →</button>
        <button class="btn btn-ghost" onclick="showScreen('learn')">Browse Courses</button>
      </div>
      <div class="hero-stats">
        <div class="hero-stat"><div class="hero-stat-n">50K+</div><div class="hero-stat-l">Learners</div></div>
        <div class="hero-stat"><div class="hero-stat-n">200+</div><div class="hero-stat-l">AI Lessons</div></div>
        <div class="hero-stat"><div class="hero-stat-n">6</div><div class="hero-stat-l">STEM Subjects</div></div>
        <div class="hero-stat"><div class="hero-stat-n">∞</div><div class="hero-stat-l">Custom Topics</div></div>
      </div>
    </div>
  </div>
</div>

<!-- ══════════════════════════════════════════ -->
<!-- SCREEN: DASHBOARD                         -->
<!-- ══════════════════════════════════════════ -->
<div id="screen-dashboard" class="screen">
  <div class="dash-hero">
    <div class="dash-hero-inner">
      <div>
        <div class="dash-greeting">Welcome back, <span id="dash-name">Learner</span> 👋</div>
        <p style="color:var(--muted);font-size:.9rem;margin-top:.3rem">You're on a <strong id="dash-streak-txt" style="color:var(--red)">0-day</strong> streak. Keep it going!</p>
        <div class="daily-streak-bar" id="streak-bar"></div>
      </div>
      <div class="dash-stats">
        <div class="dash-stat"><div class="dash-stat-n" id="d-xp">0</div><div class="dash-stat-l">Total XP</div></div>
        <div class="dash-stat"><div class="dash-stat-n" id="d-lessons">0</div><div class="dash-stat-l">Lessons Done</div></div>
        <div class="dash-stat"><div class="dash-stat-n" id="d-streak">0</div><div class="dash-stat-l">Day Streak</div></div>
        <div class="dash-stat"><div class="dash-stat-n" id="d-rank">#—</div><div class="dash-stat-l">Rank</div></div>
      </div>
    </div>
  </div>
  <div class="section">
    <div class="section-label">Quick Actions</div>
    <div class="dash-grid">
      <div class="dash-card" onclick="showScreen('challenges')">
        <div class="dash-card-icon">⚡</div>
        <div class="dash-card-title">Daily Challenge</div>
        <div class="dash-card-sub">Complete today's challenge to keep your streak alive and earn bonus XP.</div>
        <div class="dash-card-badge badge-hot">🔥 Live Now</div>
      </div>
      <div class="dash-card" onclick="showScreen('learn')">
        <div class="dash-card-icon">📚</div>
        <div class="dash-card-title">Continue Learning</div>
        <div class="dash-card-sub">Pick up where you left off or start a new AI-generated course.</div>
        <div class="dash-card-badge badge-new">✦ AI Courses</div>
      </div>
      <div class="dash-card" onclick="openChat()">
        <div class="dash-card-icon">🤖</div>
        <div class="dash-card-title">Ask the AI Tutor</div>
        <div class="dash-card-sub">Stuck on something? Spark, your AI tutor, is online 24/7.</div>
        <div class="dash-card-badge badge-new">● Online</div>
      </div>
      <div class="dash-card" onclick="showScreen('leaderboard')">
        <div class="dash-card-icon">🏆</div>
        <div class="dash-card-title">Leaderboard</div>
        <div class="dash-card-sub">See how you rank against other learners worldwide.</div>
        <div class="dash-card-badge badge-gold">🥇 Top Ranks</div>
      </div>
      <div class="dash-card" onclick="showCustomLesson()">
        <div class="dash-card-icon">✨</div>
        <div class="dash-card-title">Custom AI Lesson</div>
        <div class="dash-card-sub">Enter any STEM topic — the AI builds a full interactive lesson in seconds.</div>
        <div class="dash-card-badge badge-new">✦ Instant</div>
      </div>
      <div class="dash-card" onclick="showScreen('profile')">
        <div class="dash-card-icon">🎖️</div>
        <div class="dash-card-title">My Achievements</div>
        <div class="dash-card-sub">View earned badges, trophies, and your learning journey.</div>
        <div class="dash-card-badge badge-gold">🏅 Badges</div>
      </div>
    </div>
  </div>
</div>

<!-- ══════════════════════════════════════════ -->
<!-- SCREEN: LEARN                             -->
<!-- ══════════════════════════════════════════ -->
<div id="screen-learn" class="screen">
  <div class="section">
    <div style="display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:1rem;margin-bottom:1.5rem">
      <div>
        <h2 style="font-family:var(--serif);font-size:2rem">Courses</h2>
        <p style="color:var(--muted);font-size:.88rem;margin-top:.3rem">AI generates each lesson fresh just for you.</p>
      </div>
      <button class="btn btn-primary" onclick="showCustomLesson()">✨ Custom Lesson</button>
    </div>
    <div class="subject-tabs" id="subject-tabs">
      <button class="stab active" onclick="filterCourses('all',this)">All Subjects</button>
      <button class="stab" onclick="filterCourses('Mathematics',this)">📐 Math</button>
      <button class="stab" onclick="filterCourses('Physics',this)">⚛️ Physics</button>
      <button class="stab" onclick="filterCourses('Chemistry',this)">🧪 Chemistry</button>
      <button class="stab" onclick="filterCourses('Biology',this)">🧬 Biology</button>
      <button class="stab" onclick="filterCourses('Computer Science',this)">💻 CS</button>
      <button class="stab" onclick="filterCourses('Engineering',this)">⚙️ Engineering</button>
    </div>
    <div class="course-grid" id="course-grid"></div>
  </div>
</div>

<!-- ══════════════════════════════════════════ -->
<!-- SCREEN: LESSON                            -->
<!-- ══════════════════════════════════════════ -->
<div id="screen-lesson" class="screen">
  <div class="lesson-wrap">
    <div class="lesson-topbar">
      <button class="btn btn-ghost" id="lesson-back" style="padding:.45rem .9rem;font-size:.82rem">← Back</button>
      <div class="progress-track"><div class="progress-fill" id="lesson-progress" style="width:0%"></div></div>
      <div style="font-size:.78rem;color:var(--muted)" id="lesson-step">Step 1 / 3</div>
    </div>
    <div id="lesson-out"></div>
  </div>
</div>

<!-- ══════════════════════════════════════════ -->
<!-- SCREEN: CHALLENGES                        -->
<!-- ══════════════════════════════════════════ -->
<div id="screen-challenges" class="screen">
  <div class="section">
    <div class="challenge-hero">
      <div>
        <div class="ch-title">⚡ Daily Challenges</div>
        <div class="ch-sub">Complete challenges to earn XP and maintain your streak</div>
      </div>
      <div class="timer-pill" id="ch-timer">23:59:59</div>
    </div>
    <div class="section-label">Today's Challenges</div>
    <div class="challenge-grid" id="challenge-grid"></div>
  </div>
</div>

<!-- ══════════════════════════════════════════ -->
<!-- SCREEN: LEADERBOARD                       -->
<!-- ══════════════════════════════════════════ -->
<div id="screen-leaderboard" class="screen">
  <div class="section">
    <div style="text-align:center;margin-bottom:2rem">
      <h2 style="font-family:var(--serif);font-size:2.2rem;margin-bottom:.4rem">🏆 Leaderboard</h2>
      <p style="color:var(--muted);font-size:.9rem">Top learners this week — compete for the crown</p>
    </div>
    <div class="lb-podium" id="lb-podium"></div>
    <div class="lb-list" id="lb-list"></div>
  </div>
</div>

<!-- ══════════════════════════════════════════ -->
<!-- SCREEN: PROFILE                           -->
<!-- ══════════════════════════════════════════ -->
<div id="screen-profile" class="screen">
  <div class="profile-hero">
    <div class="profile-inner">
      <div class="profile-av" id="prof-av">?</div>
      <div class="profile-info">
        <h2 id="prof-name">Learner</h2>
        <p id="prof-sub">Joined Sparked · STEM Explorer</p>
        <div class="badges-strip" id="prof-badges"></div>
        <div class="level-bar-wrap">
          <div class="level-label"><span id="prof-level">Level 1</span><span id="prof-xp-label">0 / 500 XP</span></div>
          <div class="level-bar"><div class="level-fill" id="prof-level-bar" style="width:0%"></div></div>
        </div>
      </div>
    </div>
  </div>
  <div class="section">
    <div class="section-label">Achievements</div>
    <div class="achievements-grid" id="achievements-grid"></div>
  </div>
</div>

<!-- ══════════════════════════════════════════ -->
<!-- SCREEN: SETTINGS                          -->
<!-- ══════════════════════════════════════════ -->
<div id="screen-settings" class="screen">
  <div class="settings-wrap">
    <h2>Settings</h2>
    <p>Configure your Sparked experience. Your API key is never stored on any server — only in your browser.</p>
    <div class="settings-group">
      <div class="settings-row">
        <div class="settings-label">
          <h4>Your Name</h4>
          <p>Shown on leaderboard and dashboard</p>
        </div>
        <input class="api-in" type="text" id="name-input" placeholder="Enter name" oninput="saveName(this.value)" style="font-family:var(--font)">
      </div>
      <div class="settings-row">
        <div class="settings-label">
          <h4>Anthropic API Key</h4>
          <p>Required to generate AI lessons and use the tutor chatbot</p>
        </div>
        <input class="api-in" type="password" id="api-key-in" placeholder="sk-ant-api03-..." oninput="saveApiKey(this.value)">
      </div>
      <div class="settings-row">
        <div class="settings-label">
          <h4>Sound Effects</h4>
          <p>Play sounds for XP gains and correct answers</p>
        </div>
        <button class="toggle" id="sound-toggle" onclick="toggleSound()"></button>
      </div>
    </div>
    <div class="info-box">
      <strong>🌐 Using on your own domain?</strong><br>
      Upload this HTML file to your web host (works on any static host: Netlify, GitHub Pages, Cloudflare Pages — all free). Point your domain's DNS to your host. For a production API key setup, create a serverless function on Cloudflare Workers (free tier: 100k req/day) to proxy Anthropic API calls so your key stays server-side.<br><br>
      <strong>💡 All features are free:</strong> AI lessons use your own Anthropic API key ($5 credit = hundreds of lessons). Everything else (leaderboard, streaks, challenges, profile, chatbot) works without any backend.
    </div>
    <div style="margin-top:1.5rem;display:flex;gap:.8rem">
      <button class="btn btn-primary" onclick="showScreen('dashboard')">Save & Continue</button>
      <button class="btn btn-ghost" onclick="resetProgress()" style="color:var(--red);border-color:rgba(255,92,92,.3)">Reset Progress</button>
    </div>
  </div>
</div>

<!-- ══════════ AI TUTOR CHATBOT ══════════ -->
<button class="chat-fab" onclick="toggleChat()" id="chat-fab">
  🤖<div class="notif" id="chat-notif">1</div>
</button>
<div class="chat-window" id="chat-win">
  <div class="chat-head">
    <div class="chat-avatar">⚡</div>
    <div class="chat-head-info">
      <h4>Spark — AI Tutor</h4>
      <p>● Online · Ask me anything STEM</p>
    </div>
    <button class="chat-close" onclick="toggleChat()">✕</button>
  </div>
  <div class="chat-messages" id="chat-msgs">
    <div class="msg msg-ai">Hey! I'm <strong>Spark</strong>, your AI STEM tutor 🚀 Ask me anything — I can explain concepts, help with problems, or suggest what to study next!</div>
    <div class="msg msg-ai">Try: <em>"Explain Newton's laws"</em> or <em>"What's the difference between mitosis and meiosis?"</em></div>
  </div>
  <div class="chat-input-row">
    <input class="chat-input" id="chat-in" placeholder="Ask Spark anything..." onkeydown="if(event.key==='Enter')sendChat()">
    <button class="chat-send" onclick="sendChat()">Send</button>
  </div>
</div>

<script>
// ═══════════════════════════════════════════
// STATE
// ═══════════════════════════════════════════
const STATE = {
  name: ls('sparked_name') || '',
  apiKey: ls('sparked_key') || '',
  xp: +ls('sparked_xp') || 0,
  streak: +ls('sparked_streak') || 0,
  lessons: +ls('sparked_lessons') || 0,
  lastLesson: ls('sparked_lastday') || '',
  soundOn: ls('sparked_sound') !== 'off',
  completedChallenges: JSON.parse(ls('sparked_chal') || '[]'),
  currentSubject: '',
  currentCourse: null,
};
function ls(k){return localStorage.getItem(k)}
function lss(k,v){localStorage.setItem(k,String(v))}
function saveState(){
  lss('sparked_name',STATE.name);lss('sparked_key',STATE.apiKey);
  lss('sparked_xp',STATE.xp);lss('sparked_streak',STATE.streak);
  lss('sparked_lessons',STATE.lessons);lss('sparked_lastday',STATE.lastLesson);
  lss('sparked_sound',STATE.soundOn?'on':'off');
  lss('sparked_chal',JSON.stringify(STATE.completedChallenges));
}
function saveName(v){STATE.name=v.trim();saveState();updateNav()}
function saveApiKey(v){STATE.apiKey=v.trim();saveState()}

// ═══════════════════════════════════════════
// COURSES DATA
// ═══════════════════════════════════════════
const COURSES = [
  {s:'Mathematics',icon:'📐',title:'Introduction to Calculus',level:'beginner',desc:'Limits, derivatives, and integrals from the ground up.',lessons:8,mins:45,xp:200},
  {s:'Mathematics',icon:'📐',title:'Linear Algebra',level:'intermediate',desc:'Vectors, matrices, and eigenvalues — backbone of modern AI.',lessons:10,mins:60,xp:300},
  {s:'Mathematics',icon:'📐',title:'Probability & Statistics',level:'intermediate',desc:'Distributions, inference, and Bayesian thinking.',lessons:9,mins:50,xp:280},
  {s:'Mathematics',icon:'📐',title:'Abstract Algebra',level:'advanced',desc:'Groups, rings, and fields — the deep structure of math.',lessons:12,mins:70,xp:400},
  {s:'Mathematics',icon:'📐',title:'Number Theory',level:'advanced',desc:'Primes, congruences, and the secrets of integers.',lessons:8,mins:55,xp:350},
  {s:'Physics',icon:'⚛️',title:'Classical Mechanics',level:'beginner',desc:"Newton's laws, energy, and momentum explained.",lessons:8,mins:50,xp:200},
  {s:'Physics',icon:'⚛️',title:'Electromagnetism',level:'intermediate',desc:"Maxwell's equations and the nature of fields.",lessons:10,mins:65,xp:320},
  {s:'Physics',icon:'⚛️',title:'Quantum Mechanics',level:'advanced',desc:'Wave functions, uncertainty, and quantum weirdness.',lessons:14,mins:80,xp:500},
  {s:'Physics',icon:'⚛️',title:'Thermodynamics',level:'intermediate',desc:'Heat, entropy, and the laws of energy.',lessons:9,mins:55,xp:290},
  {s:'Chemistry',icon:'🧪',title:'Atomic Structure',level:'beginner',desc:'Electrons, orbitals, and the periodic table.',lessons:6,mins:40,xp:180},
  {s:'Chemistry',icon:'🧪',title:'Organic Chemistry I',level:'intermediate',desc:'Functional groups and reaction mechanisms.',lessons:12,mins:60,xp:340},
  {s:'Chemistry',icon:'🧪',title:'Chemical Thermodynamics',level:'advanced',desc:'Gibbs energy and spontaneous reactions.',lessons:10,mins:70,xp:380},
  {s:'Biology',icon:'🧬',title:'Cell Biology',level:'beginner',desc:'Organelles, division, and the machinery of life.',lessons:8,mins:45,xp:200},
  {s:'Biology',icon:'🧬',title:'Genetics & DNA',level:'intermediate',desc:'Inheritance, mutation, and gene expression.',lessons:10,mins:55,xp:290},
  {s:'Biology',icon:'🧬',title:'Molecular Biology',level:'advanced',desc:'Gene regulation, CRISPR, and modern biotech.',lessons:11,mins:65,xp:420},
  {s:'Biology',icon:'🧬',title:'Ecology & Evolution',level:'beginner',desc:'Natural selection, ecosystems, and biodiversity.',lessons:7,mins:40,xp:190},
  {s:'Computer Science',icon:'💻',title:'Algorithms & Data Structures',level:'intermediate',desc:'Sorting, graphs, trees, and complexity.',lessons:14,mins:70,xp:360},
  {s:'Computer Science',icon:'💻',title:'Machine Learning Basics',level:'intermediate',desc:'Regression, classification, and neural networks.',lessons:12,mins:75,xp:400},
  {s:'Computer Science',icon:'💻',title:'Operating Systems',level:'advanced',desc:'Processes, memory, concurrency, and kernels.',lessons:13,mins:80,xp:450},
  {s:'Computer Science',icon:'💻',title:'Web Development',level:'beginner',desc:'HTML, CSS, JavaScript, and how the web works.',lessons:10,mins:50,xp:240},
  {s:'Engineering',icon:'⚙️',title:'Circuit Analysis',level:'beginner',desc:"Ohm's law, Kirchhoff's laws, and circuit design.",lessons:8,mins:50,xp:220},
  {s:'Engineering',icon:'⚙️',title:'Control Systems',level:'advanced',desc:'PID controllers, Laplace transforms, and feedback.',lessons:11,mins:75,xp:440},
  {s:'Engineering',icon:'⚙️',title:'Fluid Mechanics',level:'intermediate',desc:"Bernoulli's principle, viscosity, and flow.",lessons:9,mins:60,xp:300},
];

const CHALLENGES = [
  {id:'c1',title:'Derivative Speed Round',desc:'Solve 3 differentiation problems in under 2 minutes.',subject:'Mathematics',xp:150,tags:['Calculus','Timed']},
  {id:'c2',title:'Quantum Concept Quiz',desc:'Answer 5 questions about wave-particle duality.',subject:'Physics',xp:120,tags:['Quantum','Quiz']},
  {id:'c3',title:'DNA Replication Explainer',desc:'Ask the AI tutor to explain DNA replication, then quiz yourself.',subject:'Biology',xp:100,tags:['Genetics','AI']},
  {id:'c4',title:'Big-O Challenge',desc:'Identify the time complexity of 4 algorithm snippets.',subject:'Computer Science',xp:130,tags:['Algorithms','Logic']},
  {id:'c5',title:'Organic Reaction Match',desc:'Match 6 functional group reactions to their products.',subject:'Chemistry',xp:110,tags:['Organic','Matching']},
  {id:'c6',title:'Circuit Puzzle',desc:'Find the equivalent resistance of a complex circuit.',subject:'Engineering',xp:140,tags:['Circuits','Problem-Solving']},
];

const LEADERBOARD = [
  {name:'Aiko T.',subject:'Quantum Physics',xp:12480,av:'🦊'},
  {name:'Marcus R.',subject:'Machine Learning',xp:11230,av:'🐯'},
  {name:'Priya S.',subject:'Organic Chemistry',xp:9840,av:'🦋'},
  {name:'Dev K.',subject:'Abstract Algebra',xp:8760,av:'🦅'},
  {name:'Lena H.',subject:'Molecular Biology',xp:7920,av:'🌙'},
  {name:'Omar F.',subject:'Control Systems',xp:6540,av:'⚡'},
  {name:'Yuki N.',subject:'Algorithms',xp:5890,av:'🎯'},
  {name:'Sofia M.',subject:'Thermodynamics',xp:4320,av:'🔥'},
];

const ACHIEVEMENTS = [
  {icon:'🔥',name:'First Spark',desc:'Complete your first lesson',xpReq:1,type:'lessons'},
  {icon:'⚡',name:'On Fire',desc:'Complete 5 lessons',xpReq:5,type:'lessons'},
  {icon:'🧠',name:'Big Brain',desc:'Earn 500 XP',xpReq:500,type:'xp'},
  {icon:'💎',name:'Diamond Mind',desc:'Earn 2000 XP',xpReq:2000,type:'xp'},
  {icon:'📅',name:'Consistent',desc:'3-day streak',xpReq:3,type:'streak'},
  {icon:'🏆',name:'Scholar',desc:'Complete 10 lessons',xpReq:10,type:'lessons'},
  {icon:'🚀',name:'Rocket Launch',desc:'Earn 1000 XP',xpReq:1000,type:'xp'},
  {icon:'👑',name:'STEM King/Queen',desc:'Earn 5000 XP',xpReq:5000,type:'xp'},
];

// ═══════════════════════════════════════════
// ONBOARDING
// ═══════════════════════════════════════════
function onboard(){
  if(STATE.name){showScreen('dashboard');updateAll();return}
  const name = prompt('Welcome to Sparked! What\'s your name?','');
  if(name){STATE.name=name.trim()||'Learner';saveState()}
  else{STATE.name='Learner';saveState()}
  const key = prompt('Enter your Anthropic API key to unlock AI lessons (get one free at console.anthropic.com).\n\nPress Cancel to explore without AI:','');
  if(key&&key.trim().startsWith('sk-')){STATE.apiKey=key.trim();saveState()}
  showScreen('dashboard');updateAll();
}

function updateAll(){
  document.getElementById('nav-xp').textContent=STATE.xp;
  document.getElementById('nav-streak').textContent=STATE.streak+'d';
  const initials = STATE.name?STATE.name.charAt(0).toUpperCase():'?';
  document.getElementById('nav-av').textContent=initials;
  document.getElementById('dash-name').textContent=STATE.name||'Learner';
  document.getElementById('dash-streak-txt').textContent=STATE.streak+'-day';
  document.getElementById('d-xp').textContent=STATE.xp;
  document.getElementById('d-lessons').textContent=STATE.lessons;
  document.getElementById('d-streak').textContent=STATE.streak;
  const myRank = LEADERBOARD.filter(l=>l.xp>STATE.xp).length+1;
  document.getElementById('d-rank').textContent='#'+myRank;
  buildStreakBar();
  // profile
  document.getElementById('prof-av').textContent=initials;
  document.getElementById('prof-name').textContent=STATE.name||'Learner';
  const lvl=Math.floor(STATE.xp/500)+1;
  const lvlXp=STATE.xp%500;
  document.getElementById('prof-level').textContent='Level '+lvl;
  document.getElementById('prof-xp-label').textContent=lvlXp+' / 500 XP';
  document.getElementById('prof-level-bar').style.width=(lvlXp/5)+'%';
  // settings
  document.getElementById('name-input').value=STATE.name;
  document.getElementById('api-key-in').value=STATE.apiKey;
  document.getElementById('sound-toggle').className='toggle'+(STATE.soundOn?' on':'');
  buildAchievements();
  buildBadges();
}
function updateNav(){
  document.getElementById('nav-xp').textContent=STATE.xp;
  document.getElementById('nav-streak').textContent=STATE.streak+'d';
  document.getElementById('nav-av').textContent=(STATE.name||'?').charAt(0).toUpperCase();
  document.getElementById('dash-name').textContent=STATE.name||'Learner';
}

function buildStreakBar(){
  const bar=document.getElementById('streak-bar');
  const days=['M','T','W','T','F','S','S'];
  bar.innerHTML=days.map((d,i)=>`<div class="streak-day${i<STATE.streak?' done':i===STATE.streak?' today':''}">${d}</div>`).join('');
}

function buildAchievements(){
  const grid=document.getElementById('achievements-grid');
  grid.innerHTML=ACHIEVEMENTS.map(a=>{
    const val=a.type==='xp'?STATE.xp:a.type==='lessons'?STATE.lessons:STATE.streak;
    const earned=val>=a.xpReq;
    return`<div class="ach-card${earned?' earned':''}">
      <div class="ach-icon">${a.icon}</div>
      <div class="ach-name">${a.name}</div>
      <div class="ach-desc">${a.desc}</div>
    </div>`;
  }).join('');
}

function buildBadges(){
  const earned=ACHIEVEMENTS.filter(a=>{
    const val=a.type==='xp'?STATE.xp:a.type==='lessons'?STATE.lessons:STATE.streak;
    return val>=a.xpReq;
  });
  document.getElementById('prof-badges').innerHTML=earned.map(a=>`<div class="badge-item gold">${a.icon} ${a.name}</div>`).join('');
}

// ═══════════════════════════════════════════
// SCREEN ROUTING
// ═══════════════════════════════════════════
function showScreen(name){
  document.querySelectorAll('.screen').forEach(s=>s.classList.remove('active'));
  document.getElementById('screen-'+name).classList.add('active');
  document.querySelectorAll('.nav-tab').forEach(t=>t.classList.remove('active'));
  const tabs={'dashboard':'Dashboard','learn':'Learn','challenges':'Challenges','leaderboard':'Leaderboard'};
  document.querySelectorAll('.nav-tab').forEach(t=>{if(t.textContent===tabs[name])t.classList.add('active')});
  window.scrollTo(0,0);
  if(name==='learn')buildCourseGrid('all');
  if(name==='challenges')buildChallenges();
  if(name==='leaderboard')buildLeaderboard();
  if(name==='dashboard'||name==='profile')updateAll();
}

// ═══════════════════════════════════════════
// COURSES
// ═══════════════════════════════════════════
function buildCourseGrid(filter){
  const grid=document.getElementById('course-grid');
  const list=filter==='all'?COURSES:COURSES.filter(c=>c.s===filter);
  grid.innerHTML=list.map(c=>`
    <div class="course-card">
      <div class="cc-level cc-lvl-${c.level.charAt(0)}">${c.level.toUpperCase()}</div>
      <div class="cc-title">${c.icon} ${c.title}</div>
      <div class="cc-desc">${c.desc}</div>
      <div class="cc-meta"><span>📖 ${c.lessons} lessons</span><span>⏱ ~${c.mins}m</span><span>⚡ ${c.xp} XP</span></div>
      <div class="cc-progress"><div class="cc-progress-fill" style="width:0%"></div></div>
      <button class="cc-start" onclick='startCourse(${JSON.stringify(c).replace(/'/g,"&#39;")})'>Start with AI →</button>
    </div>`).join('');
}

function filterCourses(sub,btn){
  document.querySelectorAll('.stab').forEach(b=>b.classList.remove('active'));
  btn.classList.add('active');
  buildCourseGrid(sub);
}

function startCourse(course){
  STATE.currentCourse=course;
  document.getElementById('lesson-back').onclick=()=>showScreen('learn');
  showScreen('lesson');
  generateLesson(course.s,course.title,course.level,'#lesson-out');
}

function showCustomLesson(){
  const topic=prompt('What STEM topic do you want to learn?\n\nExamples:\n• How does CRISPR work?\n• Explain gradient descent\n• What is entropy?');
  if(!topic)return;
  const levels=['Beginner','Intermediate','Advanced'];
  const level=levels[Math.floor(Math.random()*2)].toLowerCase();
  const course={s:'Science',title:topic,level,xp:200};
  STATE.currentCourse=course;
  document.getElementById('lesson-back').onclick=()=>showScreen('dashboard');
  showScreen('lesson');
  generateLesson('Science',topic,level,'#lesson-out');
}

// ═══════════════════════════════════════════
// AI LESSON GENERATION
// ═══════════════════════════════════════════
async function generateLesson(subject, topic, level, selector){
  const out=document.querySelector(selector);
  if(!out)return;
  if(!STATE.apiKey){
    out.innerHTML=`<div class="err-box">⚠ No API key set. Go to ⚙ Settings to add your free Anthropic API key, then come back!</div>
    <div style="margin-top:1rem"><button class="btn btn-primary" onclick="showScreen('settings')">Go to Settings →</button></div>`;
    return;
  }
  out.innerHTML=`<div class="loading-box"><div class="spin"></div>Spark AI is generating your <strong style="color:var(--text)">${topic}</strong> lesson…</div>`;
  document.getElementById('lesson-progress').style.width='30%';
  document.getElementById('lesson-step').textContent='Generating…';

  const prompt=`You are Spark, an expert STEM tutor on "Sparked" — an engaging learning platform. Generate a comprehensive, exciting lesson on: "${topic}" (Subject: ${subject}, Level: ${level}).

Structure EXACTLY as follows:
1. Two-sentence engaging intro paragraph
2. ### Core Concepts
   - 3 key ideas explained clearly with examples
3. If math/physics/cs: one key formula/equation wrapped in [FORMULA]...[/FORMULA]
4. ### Real-World Application
   - One vivid, surprising real-world example that makes it click
5. A mind-blowing insight wrapped in [INSIGHT]key insight here[/INSIGHT]
6. ### Summary
   - 3 bullet points of what we learned (use - for bullets)

Then provide a quiz question in EXACT format:
[QUIZ]
Question: (specific question testing understanding)
A: (option)
B: (option)
C: (option)
D: (option)
Answer: (single letter)
Explanation: (one clear sentence)
[/QUIZ]

Tone: genuinely engaging, occasionally witty, ${level} level. Use **bold** for key terms. Make the student excited to learn more!`;

  try{
    const res=await fetch('https://api.anthropic.com/v1/messages',{
      method:'POST',
      headers:{'Content-Type':'application/json','x-api-key':STATE.apiKey,'anthropic-version':'2023-06-01','anthropic-dangerous-direct-browser-access':'true'},
      body:JSON.stringify({model:'claude-sonnet-4-20250514',max_tokens:1400,messages:[{role:'user',content:prompt}]})
    });
    const data=await res.json();
    if(data.error)throw new Error(data.error.message);
    const text=data.content.map(b=>b.text||'').join('');
    document.getElementById('lesson-progress').style.width='100%';
    document.getElementById('lesson-step').textContent='Done!';
    renderLesson(subject,topic,level,text,out);
    awardXP(STATE.currentCourse?.xp||150,'Lesson Complete!');
    STATE.lessons++;
    STATE.lastLesson=new Date().toDateString();
    if(STATE.streak<7)STATE.streak++;
    saveState();updateAll();
  }catch(e){
    out.innerHTML=`<div class="err-box">⚠ AI Error: ${e.message}<br><br>Check your API key in Settings. Get a free key at <strong>console.anthropic.com</strong></div>`;
  }
}

function renderLesson(subject,topic,level,raw,container){
  // extract quiz
  const qm=raw.match(/\[QUIZ\]([\s\S]*?)\[\/QUIZ\]/);
  let quiz=null;
  if(qm){
    const qb=qm[1];
    const q=qb.match(/Question:\s*(.+)/);
    const a=qb.match(/A:\s*(.+)/),b=qb.match(/B:\s*(.+)/),c=qb.match(/C:\s*(.+)/),d=qb.match(/D:\s*(.+)/);
    const ans=qb.match(/Answer:\s*([ABCD])/);
    const exp=qb.match(/Explanation:\s*(.+)/s);
    if(q&&a&&b&&c&&d&&ans)quiz={q:q[1].trim(),opts:[a[1].trim(),b[1].trim(),c[1].trim(),d[1].trim()],ans:ans[1].trim(),exp:exp?exp[1].trim():''};
    raw=raw.replace(/\[QUIZ\][\s\S]*?\[\/QUIZ\]/,'');
  }
  const lid='qz'+Date.now();
  let body=raw
    .replace(/\[FORMULA\]([\s\S]*?)\[\/FORMULA\]/g,'</p><div class="formula-box">$1</div><p>')
    .replace(/\[INSIGHT\]([\s\S]*?)\[\/INSIGHT\]/g,'</p><div class="insight-box"><em>💡 Insight</em><br>$1</div><p>')
    .replace(/^###\s*(.+)$/gm,'</p><h3>$1</h3><p>')
    .replace(/^- (.+)$/gm,'</p><p>• $1</p><p>')
    .replace(/\*\*(.+?)\*\*/g,'<strong>$1</strong>')
    .replace(/\n\n+/g,'</p><p>')
    .replace(/\n/g,' ');

  let html=`<div class="lesson-hdr">
    <div class="lesson-tag">${subject} · ${level}</div>
    <div class="lesson-title">${topic}</div>
    <div class="lesson-meta"><span>✦ AI Generated</span><span>⚡ ${STATE.currentCourse?.xp||150} XP</span><span>~8 min</span></div>
  </div>
  <div class="lesson-body"><p>${body}</p></div>`;

  if(quiz){
    const letters=['A','B','C','D'];
    html+=`<div class="quiz-block">
      <div class="quiz-label">✦ Quick Knowledge Check</div>
      <div class="quiz-q">${quiz.q}</div>
      <div class="quiz-opts">
        ${quiz.opts.map((o,i)=>`<button class="qopt" id="${lid}_${i}" onclick="checkQ('${lid}',${i},'${letters[i]}','${quiz.ans}','${(quiz.exp||'').replace(/'/g,"\\'")}')">${letters[i]}. ${o}</button>`).join('')}
      </div>
      <div class="quiz-fb" id="${lid}_fb"></div>
    </div>`;
  }

  html+=`<div class="lesson-nav">
    <button class="btn btn-ghost" onclick="history.back()">← Previous</button>
    <button class="btn btn-primary" onclick="showScreen('challenges')">Try a Challenge ⚡</button>
  </div>`;

  container.innerHTML=html;
}

function checkQ(lid,idx,letter,correct,explanation){
  const letters=['A','B','C','D'];
  for(let i=0;i<4;i++){
    const btn=document.getElementById(`${lid}_${i}`);
    if(!btn)continue;
    btn.disabled=true;
    if(letters[i]===correct)btn.classList.add('correct');
    else if(i===idx&&letters[i]!==correct)btn.classList.add('wrong');
  }
  const fb=document.getElementById(lid+'_fb');
  if(letter===correct){
    fb.style.cssText='background:rgba(62,207,178,.1);border:1px solid rgba(62,207,178,.3);color:var(--teal);border-radius:8px;padding:.8rem 1rem;';
    fb.textContent='✓ Correct! '+explanation;
    awardXP(50,'Correct Answer!');
  }else{
    fb.style.cssText='background:rgba(255,92,92,.08);border:1px solid rgba(255,92,92,.25);color:var(--red);border-radius:8px;padding:.8rem 1rem;';
    fb.textContent='✗ Not quite. Answer: '+correct+'. '+explanation;
  }
  fb.classList.add('show');
}

// ═══════════════════════════════════════════
// XP SYSTEM
// ═══════════════════════════════════════════
function awardXP(amount,reason){
  STATE.xp+=amount;saveState();
  document.getElementById('nav-xp').textContent=STATE.xp;
  showToast('+'+amount+' XP — '+reason);
}

function showToast(msg){
  const el=document.createElement('div');
  el.className='xp-toast';el.textContent=msg;
  document.body.appendChild(el);
  setTimeout(()=>el.remove(),2500);
}

// ═══════════════════════════════════════════
// CHALLENGES
// ═══════════════════════════════════════════
function buildChallenges(){
  const grid=document.getElementById('challenge-grid');
  grid.innerHTML=CHALLENGES.map(c=>{
    const done=STATE.completedChallenges.includes(c.id);
    return`<div class="chal-card${done?' ':''}" onclick="${done?'':
      `completeChallenge('${c.id}','${c.title}','${c.subject}',${c.xp})`}">
      <div class="chal-xp">⚡ +${c.xp} XP ${done?'· ✓ Done':''}</div>
      <div class="chal-title">${c.title}</div>
      <div class="chal-desc">${c.desc}</div>
      <div class="chal-tags">${c.tags.map(t=>`<div class="tag">${t}</div>`).join('')}</div>
      ${!done?`<button class="cc-start" style="margin-top:.9rem">Start Challenge →</button>`:`<div style="margin-top:.9rem;font-size:.78rem;color:var(--teal);font-weight:700">✓ Completed today</div>`}
    </div>`;
  }).join('');
  startTimer();
}

function completeChallenge(id,title,subject,xp){
  showScreen('lesson');
  STATE.completedChallenges.push(id);saveState();
  document.getElementById('lesson-back').onclick=()=>{showScreen('challenges');buildChallenges()};
  generateLesson(subject,title,'intermediate','#lesson-out');
  awardXP(xp,'Challenge: '+title);
}

let timerInterval;
function startTimer(){
  clearInterval(timerInterval);
  function tick(){
    const now=new Date();
    const midnight=new Date(now);
    midnight.setHours(24,0,0,0);
    const diff=midnight-now;
    const h=String(Math.floor(diff/3600000)).padStart(2,'0');
    const m=String(Math.floor((diff%3600000)/60000)).padStart(2,'0');
    const s=String(Math.floor((diff%60000)/1000)).padStart(2,'0');
    const el=document.getElementById('ch-timer');
    if(el)el.textContent=`${h}:${m}:${s}`;
  }
  tick();timerInterval=setInterval(tick,1000);
}

// ═══════════════════════════════════════════
// LEADERBOARD
// ═══════════════════════════════════════════
function buildLeaderboard(){
  const allPlayers=[...LEADERBOARD,{name:STATE.name||'You',subject:'STEM',xp:STATE.xp,av:'⭐',isMe:true}]
    .sort((a,b)=>b.xp-a.xp);
  const top3=allPlayers.slice(0,3);
  const rest=allPlayers.slice(3);
  const pClasses=['p2','p1','p3'];
  const pLabels=['2nd','1st','3rd'];
  const reordered=[top3[1],top3[0],top3[2]];
  document.getElementById('lb-podium').innerHTML=reordered.filter(Boolean).map((p,i)=>`
    <div class="podium-item ${pClasses[i]}">
      <div class="podium-avatar">${p.av||p.name.charAt(0)}</div>
      <div class="podium-name">${p.name}</div>
      <div class="podium-xp">⚡ ${p.xp.toLocaleString()} XP</div>
      <div class="podium-rank">${pLabels[i]}</div>
      <div class="podium-bar"></div>
    </div>`).join('');
  document.getElementById('lb-list').innerHTML=allPlayers.map((p,i)=>`
    <div class="lb-row${p.isMe?' me':''}">
      <div class="lb-pos">${i+1}</div>
      <div class="lb-av">${p.av||p.name.charAt(0)}</div>
      <div class="lb-name">${p.name}${p.isMe?' (You)':''}<br><span class="lb-subject">${p.subject}</span></div>
      <div class="lb-score">⚡ ${p.xp.toLocaleString()}</div>
    </div>`).join('');
}

// ═══════════════════════════════════════════
// AI TUTOR CHATBOT
// ═══════════════════════════════════════════
let chatOpen=false;
const chatHistory=[];

function toggleChat(){
  chatOpen=!chatOpen;
  document.getElementById('chat-win').classList.toggle('open',chatOpen);
  document.getElementById('chat-notif').style.display='none';
}
function openChat(){toggleChat();if(!chatOpen)toggleChat();}

async function sendChat(){
  const input=document.getElementById('chat-in');
  const msg=input.value.trim();
  if(!msg)return;
  input.value='';
  appendMsg(msg,'user');
  chatHistory.push({role:'user',content:msg});
  const typing=appendTyping();
  if(!STATE.apiKey){
    typing.remove();
    appendMsg("I'd love to help! Please add your Anthropic API key in ⚙ Settings first. It's free to get at console.anthropic.com","ai");
    return;
  }
  try{
    const res=await fetch('https://api.anthropic.com/v1/messages',{
      method:'POST',
      headers:{'Content-Type':'application/json','x-api-key':STATE.apiKey,'anthropic-version':'2023-06-01','anthropic-dangerous-direct-browser-access':'true'},
      body:JSON.stringify({
        model:'claude-sonnet-4-20250514',
        max_tokens:600,
        system:'You are Spark, a friendly and enthusiastic AI STEM tutor on the Sparked learning platform. You explain concepts clearly, use analogies, and encourage students. Keep answers concise (2-4 sentences usually). Use occasional emojis. If asked about non-STEM topics, gently redirect to STEM learning.',
        messages:chatHistory.slice(-8)
      })
    });
    const data=await res.json();
    typing.remove();
    if(data.error)throw new Error(data.error.message);
    const reply=data.content.map(b=>b.text||'').join('');
    chatHistory.push({role:'assistant',content:reply});
    appendMsg(reply,'ai');
    awardXP(10,'Asked the Tutor');
  }catch(e){
    typing.remove();
    appendMsg('Oops, something went wrong: '+e.message,'ai');
  }
}

function appendMsg(text,role){
  const msgs=document.getElementById('chat-msgs');
  const div=document.createElement('div');
  div.className='msg msg-'+role;
  div.innerHTML=text.replace(/\*\*(.+?)\*\*/g,'<strong>$1</strong>').replace(/\n/g,'<br>');
  msgs.appendChild(div);
  msgs.scrollTop=msgs.scrollHeight;
  return div;
}
function appendTyping(){
  const msgs=document.getElementById('chat-msgs');
  const div=document.createElement('div');
  div.className='msg-typing';
  div.innerHTML='<span></span><span></span><span></span>';
  msgs.appendChild(div);
  msgs.scrollTop=msgs.scrollHeight;
  return div;
}

// ═══════════════════════════════════════════
// SETTINGS / UTILS
// ═══════════════════════════════════════════
function toggleSound(){
  STATE.soundOn=!STATE.soundOn;saveState();
  document.getElementById('sound-toggle').className='toggle'+(STATE.soundOn?' on':'');
}
function resetProgress(){
  if(!confirm('Reset all XP, streak, and progress? This cannot be undone.'))return;
  STATE.xp=0;STATE.streak=0;STATE.lessons=0;STATE.completedChallenges=[];saveState();updateAll();
  showToast('Progress reset.');
}
function navToSettings(){showScreen('settings')}

// ═══════════════════════════════════════════
// INIT
// ═══════════════════════════════════════════
updateAll();
// Add settings link in nav avatar context
document.getElementById('nav-av').addEventListener('contextmenu',e=>{e.preventDefault();showScreen('settings')});
document.getElementById('nav-av').title='Click: Profile | Right-click: Settings';
// Build course grid on first load if visiting learn
</script>
</body>
</html>
