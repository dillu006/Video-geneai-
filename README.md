<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>BharatAI</title>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700;800&display=swap" rel="stylesheet"/>
<style>
* { box-sizing: border-box; margin: 0; padding: 0; }

body {
  font-family: 'Poppins', sans-serif;
  background: #0a0a14;
  color: #fff;
  min-height: 100vh;
}

body::before {
  content: '';
  position: fixed; inset: 0; z-index: 0; pointer-events: none;
  background:
    radial-gradient(ellipse 70% 50% at 10% 0%, rgba(255,100,0,0.12) 0%, transparent 60%),
    radial-gradient(ellipse 60% 40% at 90% 100%, rgba(0,150,120,0.1) 0%, transparent 60%);
}

.page { position: relative; z-index: 1; max-width: 900px; margin: 0 auto; padding: 20px 16px 80px; }

/* HEADER */
.header { text-align: center; padding: 32px 0 20px; }
.flag-badge {
  display: inline-flex; align-items: center; gap: 8px;
  background: rgba(255,100,0,0.12); border: 1px solid rgba(255,150,0,0.3);
  border-radius: 40px; padding: 5px 16px; margin-bottom: 12px;
  font-size: 12px; font-weight: 700; letter-spacing: 0.1em; color: #FFB300;
  text-transform: uppercase;
}
.title {
  font-size: clamp(1.9rem, 5vw, 3rem); font-weight: 800;
  background: linear-gradient(135deg, #FF6600, #FFB300);
  -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
  margin-bottom: 6px;
}
.sub { font-size: 0.88rem; color: rgba(255,255,255,0.4); font-weight: 300; }
.strip { display: flex; height: 3px; border-radius: 2px; margin: 18px 0; overflow: hidden; }
.strip span:nth-child(1) { flex:1; background:#FF9933; }
.strip span:nth-child(2) { flex:1; background:#ffffff; }
.strip span:nth-child(3) { flex:1; background:#138808; }

/* CARD */
.card {
  background: rgba(255,255,255,0.04);
  border: 1px solid rgba(255,150,0,0.2);
  border-radius: 16px; padding: 20px; margin-bottom: 14px;
}
.card-label {
  font-size: 11px; font-weight: 700; letter-spacing: 0.12em;
  text-transform: uppercase; color: #FFB300; margin-bottom: 12px;
}

/* API KEY */
.api-wrap { display: flex; gap: 10px; flex-wrap: wrap; }
.api-wrap input {
  flex: 1; min-width: 220px;
  background: rgba(0,0,0,0.4); border: 1px solid rgba(255,100,0,0.3);
  border-radius: 10px; padding: 10px 14px; color: #fff;
  font-family: 'Poppins', sans-serif; font-size: 0.85rem; outline: none;
}
.api-wrap input:focus { border-color: #FF6600; }
.api-save {
  padding: 10px 20px; border-radius: 10px; border: none;
  background: rgba(255,100,0,0.2); color: #FF6600;
  font-family: 'Poppins', sans-serif; font-size: 0.83rem; font-weight: 700;
  cursor: pointer; transition: background 0.2s; white-space: nowrap;
}
.api-save:hover { background: rgba(255,100,0,0.35); }
.api-hint { font-size: 11px; color: rgba(255,255,255,0.3); margin-top: 6px; }
.api-hint a { color: rgba(255,179,0,0.5); }

/* TEXTAREA */
textarea {
  width: 100%; min-height: 100px;
  background: rgba(0,0,0,0.35); border: 1px solid rgba(255,150,0,0.2);
  border-radius: 10px; color: #fff;
  font-family: 'Poppins', sans-serif; font-size: 0.88rem;
  padding: 12px; resize: vertical; outline: none;
}
textarea:focus { border-color: #FF6600; }
textarea::placeholder { color: rgba(255,255,255,0.25); }

/* GENDER */
.gender-row { display: flex; gap: 12px; }
.g-btn {
  flex: 1; padding: 14px 10px; border-radius: 12px;
  border: 2px solid rgba(255,150,0,0.2);
  background: rgba(0,0,0,0.2); cursor: pointer;
  font-family: 'Poppins', sans-serif; font-size: 0.85rem; font-weight: 600;
  color: rgba(255,255,255,0.55); text-align: center; transition: all 0.22s;
}
.g-btn .big { font-size: 1.8rem; display: block; margin-bottom: 4px; }
.g-btn:hover { border-color: #FFB300; color: #fff; }
.g-btn.sel-girl { border-color: #E91E63; background: rgba(233,30,99,0.12); color: #E91E63; }
.g-btn.sel-boy  { border-color: #42A5F5; background: rgba(66,165,245,0.12); color: #42A5F5; }

/* STATES */
.state-grid {
  display: grid; grid-template-columns: repeat(auto-fill, minmax(110px, 1fr));
  gap: 8px; max-height: 260px; overflow-y: auto; padding-right: 2px;
}
.state-grid::-webkit-scrollbar { width: 3px; }
.state-grid::-webkit-scrollbar-thumb { background: #FF6600; border-radius: 2px; }
.s-btn {
  padding: 9px 6px; border-radius: 9px;
  border: 1px solid rgba(255,150,0,0.2);
  background: rgba(0,0,0,0.2); cursor: pointer;
  font-family: 'Poppins', sans-serif; font-size: 11px; font-weight: 600;
  color: rgba(255,255,255,0.55); text-align: center; transition: all 0.18s;
}
.s-btn .ico { display: block; font-size: 1.3rem; margin-bottom: 3px; }
.s-btn:hover { border-color: #FFB300; color: #fff; }
.s-btn.sel { border-color: #FF6600; background: rgba(255,100,0,0.15); color: #FF6600; }

/* LANG */
.lang-row { display: flex; flex-wrap: wrap; gap: 7px; }
.l-btn {
  padding: 6px 13px; border-radius: 40px;
  border: 1px solid rgba(255,150,0,0.2);
  background: rgba(0,0,0,0.2); cursor: pointer;
  font-family: 'Poppins', sans-serif; font-size: 12px; font-weight: 600;
  color: rgba(255,255,255,0.5); transition: all 0.18s;
}
.l-btn:hover { border-color: #00897B; color: #fff; }
.l-btn.sel { border-color: #00897B; background: rgba(0,137,123,0.15); color: #4DB6AC; }

/* MODE TABS */
.mode-row { display: flex; gap: 8px; flex-wrap: wrap; margin-bottom: 14px; }
.m-tab {
  padding: 8px 16px; border-radius: 40px;
  border: 1px solid rgba(255,150,0,0.2);
  background: rgba(0,0,0,0.2); cursor: pointer;
  font-family: 'Poppins', sans-serif; font-size: 12px; font-weight: 600;
  color: rgba(255,255,255,0.45); transition: all 0.18s;
}
.m-tab:hover { color: #fff; border-color: rgba(255,150,0,0.4); }
.m-tab.sel { background: rgba(255,100,0,0.18); border-color: #FF6600; color: #FFB300; }

/* GENERATE */
.gen-btn {
  width: 100%; padding: 16px; border-radius: 12px; border: none;
  background: linear-gradient(135deg, #FF6600, #FFB300);
  color: #fff; font-family: 'Poppins', sans-serif;
  font-size: 0.95rem; font-weight: 700; cursor: pointer;
  transition: all 0.25s; letter-spacing: 0.04em;
}
.gen-btn:hover { transform: translateY(-2px); box-shadow: 0 8px 24px rgba(255,102,0,0.35); }
.gen-btn:active { transform: translateY(0); }
.gen-btn:disabled { opacity: 0.5; cursor: not-allowed; transform: none; }

/* OUTPUT */
#output { display: none; }
#output.show { display: block; }

/* CHARACTER BOX */
.char-box {
  display: flex; align-items: center; gap: 14px;
  background: rgba(255,100,0,0.06); border: 1px solid rgba(255,150,0,0.2);
  border-radius: 13px; padding: 16px; margin-bottom: 12px;
}
.av-wrap {
  width: 60px; height: 60px; min-width: 60px;
  border-radius: 50%; background: rgba(255,100,0,0.1);
  border: 2px solid #FF6600; display: flex;
  align-items: center; justify-content: center; font-size: 2rem;
  animation: spin-border 4s linear infinite;
}
@keyframes spin-border {
  0%,100% { border-color: #FF6600; }
  50% { border-color: #FFB300; }
}
.char-info h3 { font-size: 1.05rem; font-weight: 700; margin-bottom: 3px; }
.char-info .meta { font-size: 11px; color: rgba(255,255,255,0.4); margin-bottom: 6px; }
.tags { display: flex; flex-wrap: wrap; gap: 5px; }
.tag {
  font-size: 10px; font-weight: 600; padding: 2px 9px;
  border-radius: 40px; background: rgba(255,179,0,0.1);
  border: 1px solid rgba(255,179,0,0.25); color: #FFB300;
}

/* RESPONSE */
.r-box {
  background: rgba(0,0,0,0.25); border: 1px solid rgba(255,150,0,0.2);
  border-radius: 12px; padding: 16px; margin-bottom: 12px;
  min-height: 70px; line-height: 1.75; font-size: 0.9rem;
  white-space: pre-wrap;
}
.r-box.loading::after {
  content: '\u258b'; color: #FF6600;
  animation: blink 1s step-end infinite;
}
@keyframes blink { 50% { opacity: 0; } }

/* ACTION BUTTONS */
.act-row { display: flex; gap: 9px; flex-wrap: wrap; }
.a-btn {
  padding: 8px 16px; border-radius: 40px;
  border: 1px solid rgba(0,150,120,0.3);
  background: rgba(0,137,123,0.1); color: #4DB6AC;
  font-family: 'Poppins', sans-serif; font-size: 12px; font-weight: 600;
  cursor: pointer; transition: all 0.18s;
}
.a-btn:hover { background: rgba(0,137,123,0.2); }
.a-btn.spk { background: rgba(233,30,99,0.12); border-color: rgba(233,30,99,0.4); color: #F48FB1; }

/* CHAT */
.chat-msgs {
  height: 260px; overflow-y: auto; padding: 12px;
  background: rgba(0,0,0,0.18); border: 1px solid rgba(255,150,0,0.2);
  border-radius: 12px; margin-bottom: 10px;
  display: flex; flex-direction: column; gap: 9px;
}
.chat-msgs::-webkit-scrollbar { width: 3px; }
.chat-msgs::-webkit-scrollbar-thumb { background: #FF6600; border-radius: 2px; }
.msg {
  max-width: 78%; padding: 9px 13px; border-radius: 12px;
  font-size: 0.87rem; line-height: 1.6;
}
.msg.user {
  align-self: flex-end;
