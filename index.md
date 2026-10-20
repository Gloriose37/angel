<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0,maximum-scale=1.0,user-scalable=no">
<title>PSEROS · 无声沉沦</title>
<style>
:root {
  --bg: #08080a;
  --gold: #c5a059;
  --gold-dim: rgba(197,160,89,0.3);
  --gold-glow: rgba(197,160,89,0.12);
  --text: #dcd5c6;
  --sub: #a0a5b5;
  --danger: #b0455a;
  --layer: #0f0f14;
  --layer2: #16161e;
  --font-en: Georgia, "Times New Roman", serif;
  --font-cn: "Songti SC", "SimSun", "STSong", serif;
  --font-sans: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
  --ease-out: cubic-bezier(.22,.61,.36,1);
  --ease-std: cubic-bezier(.4,0,.2,1);
}

* { margin: 0; padding: 0; box-sizing: border-box; }
html { scroll-behavior: auto; }

body {
  background-color: var(--bg);
  color: var(--text); font-family: var(--font-cn); line-height: 1.8;
  overflow-x: hidden;
  overflow-y: auto;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.85' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.045'/%3E%3C/svg%3E");
  -webkit-tap-highlight-color: transparent;
  height: 100vh;
}

body::after {
  content: ""; position: fixed; inset: 0; pointer-events: none; z-index: 99;
  background: radial-gradient(circle at 50% 40%, transparent 20%, rgba(0,0,0,0.85) 100%);
}

::-webkit-scrollbar { width: 4px; }
::-webkit-scrollbar-track { background: var(--bg); }
::-webkit-scrollbar-thumb { background: var(--gold-dim); }

/* ========== 翻页系统 ========== */
.page {
  position: fixed; inset: 0;
  display: flex; flex-direction: column; justify-content: center; align-items: center;
  padding: 60px 20px;
  opacity: 0; visibility: hidden;
  transition: opacity .7s var(--ease-out), visibility .7s;
  overflow-y: auto;
  z-index: 1;
}
.page.active {
  opacity: 1; visibility: visible;
  z-index: 10;
}
.inner { max-width: 720px; width: 100%; position: relative; z-index: 2; }

/* ========== 通用 ========== */
.en {
  font-family: var(--font-en); font-size: 11px; letter-spacing: 0.45em;
  color: var(--gold); text-align: center; margin-bottom: 14px;
  text-transform: uppercase;
}
.cn-title {
  font-size: 24px; letter-spacing: 0.14em; text-align: center;
  margin-bottom: 30px; text-indent: 0.14em;
  text-shadow: 0 0 20px rgba(197,160,89,0.25);
  font-weight: 400;
}

.divider {
  width: 100%; height: 1px; margin: 36px 0;
  background: linear-gradient(90deg, transparent, var(--gold-dim) 20%, var(--gold-dim) 80%, transparent);
  position: relative;
}
.divider::after {
  content: "✦"; position: absolute; left: 50%; top: 50%;
  transform: translate(-50%, -50%); font-size: 10px; color: var(--gold-dim);
  background: var(--bg); padding: 0 8px; line-height: 1;
}

.card {
  background: rgba(255,255,255,.028);
  border: 1px solid rgba(255,255,255,.06);
  padding: 30px;
  position: relative;
  box-shadow: inset 0 1px 0 rgba(255,255,255,.05), 0 0 40px rgba(0,0,0,.5);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
}
.card::before, .card::after {
  content: ""; position: absolute; width: 10px; height: 10px; border: 1px solid var(--gold);
  opacity: .6;
}
.card::before { top: -1px; left: -1px; border-right: 0; border-bottom: 0; }
.card::after { bottom: -1px; right: -1px; border-left: 0; border-top: 0; }

.reveal {
  opacity: 0; transform: translateY(22px);
  transition: opacity .8s var(--ease-out), transform .8s var(--ease-out);
}
.page.active .reveal { opacity: 1; transform: translateY(0); }
.page.active .reveal:nth-child(1) { transition-delay: 0ms; }
.page.active .reveal:nth-child(2) { transition-delay: 80ms; }
.page.active .reveal:nth-child(3) { transition-delay: 160ms; }
.page.active .reveal:nth-child(4) { transition-delay: 240ms; }
.page.active .reveal:nth-child(5) { transition-delay: 320ms; }
.page.active .reveal:nth-child(6) { transition-delay: 400ms; }

/* ========== 封面 ========== */
#page0 {
  padding: 0; align-items: center; text-align: center;
  cursor: pointer;
  overflow: hidden;
}
.bg-img {
  position: absolute; inset: 0;
  background:
    radial-gradient(ellipse at 50% 30%, rgba(197,160,89,0.08) 0%, transparent 55%),
    radial-gradient(ellipse at 20% 80%, rgba(176,69,90,0.05) 0%, transparent 50%),
    linear-gradient(180deg, rgba(10,10,15,0.3), rgba(5,5,8,1));
  filter: grayscale(0.2) contrast(1.1); z-index: 0;
}
.bg-img::after {
  content: ""; position: absolute; inset: 0;
  background: radial-gradient(circle at 50% 45%, rgba(197,160,89,0.06) 0%, transparent 40%);
  animation: breathe 6s ease-in-out infinite;
}
@keyframes breathe {
  0%, 100% { opacity: 0.5; transform: scale(1); }
  50% { opacity: 1; transform: scale(1.08); }
}

#page0 h1 {
  font-family: var(--font-en);
  font-size: clamp(2.2rem, 9vw, 4.2rem);
  letter-spacing: 0.18em; color: #fff; z-index: 2;
  text-indent: 0.18em;
  font-weight: 400;
  display: flex; justify-content: center; flex-wrap: wrap;
}
#page0 h1 .letter {
  display: inline-block;
  transition: transform 0.5s var(--ease-out), color 0.4s var(--ease-std), text-shadow 0.4s var(--ease-std);
  text-shadow: 0 0 30px rgba(197,160,89,0.15);
}
#page0 h1 .letter:hover {
  color: var(--gold);
  text-shadow: 0 0 12px rgba(197,160,89,0.6), 0 0 40px rgba(197,160,89,0.3);
  transform: translateY(-6px) scale(1.05);
}

#page0 p {
  font-size: 1.05rem; letter-spacing: 0.6em; color: var(--gold);
  margin-top: 18px; margin-left: 0.6em; z-index: 2; text-indent: 0.6em;
}
.cover-sub {
  margin-top: 42px; font-size: 12px; letter-spacing: 0.2em; color: var(--sub);
  z-index: 2; max-width: 320px; line-height: 2; opacity: 0.8;
  font-style: italic;
}
.tap-hint {
  margin-top: 56px; font-size: 11px; letter-spacing: 0.3em; color: var(--sub);
  z-index: 2; animation: pulse 2.8s infinite; cursor: pointer;
}
@keyframes pulse { 0%, 100% { opacity: 0.25; } 50% { opacity: 1; } }

/* ========== 档案 ========== */
.row {
  display: flex; justify-content: space-between; align-items: center;
  border-bottom: 1px solid rgba(255,255,255,.06);
  padding: 15px 0;
}
.row:last-child { border-bottom: 0; }
.k {
  color: var(--gold); font-size: 0.82rem; font-family: var(--font-en);
  letter-spacing: 0.12em; text-transform: uppercase;
}
.v {
  text-align: right; font-size: 0.95rem; color: var(--text);
  font-variant-numeric: tabular-nums;
}

/* ========== 风格 ========== */
.style-grid {
  display: grid; grid-template-columns: 1fr 1fr; gap: 12px;
}
.style-item {
  display: flex; flex-direction: column; align-items: center; justify-content: center;
  padding: 26px 16px;
  background: rgba(255,255,255,.015);
  border: 1px solid rgba(255,255,255,.06);
  cursor: pointer; position: relative; overflow: hidden;
  transition: transform .3s var(--ease-out), border-color .3s var(--ease-std), background .3s var(--ease-std), box-shadow .3s var(--ease-std);
  text-align: center;
  border-radius: 1px;
}
.style-item:hover {
  transform: translateY(-4px);
  border-color: var(--gold-dim);
  background: var(--gold-glow);
  box-shadow: 0 0 8px rgba(197,160,89,0.08), 0 0 34px rgba(197,160,89,0.06);
}
.style-item:active { transform: scale(.97); }
.style-item:focus-visible { outline: 2px solid var(--gold); outline-offset: 2px; }
.style-item .s-icon {
  font-size: 1.5rem; margin-bottom: 10px; color: var(--gold);
  font-style: normal; line-height: 1;
}
.style-item .s-name {
  font-size: 1.1rem; letter-spacing: 0.12em; color: var(--text);
  font-family: var(--font-cn);
}
.style-item .s-en {
  font-family: var(--font-sans); font-size: 0.52rem; color: var(--sub);
  letter-spacing: 0.18em; text-transform: uppercase; margin-top: 5px;
}

/* ========== 须知页（独立页面） ========== */
#page3 .inner {
  max-width: 720px;
  padding-top: 8px;
}
#page3 .en {
  position: relative;
  z-index: 3;
  margin-top: 0;
}
#page3 .cn-title {
  position: relative;
  z-index: 3;
  margin-top: 0;
}
.notice-content {
  padding: 30px 32px;
  font-size: 0.92rem;
  line-height: 2.1;
  letter-spacing: 0.03em;
  color: var(--sub);
  margin-top: 0;
  position: relative;
  z-index: 2;
}
.notice-content p {
  margin-bottom: 14px;
}
.notice-content p:last-child {
  margin-bottom: 0;
}
.notice-content .notice-first {
  color: var(--gold);
  font-family: var(--font-en);
  font-size: 0.85rem;
  letter-spacing: 0.15em;
  margin-bottom: 20px;
  text-transform: uppercase;
}

/* 弹窗 */
.modal-overlay {
  position: fixed; inset: 0; z-index: 1000;
  background: rgba(0,0,0,.72);
  backdrop-filter: blur(6px);
  -webkit-backdrop-filter: blur(6px);
  display: flex; align-items: center; justify-content: center;
  padding: 24px;
  opacity: 0; pointer-events: none;
  transition: opacity .35s var(--ease-std);
}
.modal-overlay.open { opacity: 1; pointer-events: auto; }
.modal-box {
  max-width: 500px; width: 100%;
  background: var(--layer2);
  border: 1px solid rgba(197,160,89,.25);
  padding: 36px 28px 30px;
  position: relative;
  box-shadow: inset 0 1px 0 rgba(255,255,255,.06), 0 0 8px rgba(197,160,89,.1), 0 0 40px rgba(0,0,0,.8);
  transform: translateY(16px) scale(.98);
  transition: transform .35s var(--ease-out);
  border-radius: 2px;
  max-height: 80vh; overflow-y: auto;
}
.modal-overlay.open .modal-box { transform: translateY(0) scale(1); }
.modal-box .m-title {
  font-family: var(--font-en); font-size: 14px; letter-spacing: 0.25em;
  color: var(--gold); text-transform: uppercase; margin-bottom: 6px;
}
.modal-box .m-name {
  font-size: 22px; letter-spacing: 0.1em; margin-bottom: 18px;
  text-indent: 0.1em;
}
.modal-box .m-section {
  margin-bottom: 14px;
}
.modal-box .m-section:last-child { margin-bottom: 0; }
.modal-box .m-label {
  font-family: var(--font-sans); font-size: 0.55rem; color: var(--gold);
  letter-spacing: 0.2em; text-transform: uppercase; margin-bottom: 4px;
  opacity: 0.7;
}
.modal-box .m-text {
  font-size: 0.92rem; color: var(--sub); line-height: 2;
  letter-spacing: 0.03em;
}
.modal-box .m-text em {
  color: var(--gold-dim); font-style: normal; margin: 0 2px;
}
.modal-close {
  position: absolute; top: 12px; right: 16px;
  background: none; border: none; color: var(--sub); font-size: 20px;
  cursor: pointer; padding: 6px; line-height: 1;
  transition: color .2s var(--ease-std), transform .2s var(--ease-std);
}
.modal-close:hover { color: var(--gold); transform: rotate(90deg); }
.modal-close:active { transform: scale(.9); }
.modal-close:focus-visible { outline: 2px solid var(--gold); outline-offset: 2px; }

/* 翻页提示 */
.page-hint {
  position: absolute; bottom: 30px; left: 50%;
  transform: translateX(-50%);
  font-size: 10px; letter-spacing: 0.4em; color: var(--sub);
  opacity: .25; z-index: 3; pointer-events: none;
  transition: opacity .3s;
  white-space: nowrap;
}
.page:hover .page-hint { opacity: .5; }

/* 左侧返回提示 */
.back-hint {
  position: absolute; left: 30px; top: 50%;
  transform: translateY(-50%);
  writing-mode: vertical-rl;
  font-size: 10px; letter-spacing: 0.4em; color: var(--sub);
  opacity: .2; z-index: 3; pointer-events: none;
  transition: opacity .3s;
}
.page:hover .back-hint { opacity: .45; }

/* ========== 第三部分 ========== */
.board-grid {
  display: grid; grid-template-columns: 1fr; gap: 16px;
}
.board-item {
  display: flex; align-items: center; justify-content: space-between;
  padding: 22px 24px;
  background: rgba(255,255,255,.015);
  border: 1px solid rgba(255,255,255,.06);
  border-left: 2px solid var(--gold);
  text-decoration: none; color: var(--text);
  transition: transform .3s var(--ease-out), border-color .3s var(--ease-std), background .3s var(--ease-std), box-shadow .3s var(--ease-std);
}
.board-item:hover {
  transform: translateY(-3px);
  border-color: var(--gold-dim);
  border-left-color: var(--gold);
  background: var(--gold-glow);
  box-shadow: 0 0 8px rgba(197,160,89,0.06), 0 0 34px rgba(197,160,89,0.04);
}
.board-item:active { transform: scale(.98); }
.board-item:focus-visible { outline: 2px solid var(--gold); outline-offset: 2px; }
.board-item .b-left { display: flex; align-items: center; gap: 16px; }
.board-item .b-icon {
  font-size: 1.3rem; color: var(--gold); width: 28px; text-align: center;
  line-height: 1;
}
.board-item .b-label { font-size: 1rem; letter-spacing: 0.1em; }
.board-item .b-en {
  font-family: var(--font-sans); font-size: 0.5rem; color: var(--sub);
  letter-spacing: 0.18em; text-transform: uppercase; display: block; margin-top: 3px;
}
.board-item .b-arrow {
  color: var(--gold-dim); font-size: 1.1rem;
  transition: transform .3s var(--ease-std), color .3s var(--ease-std);
}
.board-item:hover .b-arrow { transform: translateX(4px); color: var(--gold); }

/* ========== Chapter V：留言 ========== */
#page5 .inner { max-width: 600px; }
.chat-box {
  background: rgba(255,255,255,.028);
  border: 1px solid rgba(255,255,255,.06);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  box-shadow: inset 0 1px 0 rgba(255,255,255,.05), 0 0 40px rgba(0,0,0,.5);
  padding: 0;
  position: relative;
  overflow: hidden;
}
.chat-box::before {
  content: ""; position: absolute; top: 0; left: 0; right: 0; height: 1px;
  background: linear-gradient(90deg, transparent, var(--gold-dim) 30%, var(--gold-dim) 70%, transparent);
}
.chat-messages {
  padding: 28px 22px 16px;
  max-height: 44vh; overflow-y: auto;
  display: flex; flex-direction: column; gap: 18px;
  scrollbar-width: thin; scrollbar-color: var(--gold-dim) transparent;
}
.chat-messages::-webkit-scrollbar { width: 3px; }
.chat-messages::-webkit-scrollbar-thumb { background: var(--gold-dim); border-radius: 2px; }

.chat-msg {
  display: flex; gap: 10px; align-items: flex-end;
  animation: msgIn .45s var(--ease-out) both;
}
@keyframes msgIn {
  from { opacity: 0; transform: translateY(10px); }
  to { opacity: 1; transform: translateY(0); }
}
.chat-msg.left { align-self: flex-start; flex-direction: row; }
.chat-msg.right { align-self: flex-end; flex-direction: row-reverse; }

.chat-msg > div:last-child {
  min-width: 0;
  flex: 0 1 auto;
  display: flex;
  flex-direction: column;
}

.chat-avatar {
  width: 30px; height: 30px; border-radius: 50%;
  display: flex; align-items: center; justify-content: center;
  font-size: 0.7rem; font-family: var(--font-en); letter-spacing: 0;
  flex-shrink: 0;
  border: 1px solid var(--gold-dim);
  background: rgba(197,160,89,.08);
  color: var(--gold);
}
.chat-msg.right .chat-avatar {
  border-color: rgba(160,165,181,.3);
  background: rgba(160,165,181,.06);
  color: var(--sub);
}
.chat-bubble {
  display: block;
  max-width: 100%;
  padding: 12px 16px;
  font-size: 0.88rem; line-height: 1.85;
  letter-spacing: 0.02em;
  position: relative;
  border-radius: 2px;
  word-break: break-word;
  white-space: normal;
  width: fit-content;
}
.chat-msg.left .chat-bubble {
  background: rgba(197,160,89,.06);
  border: 1px solid rgba(197,160,89,.18);
  color: var(--text);
  border-bottom-left-radius: 0;
}
.chat-msg.right .chat-bubble {
  background: rgba(255,255,255,.03);
  border: 1px solid rgba(255,255,255,.06);
  color: var(--sub);
  border-bottom-right-radius: 0;
  margin-left: auto;
}
.chat-time {
  font-size: 0.55rem; color: var(--sub); opacity: 0.4;
  margin-top: 6px; letter-spacing: 0.1em;
}
.chat-msg.right .chat-time { text-align: right; }

.chat-input-area {
  display: flex; align-items: center; gap: 10px;
  padding: 16px 22px 20px;
  border-top: 1px solid rgba(255,255,255,.06);
}
.chat-input {
  flex: 1;
  background: rgba(0,0,0,.4);
  border: 1px solid rgba(255,255,255,.08);
  color: var(--text);
  padding: 12px 16px;
  font-family: var(--font-cn);
  font-size: 0.88rem;
  letter-spacing: 0.02em;
  outline: none;
  transition: border-color .3s var(--ease-std), box-shadow .3s var(--ease-std);
  border-radius: 1px;
  min-width: 0;
}
.chat-input::placeholder { color: var(--sub); opacity: 0.35; }
.chat-input:focus {
  border-color: var(--gold-dim);
  box-shadow: 0 0 0 1px rgba(197,160,89,.1);
}
.chat-send {
  background: rgba(197,160,89,.1);
  border: 1px solid var(--gold-dim);
  color: var(--gold);
  padding: 12px 20px;
  font-family: var(--font-sans);
  font-size: 0.7rem; letter-spacing: 0.15em;
  cursor: pointer;
  transition: background .3s var(--ease-std), border-color .3s var(--ease-std), transform .15s var(--ease-std), box-shadow .3s var(--ease-std);
  border-radius: 1px;
  white-space: nowrap;
}
.chat-send:hover {
  background: rgba(197,160,89,.18);
  border-color: var(--gold);
  box-shadow: 0 0 8px rgba(197,160,89,.1), 0 0 20px rgba(197,160,89,.05);
}
.chat-send:active { transform: scale(.95); }
.chat-send:focus-visible { outline: 2px solid var(--gold); outline-offset: 2px; }

/* ========== 音效开关 ========== */
#btn {
  position: fixed; top: 20px; right: 20px; z-index: 9999;
  width: 44px; height: 44px; border-radius: 50%;
  border: 1px solid var(--gold-dim);
  background: rgba(0,0,0,0.6); color: var(--sub);
  font-size: 18px; cursor: pointer;
  transition: color .3s var(--ease-std), border-color .3s var(--ease-std), box-shadow .3s var(--ease-std), background .3s var(--ease-std);
  backdrop-filter: blur(4px); -webkit-backdrop-filter: blur(4px);
  display: flex; align-items: center; justify-content: center;
}
#btn:hover { border-color: var(--gold); color: var(--gold); }
#btn:active { transform: scale(.92); }
#btn:focus-visible { outline: 2px solid var(--gold); outline-offset: 2px; }
#btn.on {
  color: var(--gold); border-color: var(--gold);
  box-shadow: 0 0 8px rgba(197,160,89,.3), 0 0 34px rgba(197,160,89,.12);
  background: var(--gold-glow);
}
#sound-label {
  position: fixed; top: 70px; right: 20px; z-index: 9998;
  font-size: 9px; letter-spacing: 0.2em; color: var(--sub);
  opacity: 0; transition: opacity .3s; pointer-events: none;
}
#btn.on ~ #sound-label { opacity: .5; }

/* 翻页导航点 */
.page-dots {
  position: fixed; right: 24px; top: 50%;
  transform: translateY(-50%);
  z-index: 100;
  display: flex; flex-direction: column; gap: 14px;
}
.dot {
  width: 6px; height: 6px; border-radius: 50%;
  border: 1px solid var(--gold-dim);
  background: transparent;
  cursor: pointer;
  transition: background .3s var(--ease-std), border-color .3s var(--ease-std), box-shadow .3s var(--ease-std);
  padding: 0;
}
.dot:hover { border-color: var(--gold); background: rgba(197,160,89,.3); }
.dot.active {
  background: var(--gold);
  border-color: var(--gold);
  box-shadow: 0 0 8px rgba(197,160,89,.5);
}
.dot:focus-visible { outline: 2px solid var(--gold); outline-offset: 3px; }

/* ========== 响应式 ========== */
@media (max-width: 520px) {
  .page { padding: 40px 16px; }
  .style-grid { grid-template-columns: 1fr 1fr; gap: 10px; }
  .style-item { padding: 20px 10px; }
  .style-item .s-name { font-size: 0.95rem; }
  .cn-title { font-size: 21px; letter-spacing: 0.1em; text-indent: 0.1em; }
  #page0 h1 { font-size: clamp(1.8rem, 11vw, 3rem); letter-spacing: 0.12em; text-indent: 0.12em; }
  .card { padding: 22px 18px; }
  .board-item { padding: 18px 18px; }
  .board-item .b-label { font-size: 0.92rem; }
  .modal-box { padding: 30px 20px 24px; }
  .chat-messages { max-height: 38vh; padding: 22px 16px 12px; }
  .chat-input-area { padding: 12px 16px 16px; }
  .chat-send { padding: 12px 14px; font-size: 0.65rem; }
  .page-dots { right: 12px; gap: 10px; }
  .dot { width: 5px; height: 5px; }
  .back-hint { display: none; }
  .notice-content { padding: 22px 18px; font-size: 0.88rem; }
}

@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
  .reveal { opacity: 1; transform: none; }
  .bg-img::after { animation: none; }
  .tap-hint { animation: none; opacity: 0.6; }
  .chat-msg { animation: none; }
}
</style>
</head>
<body>

<button id="btn" aria-label="切换音效" title="点击开启音效">♪</button>
<span id="sound-label">SOUND OFF</span>

<!-- 翻页导航点（6 个点，对应 6 页） -->
<div class="page-dots" role="tablist" aria-label="页面导航">
  <button class="dot active" data-page="0" role="tab" aria-label="封面" aria-selected="true"></button>
  <button class="dot" data-page="1" role="tab" aria-label="档案" aria-selected="false"></button>
  <button class="dot" data-page="2" role="tab" aria-label="风格" aria-selected="false"></button>
  <button class="dot" data-page="3" role="tab" aria-label="须知" aria-selected="false"></button>
  <button class="dot" data-page="4" role="tab" aria-label="密约" aria-selected="false"></button>
  <button class="dot" data-page="5" role="tab" aria-label="留言" aria-selected="false"></button>
</div>

<!-- ============ 封面 ============ -->
<div class="page active" id="page0" role="button" tabindex="0" aria-label="点击进入">
  <div class="bg-img"></div>
  <h1 id="cover-title" aria-label="PSEROS"></h1>
  <p>无声沉沦</p>
  <div class="cover-sub">你如此咬文嚼字，<br>是为了找寻我的破绽吗。</div>
  <div class="tap-hint">点击封面 · 步入古堡</div>
</div>

<!-- ============ 个人档案 ============ -->
<div class="page" id="page1">
  <div class="inner">
    <div class="en reveal">Chapter I · 档案</div>
    <div class="cn-title reveal">旅者档案</div>
    <div class="card reveal">
      <div class="row"><span class="k">代号 / Code</span><span class="v">PSEROS</span></div>
      <div class="row"><span class="k">性别 / Gender</span><span class="v">女</span></div>
      <div class="row"><span class="k">十六型 / MBTI</span><span class="v">INFP</span></div>
      <div class="row"><span class="k">技能 / Skills</span><span class="v">虚恋 · 病恋 · 虐恋 · 树洞</span></div>
    </div>
    <div class="divider reveal"></div>
  </div>
  <div class="back-hint">返回</div>
  <div class="page-hint">点击右侧 · 继续</div>
</div>

<!-- ============ 风格 ============ -->
<div class="page" id="page2">
  <div class="inner">
    <div class="en reveal">Chapter II · 风格</div>
    <div class="cn-title reveal">风格</div>
    <div class="style-grid reveal" id="style-grid">
      <div class="style-item" data-style="虚恋" tabindex="0" role="button" aria-label="虚恋">
        <span class="s-icon">✧</span>
        <span class="s-name">虚恋</span>
        <span class="s-en">Ethereal</span>
      </div>
      <div class="style-item" data-style="病恋" tabindex="0" role="button" aria-label="病恋">
        <span class="s-icon">❀</span>
        <span class="s-name">病恋</span>
        <span class="s-en">Morbid</span>
      </div>
      <div class="style-item" data-style="虐恋" tabindex="0" role="button" aria-label="虐恋">
        <span class="s-icon">⚔</span>
        <span class="s-name">虐恋</span>
        <span class="s-en">Tragic</span>
      </div>
      <div class="style-item" data-style="树洞" tabindex="0" role="button" aria-label="树洞">
        <span class="s-icon">◈</span>
        <span class="s-name">树洞</span>
        <span class="s-en">Hollow</span>
      </div>
    </div>
    <div class="divider reveal"></div>
  </div>
  <div class="back-hint">返回</div>
  <div class="page-hint">点击右侧 · 继续</div>
</div>

<!-- ============ 须知（独立页面，位于风格之后） ============ -->
<div class="page" id="page3">
  <div class="inner">
    <div class="en reveal">Chapter III · 须知</div>
    <div class="cn-title reveal">须知</div>
    <div class="card reveal notice-content">
      <p class="notice-first">下单默认已读须知</p>
      <p>开始时单内虚病默认恋人关系，虐树洞默认非恋人关系，如有特殊需求请告诉我</p>
      <p>请在开始前告诉我您的喜雷，如单内触到隐雷，概不负责</p>
      <p>能力有限，不保证所有人都喜欢我的风格，都能有很好的体验</p>
      <p>单内如有不适，请及时打断暂停，并告诉我，我会进行安抚</p>
      <p>默认回合制问答，如有抢答导致的意思理解不正确，概不负责</p>
      <p>婉拒故意刁难，敷衍，反驳型人格，带有审视目的（审核除外）</p>
      <p>如果故意玩抽象，或者故意隐瞒，伪装，体验感不佳，概不负责</p>
      <p>如在单内有辱骂贬低我皮下，非恋人情况下开h，默认送单并永拒</p>
      <p>为保证不耽误彼此时间，请提前约好，临时有事提前告知。</p>
      <p>开始后十分钟内未到场，默认存单。</p>
      <p>请勿在未允许的情况下截图录屏外传</p>
      <p>十分钟内不满意可随时换人</p>
    </div>
    <div class="divider reveal"></div>
  </div>
  <div class="back-hint">返回</div>
  <div class="page-hint">点击右侧 · 继续</div>
</div>

<!-- ============ 密约（已移除须知，仅保留话术与板评） ============ -->
<div class="page" id="page4">
  <div class="inner">
    <div class="en reveal">Chapter IV · 密约</div>
    <div class="cn-title reveal">隐秘契约</div>
    <div class="board-grid reveal">
      <a href="https://www.kdocs.cn/l/cvwzjx6si9UH" target="_blank" rel="noopener" class="board-item">
        <div class="b-left">
          <span class="b-icon">✦</span>
          <div>
            <span class="b-label">密语 / 话术</span>
            <span class="b-en">Scripts · Lines</span>
          </div>
        </div>
        <span class="b-arrow">→</span>
      </a>
      <a href="https://www.kdocs.cn/l/chQuAvdBNID5" target="_blank" rel="noopener" class="board-item">
        <div class="b-left">
          <span class="b-icon">🕯</span>
          <div>
            <span class="b-label">颂词 / 板评</span>
            <span class="b-en">Reviews · Board</span>
          </div>
        </div>
        <span class="b-arrow">→</span>
      </a>
    </div>
    <div class="divider reveal"></div>
  </div>
  <div class="back-hint">返回</div>
  <div class="page-hint">点击右侧 · 留言</div>
</div>

<!-- ============ Chapter V：留言 ============ -->
<div class="page" id="page5">
  <div class="inner">
    <div class="en reveal">Chapter V · 留言</div>
    <div class="cn-title reveal">低语</div>
    <div class="chat-box reveal">
      <div class="chat-messages" id="chat-messages">
        <div class="chat-msg left">
          <div class="chat-avatar">P</div>
          <div>
            <div class="chat-bubble">你好，我是 PSEROS。<br>我们什么时候才能再见呢？</div>
            <div class="chat-time">PSEROS · 刚刚</div>
          </div>
        </div>
      </div>
      <div class="chat-input-area">
        <input type="text" class="chat-input" id="chat-input" placeholder="写下你想说的话……" maxlength="200" aria-label="输入留言">
        <button class="chat-send" id="chat-send" aria-label="发送">发送</button>
      </div>
    </div>
    <div class="divider reveal"></div>
  </div>
  <div class="back-hint">返回</div>
</div>

<!-- ============ 风格弹窗 ============ -->
<div class="modal-overlay" id="modal" role="dialog" aria-modal="true" aria-label="风格详情">
  <div class="modal-box">
    <button class="modal-close" id="modal-close" aria-label="关闭">×</button>
    <div class="m-title" id="modal-en">Ethereal</div>
    <div class="m-name" id="modal-name">虚恋</div>
    <div id="modal-body"></div>
  </div>
</div>

<script>
/* =============================================
   0. 封面字母动效
   ============================================= */
(function() {
  var title = document.getElementById('cover-title');
  var text = 'PSEROS';
  title.innerHTML = '';
  text.split('').forEach(function(ch) {
    var span = document.createElement('span');
    span.className = 'letter';
    span.textContent = ch;
    title.appendChild(span);
  });
  var letters = title.querySelectorAll('.letter');
  letters.forEach(function(letter, i) {
    var delay = Math.random() * 2;
    var dur = 3 + Math.random() * 2;
    letter.style.animation = 'letterFloat ' + dur + 's ease-in-out ' + delay + 's infinite alternate';
  });
  var style = document.createElement('style');
  style.textContent = '@keyframes letterFloat { 0% { transform: translateY(0); } 100% { transform: translateY(-5px); } }';
  document.head.appendChild(style);
})();

/* =============================================
   1. 翻页系统（6 页）
   ============================================= */
var currentPage = 0;
var pages = document.querySelectorAll('.page');
var dots = document.querySelectorAll('.dot');
var totalPages = pages.length;

function goToPage(index) {
  if (index < 0 || index >= totalPages) return;
  pages[currentPage].classList.remove('active');
  dots[currentPage].classList.remove('active');
  dots[currentPage].setAttribute('aria-selected', 'false');
  currentPage = index;
  pages[currentPage].classList.add('active');
  dots[currentPage].classList.add('active');
  dots[currentPage].setAttribute('aria-selected', 'true');
  playSound('page');
}

pages.forEach(function(page, i) {
  page.addEventListener('click', function(e) {
    if (modal.classList.contains('open')) return;
    if (e.target.closest('.style-item')) return;
    if (e.target.closest('.chat-input-area')) return;
    if (e.target.closest('.board-item')) return;
    if (e.target.closest('.modal-box')) return;
    if (e.target.closest('button')) return;

    var rect = page.getBoundingClientRect();
    var clickX = e.clientX - rect.left;

    if (i === 0) {
      goToPage(1);
      return;
    }

    if (clickX > rect.width * 0.7 && i < totalPages - 1) {
      goToPage(i + 1);
    } else if (clickX < rect.width * 0.3 && i > 0) {
      goToPage(i - 1);
    }
  });
});

document.addEventListener('keydown', function(e) {
  if (modal.classList.contains('open')) return;
  if (e.key === 'ArrowRight' || e.key === 'ArrowDown') {
    e.preventDefault();
    goToPage(currentPage + 1);
  } else if (e.key === 'ArrowLeft' || e.key === 'ArrowUp') {
    e.preventDefault();
    goToPage(currentPage - 1);
  }
});

dots.forEach(function(dot) {
  dot.addEventListener('click', function(e) {
    e.stopPropagation();
    goToPage(parseInt(this.dataset.page));
  });
});

document.getElementById('page0').addEventListener('keydown', function(e) {
  if (e.key === 'Enter' || e.key === ' ') {
    e.preventDefault();
    goToPage(1);
  }
});

/* =============================================
   2. 风格弹窗数据
   ============================================= */
var styleData = {
  '虚恋': {
    en: 'Ethereal',
    sections: [
      { label: '主风格', text: '高恋 · 微文 · 引导' },
      { label: '副风格', text: '下位 · 动描 · 微擦' }
    ]
  },
  '病恋': {
    en: 'Morbid',
    sections: [
      { label: '主风格', text: '高恋 · 温病 · 微文 · 剖析' },
      { label: '副风格', text: '低无 · 白话 · 动描' },
      { label: '附加', text: '汹涌 / 窥伺 / 爱而不得强制' }
    ]
  },
  '虐恋': {
    en: 'Tragic',
    sections: [
      { label: '主风格', text: '低无 · 白话 · 救赎' },
      { label: '副风格', text: '剖析 · 微涉三' }
    ]
  },
  '树洞': {
    en: 'Hollow',
    sections: [
      { label: '主风格', text: '安抚 · 共情' },
      { label: '副风格', text: '分析 · 解决' }
    ]
  }
};

var modal = document.getElementById('modal');
var modalEn = document.getElementById('modal-en');
var modalName = document.getElementById('modal-name');
var modalBody = document.getElementById('modal-body');
var modalClose = document.getElementById('modal-close');

function openModal(styleName) {
  var data = styleData[styleName];
  if (!data) return;
  modalEn.textContent = data.en;
  modalName.textContent = styleName;
  var html = '';
  data.sections.forEach(function(sec) {
    html += '<div class="m-section">';
    html += '<div class="m-label">' + sec.label + '</div>';
    html += '<div class="m-text">' + sec.text.replace(/\n/g, '<br>') + '</div>';
    html += '</div>';
  });
  modalBody.innerHTML = html;
  modal.classList.add('open');
  playSound('open');
}

function closeModal() {
  modal.classList.remove('open');
  playSound('close');
}

document.querySelectorAll('.style-item').forEach(function(item) {
  item.addEventListener('click', function(e) {
    e.stopPropagation();
    openModal(this.dataset.style);
  });
  item.addEventListener('keydown', function(e) {
    if (e.key === 'Enter' || e.key === ' ') {
      e.preventDefault();
      openModal(this.dataset.style);
    }
  });
});

modalClose.addEventListener('click', closeModal);
modal.addEventListener('click', function(e) {
  if (e.target === modal) closeModal();
});
document.addEventListener('keydown', function(e) {
  if (e.key === 'Escape' && modal.classList.contains('open')) closeModal();
});

/* =============================================
   3. 留言交互（无自动回复）
   ============================================= */
var chatMessages = document.getElementById('chat-messages');
var chatInput = document.getElementById('chat-input');
var chatSend = document.getElementById('chat-send');

function addUserMessage(text) {
  if (!text.trim()) return;
  var msg = document.createElement('div');
  msg.className = 'chat-msg right';
  msg.innerHTML =
    '<div class="chat-avatar">U</div>' +
    '<div>' +
      '<div class="chat-bubble">' + escapeHTML(text.trim()) + '</div>' +
      '<div class="chat-time">你 · 刚刚</div>' +
    '</div>';
  chatMessages.appendChild(msg);
  chatMessages.scrollTop = chatMessages.scrollHeight;
  chatInput.value = '';
  playSound('send');
}

function escapeHTML(str) {
  return str.replace(/&/g, '&amp;').replace(/</g, '&lt;').replace(/>/g, '&gt;').replace(/"/g, '&quot;');
}

chatSend.addEventListener('click', function(e) {
  e.stopPropagation();
  addUserMessage(chatInput.value);
});

chatInput.addEventListener('keydown', function(e) {
  e.stopPropagation();
  if (e.key === 'Enter') {
    e.preventDefault();
    addUserMessage(chatInput.value);
  }
});

/* =============================================
   4. Web Audio 音效引擎
   ============================================= */
var actx = null;
var masterGain = null;
var soundEnabled = false;
var btn = document.getElementById('btn');
var soundLabel = document.getElementById('sound-label');
var lastHoverTime = 0;

function initAudio() {
  if (actx) return;
  var AC = window.AudioContext || window.webkitAudioContext;
  if (!AC) return;
  actx = new AC();
  masterGain = actx.createGain();
  masterGain.gain.value = 0.5;
  masterGain.connect(actx.destination);
}

function playSound(type) {
  if (!soundEnabled || !actx) return;
  if (actx.state === 'suspended') actx.resume();

  var t = actx.currentTime;
  var osc, gain, filter, osc2, gain2;

  switch (type) {
    case 'hover':
      if (t - lastHoverTime < 0.12) return;
      lastHoverTime = t;
      osc = actx.createOscillator();
      gain = actx.createGain();
      filter = actx.createBiquadFilter();
      osc.type = 'sine';
      osc.frequency.setValueAtTime(620, t);
      filter.type = 'lowpass';
      filter.frequency.setValueAtTime(1200, t);
      gain.gain.setValueAtTime(0, t);
      gain.gain.linearRampToValueAtTime(0.04, t + 0.005);
      gain.gain.linearRampToValueAtTime(0, t + 0.06);
      osc.connect(filter); filter.connect(gain); gain.connect(masterGain);
      osc.start(t); osc.stop(t + 0.07);
      break;

    case 'page':
      osc = actx.createOscillator();
      gain = actx.createGain();
      filter = actx.createBiquadFilter();
      osc.type = 'square';
      osc.frequency.setValueAtTime(600, t);
      osc.frequency.exponentialRampToValueAtTime(1500, t + 0.12);
      filter.type = 'lowpass';
      filter.frequency.setValueAtTime(1500, t);
      gain.gain.setValueAtTime(0, t);
      gain.gain.linearRampToValueAtTime(0.06, t + 0.02);
      gain.gain.linearRampToValueAtTime(0, t + 0.12);
      osc.connect(filter); filter.connect(gain); gain.connect(masterGain);
      osc.start(t); osc.stop(t + 0.13);
      break;

    case 'open':
      osc = actx.createOscillator();
      gain = actx.createGain();
      filter = actx.createBiquadFilter();
      osc.type = 'square';
      osc.frequency.setValueAtTime(600, t);
      osc.frequency.exponentialRampToValueAtTime(1500, t + 0.12);
      filter.type = 'lowpass';
      filter.frequency.setValueAtTime(1500, t);
      gain.gain.setValueAtTime(0, t);
      gain.gain.linearRampToValueAtTime(0.08, t + 0.02);
      gain.gain.linearRampToValueAtTime(0, t + 0.12);
      osc.connect(filter); filter.connect(gain); gain.connect(masterGain);
      osc.start(t); osc.stop(t + 0.13);
      break;

    case 'close':
      osc = actx.createOscillator();
      gain = actx.createGain();
      osc.type = 'triangle';
      osc.frequency.setValueAtTime(560, t);
      osc.frequency.exponentialRampToValueAtTime(380, t + 0.11);
      gain.gain.setValueAtTime(0, t);
      gain.gain.linearRampToValueAtTime(0.08, t + 0.01);
      gain.gain.linearRampToValueAtTime(0, t + 0.11);
      osc.connect(gain); gain.connect(masterGain);
      osc.start(t); osc.stop(t + 0.12);
      break;

    case 'send':
      osc = actx.createOscillator();
      gain = actx.createGain();
      osc.type = 'triangle';
      osc.frequency.setValueAtTime(480, t);
      gain.gain.setValueAtTime(0, t);
      gain.gain.linearRampToValueAtTime(0.08, t + 0.01);
      gain.gain.linearRampToValueAtTime(0, t + 0.15);
      osc.connect(gain); gain.connect(masterGain);
      osc.start(t); osc.stop(t + 0.16);

      osc2 = actx.createOscillator();
      gain2 = actx.createGain();
      osc2.type = 'triangle';
      osc2.frequency.setValueAtTime(700, t + 0.09);
      gain2.gain.setValueAtTime(0, t + 0.09);
      gain2.gain.linearRampToValueAtTime(0.08, t + 0.10);
      gain2.gain.linearRampToValueAtTime(0, t + 0.24);
      osc2.connect(gain2); gain2.connect(masterGain);
      osc2.start(t + 0.09); osc2.stop(t + 0.25);
      break;

    case 'toggle':
      osc = actx.createOscillator();
      gain = actx.createGain();
      osc.type = 'triangle';
      osc.frequency.setValueAtTime(480, t);
      gain.gain.setValueAtTime(0, t);
      gain.gain.linearRampToValueAtTime(0.10, t + 0.01);
      gain.gain.linearRampToValueAtTime(0, t + 0.15);
      osc.connect(gain); gain.connect(masterGain);
      osc.start(t); osc.stop(t + 0.16);

      osc2 = actx.createOscillator();
      gain2 = actx.createGain();
      osc2.type = 'triangle';
      osc2.frequency.setValueAtTime(700, t + 0.09);
      gain2.gain.setValueAtTime(0, t + 0.09);
      gain2.gain.linearRampToValueAtTime(0.10, t + 0.10);
      gain2.gain.linearRampToValueAtTime(0, t + 0.24);
      osc2.connect(gain2); gain2.connect(masterGain);
      osc2.start(t + 0.09); osc2.stop(t + 0.25);
      break;
  }
}

btn.addEventListener('click', function(e) {
  e.stopPropagation();
  initAudio();
  if (actx && actx.state === 'suspended') actx.resume();

  soundEnabled = !soundEnabled;
  btn.className = soundEnabled ? 'on' : '';
  soundLabel.textContent = soundEnabled ? 'SOUND ON' : 'SOUND OFF';
  localStorage.setItem('pseros_sound', soundEnabled ? '1' : '0');

  if (soundEnabled) {
    playSound('toggle');
  }
});

(function() {
  if (localStorage.getItem('pseros_sound') === '1') {
    soundEnabled = true;
    btn.className = 'on';
    soundLabel.textContent = 'SOUND ON';
  }
})();

document.querySelectorAll('.style-item, .board-item, .row').forEach(function(el) {
  el.addEventListener('mouseenter', function() {
    playSound('hover');
  });
});

document.addEventListener('visibilitychange', function() {
  if (document.hidden) {
    if (actx && actx.state === 'running') actx.suspend();
  } else {
    if (actx && soundEnabled && actx.state === 'suspended') actx.resume();
  }
});

document.addEventListener('click', function() {
  if (actx && actx.state === 'suspended') actx.resume();
}, { once: true });
</script>
</body>
</html>
