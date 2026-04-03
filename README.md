# study_worldheritage2
世界遺産検定2級学習管理アプリ
[sekaken2.html](https://github.com/user-attachments/files/26457855/sekaken2.html)
<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<title>世界遺産検定2級 学習管理</title>
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@400;500;700&display=swap" rel="stylesheet">
<style>
:root {
  --green:#1D9E75; --green-lt:#E1F5EE; --green-dk:#085041;
  --purple:#7F77DD; --purple-lt:#EEEDFE; --purple-dk:#3C3489;
  --amber:#BA7517; --amber-lt:#FAEEDA;
  --coral:#D85A30; --coral-lt:#FAECE7;
  --blue:#378ADD; --blue-lt:#E6F1FB;
  --red:#E24B4A; --red-lt:#FCEBEB;
  --bg:#f6f4ef; --card:#fff; --border:#e6e3db;
  --text:#1a1a1a; --t2:#555; --t3:#999;
  --r:12px; --rs:8px;
}
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
html,body{height:100%;font-family:'Noto Sans JP',-apple-system,sans-serif;background:var(--bg);color:var(--text);font-size:14px;line-height:1.6}
input,textarea,button,select{font-family:inherit;font-size:14px}

/* ── Layout ── */
.app{max-width:620px;margin:0 auto;padding-bottom:88px}

/* ── Header ── */
.hdr{background:var(--card);border-bottom:1px solid var(--border);padding:12px 16px 0;position:sticky;top:0;z-index:100}
.hdr-top{display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:10px}
.hdr-title{font-size:15px;font-weight:700;letter-spacing:-.3px}
.hdr-sub{font-size:10px;color:var(--t3);margin-top:1px}
.hdr-day{font-size:12px;color:var(--t2);text-align:right}
.pills{display:flex;gap:5px;overflow-x:auto;padding-bottom:10px;scrollbar-width:none}
.pills::-webkit-scrollbar{display:none}
.pill{flex-shrink:0;background:var(--bg);border:1px solid var(--border);border-radius:20px;padding:4px 11px;font-size:11px;white-space:nowrap}
.pill b{color:var(--green-dk)}

/* ── Tabs ── */
.tabs{display:flex;background:var(--card);border-bottom:1px solid var(--border)}
.tab{flex:1;padding:9px 4px;text-align:center;font-size:10px;color:var(--t3);cursor:pointer;border-bottom:2px solid transparent;transition:all .15s;user-select:none}
.tab.on{color:var(--green-dk);border-color:var(--green);font-weight:700}
.ti{font-size:15px;display:block;margin-bottom:2px}

/* ── Panels ── */
.panel{display:none;padding:14px}
.panel.on{display:block}

/* ── Cards ── */
.card{background:var(--card);border:1px solid var(--border);border-radius:var(--r);padding:14px;margin-bottom:12px}
.card-title{font-size:10px;font-weight:700;color:var(--t3);letter-spacing:.8px;text-transform:uppercase;margin-bottom:11px}

/* ── Form ── */
.fld{margin-bottom:13px}
.fld-lbl{display:flex;justify-content:space-between;align-items:center;font-size:11px;color:var(--t2);margin-bottom:5px}
.badge{font-size:10px;background:var(--bg);border:1px solid var(--border);padding:2px 8px;border-radius:10px;color:var(--t3)}
.sl-row{display:grid;grid-template-columns:1fr auto;gap:12px;align-items:center}
.bignum{font-size:26px;font-weight:700;text-align:right;min-width:64px;line-height:1}
.bignum span{font-size:12px;font-weight:400;color:var(--t3)}
input[type=range]{width:100%;accent-color:var(--green);height:3px;cursor:pointer}
input[type=text],textarea,input[type=date]{width:100%;border:1px solid var(--border);border-radius:var(--rs);padding:8px 10px;background:var(--bg);color:var(--text);outline:none;transition:border .15s}
input:focus,textarea:focus{border-color:var(--green);background:#fff}
textarea{resize:none}

/* ── Buttons ── */
.btn{display:block;width:100%;padding:12px;border-radius:var(--rs);border:none;font-size:13px;font-weight:700;cursor:pointer;transition:opacity .15s;letter-spacing:.3px}
.btn-primary{background:var(--green-dk);color:#fff}
.btn-primary:hover{opacity:.85}
.save-msg{font-size:11px;color:var(--green);text-align:center;margin-top:7px;height:14px}

/* ── Progress bar ── */
.pb-wrap{margin-bottom:9px}
.pb-lbl{display:flex;justify-content:space-between;font-size:11px;color:var(--t2);margin-bottom:4px}
.pb-track{background:var(--border);border-radius:3px;height:6px}
.pb-fill{border-radius:3px;height:6px;transition:width .4s}

/* ── TOC ── */
.toc-part{margin-bottom:14px}
.toc-ph{display:flex;align-items:center;justify-content:space-between;padding:9px 12px;border-radius:var(--rs);margin-bottom:6px;border-left:3px solid transparent}
.toc-ph-name{font-size:12px;font-weight:700}
.toc-ph-ct{font-size:11px;color:var(--t3)}
.toc-items{display:flex;flex-direction:column;gap:4px}
.toc-item{display:flex;align-items:center;gap:10px;padding:9px 12px;border:1px solid var(--border);border-radius:var(--rs);background:var(--card);cursor:pointer;transition:all .12s}
.toc-item.done{background:var(--green-lt);border-color:#9FE1CB}
.chk{width:18px;height:18px;border:2px solid var(--border);border-radius:4px;flex-shrink:0;display:flex;align-items:center;justify-content:center;font-size:11px;color:#fff;transition:all .12s}
.toc-item.done .chk{background:var(--green);border-color:var(--green)}
.toc-name{font-size:12px;flex:1}
.toc-item.done .toc-name{color:var(--green-dk)}

/* ── Week selector ── */
.wk-scroll{display:flex;gap:5px;overflow-x:auto;padding-bottom:8px;margin-bottom:12px;scrollbar-width:none}
.wk-scroll::-webkit-scrollbar{display:none}
.wk-btn{flex-shrink:0;padding:6px 10px;border-radius:20px;border:1px solid var(--border);font-size:10px;cursor:pointer;background:var(--card);color:var(--t3);text-align:center;line-height:1.4;transition:all .12s;font-family:inherit;white-space:nowrap}
.wk-btn.on{background:var(--green-dk);color:#fff;border-color:var(--green-dk);font-weight:700}

/* ── Day rows ── */
.day-row{border:1px solid var(--border);border-radius:var(--rs);padding:10px 12px;margin-bottom:6px;background:var(--card)}
.day-row.has{border-color:#9FE1CB;background:var(--green-lt)}
.day-row-hd{display:flex;justify-content:space-between;align-items:center;margin-bottom:3px}
.day-name{font-size:12px;font-weight:700}
.day-mins{font-size:12px;font-weight:700;color:var(--green-dk)}
.day-detail{font-size:11px;color:var(--t2);margin-top:2px}
.day-empty{font-size:11px;color:var(--t3)}

/* ── Session inputs ── */
.sess-grid{display:grid;grid-template-columns:1fr 54px 54px;gap:6px;align-items:center;margin-bottom:6px}
.sess-cat{font-size:11px;color:var(--t2)}
.mini{border:1px solid var(--border);border-radius:6px;padding:5px 7px;text-align:center;font-size:12px;background:var(--bg);color:var(--text);outline:none;font-family:inherit;width:100%}
.mini:focus{border-color:var(--green);background:#fff}
.sess-hd{display:grid;grid-template-columns:1fr 54px 54px;gap:6px;margin-bottom:4px}
.sess-hd span{font-size:9px;color:var(--t3);text-align:center}
.sess-hd span:first-child{text-align:left}

/* ── Accuracy table ── */
.acc-tbl{width:100%;border-collapse:collapse;font-size:11px}
.acc-tbl th{text-align:left;font-size:9px;color:var(--t3);padding:4px 6px;border-bottom:1px solid var(--border);font-weight:500}
.acc-tbl td{padding:7px 6px;border-bottom:1px solid var(--border);vertical-align:middle}
.acc-bar-wrap{display:flex;align-items:center;gap:8px}
.acc-bar-bg{flex:1;background:var(--border);border-radius:3px;height:5px}
.acc-bar-fill{border-radius:3px;height:5px}
.acc-pct{font-size:11px;font-weight:700;min-width:34px;text-align:right}

/* ── Chart ── */
.chart-wrap{position:relative;height:200px;margin-bottom:6px}
</style>
</head>
<body>
<div class="app">

<!-- HEADER -->
<div class="hdr">
  <div class="hdr-top">
    <div>
      <div class="hdr-title">世界遺産検定2級 学習管理</div>
      <div class="hdr-sub">くわしく学ぶ世界遺産300（2025年3月発行）｜目標：2026年7月12日</div>
    </div>
    <div class="hdr-day" id="hdr-day"></div>
  </div>
  <div class="pills" id="pills"></div>
  <div class="tabs">
    <div class="tab on" onclick="go('rec')"><span class="ti">📅</span>今日</div>
    <div class="tab" onclick="go('toc')"><span class="ti">📚</span>テキスト</div>
    <div class="tab" onclick="go('wk')"><span class="ti">📊</span>週まとめ</div>
    <div class="tab" onclick="go('ch')"><span class="ti">📈</span>成長曲線</div>
  </div>
</div>

<!-- TAB: 今日の記録 -->
<div class="panel on" id="panel-rec">
  <div class="card">
    <div class="card-title">今日の記録</div>
    <div class="fld">
      <div class="fld-lbl"><span>日付</span><span class="badge" id="phase-badge"></span></div>
      <input type="date" id="r-date">
    </div>
    <div class="fld">
      <div class="fld-lbl"><span>勉強時間</span><span class="badge" id="target-badge"></span></div>
      <div class="sl-row">
        <div>
          <input type="range" id="r-mins" min="0" max="180" step="5" value="0"
            oninput="document.getElementById('r-mins-d').textContent=this.value">
          <div style="display:flex;justify-content:space-between;font-size:9px;color:var(--t3);margin-top:3px"><span>0</span><span>90</span><span>180分</span></div>
        </div>
        <div class="bignum"><span id="r-mins-d">0</span><span>分</span></div>
      </div>
    </div>
    <div class="fld">
      <div class="fld-lbl"><span>今日読んだテキストの範囲</span></div>
      <input type="text" id="r-text" placeholder="例：日本の遺産（法隆寺〜姫路城）">
    </div>
  </div>

  <div class="card">
    <div class="card-title">アプリ演習（今日）</div>
    <div class="sess-hd"><span>カテゴリ</span><span>正解数</span><span>問題数</span></div>
    <div id="sess-inputs"></div>
    <div style="font-size:10px;color:var(--t3);margin-top:4px">解かなかったカテゴリは空欄のままでOK</div>
  </div>

  <div class="card">
    <div class="card-title">一言メモ</div>
    <textarea id="r-memo" rows="2" placeholder="今日の気づき・明日やること・感想"></textarea>
  </div>

  <button class="btn btn-primary" onclick="saveDay()">保存する</button>
  <div class="save-msg" id="save-msg"></div>
</div>

<!-- TAB: テキスト進捗 -->
<div class="panel" id="panel-toc">
  <div class="card">
    <div class="card-title">テキスト全体の進捗</div>
    <div class="pb-wrap">
      <div class="pb-lbl"><span>読了セクション</span><span id="toc-ttl">0 / 43</span></div>
      <div class="pb-track"><div class="pb-fill" id="toc-bar" style="width:0%;background:var(--green)"></div></div>
    </div>
    <div id="part-bars"></div>
  </div>
  <div style="font-size:10px;color:var(--t3);margin-bottom:10px;padding:0 2px">
    ※テキストの目次構成を参考にしています。タップで読了をマーク。
  </div>
  <div id="toc-list"></div>
</div>

<!-- TAB: 週まとめ -->
<div class="panel" id="panel-wk">
  <div class="wk-scroll" id="wk-tabs"></div>
  <div id="wk-content"></div>
</div>

<!-- TAB: 成長曲線 -->
<div class="panel" id="panel-ch">
  <div class="card">
    <div class="card-title">累計勉強時間（目標90h）</div>
    <div class="pb-wrap">
      <div class="pb-lbl"><span>進捗</span><span id="ch-hrs-lbl">0h / 90h</span></div>
      <div class="pb-track"><div class="pb-fill" id="ch-hrs-bar" style="width:0%;background:var(--green)"></div></div>
    </div>
    <div class="chart-wrap"><canvas id="chart-daily"></canvas></div>
    <div style="font-size:10px;color:var(--t3);text-align:center">棒グラフ：日別（時間）　折れ線：累計（時間）</div>
  </div>
  <div class="card">
    <div class="card-title">カテゴリ別アプリ正答率（直近）</div>
    <table class="acc-tbl">
      <thead><tr><th>カテゴリ</th><th>正答率</th><th></th></tr></thead>
      <tbody id="acc-tbody"></tbody>
    </table>
  </div>
  <div class="card">
    <div class="card-title">正答率の推移（カテゴリ別）</div>
    <div class="chart-wrap"><canvas id="chart-acc"></canvas></div>
  </div>
</div>

</div><!-- .app -->

<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.js"></script>
<script>
// ─── DATA DEFINITIONS ───────────────────────────────────────

const CATS = [
  '基礎知識','日本の遺産（自然）','日本の遺産（文化）',
  'アジア・太平洋','アラブ諸国','アフリカ','ヨーロッパ・北米','ラテンアメリカ'
];

const TOC = [
  // 基礎知識
  {id:'b1', part:'基礎知識', name:'世界遺産とは・世界遺産条約の成立と目的'},
  {id:'b2', part:'基礎知識', name:'登録基準（OUV）・10項目の内容'},
  {id:'b3', part:'基礎知識', name:'登録のプロセス・推薦書・諮問機関（ICOMOS・IUCN）'},
  {id:'b4', part:'基礎知識', name:'世界遺産委員会・危機遺産リスト・抹消'},
  {id:'b5', part:'基礎知識', name:'文化遺産・自然遺産・複合遺産の分類'},
  {id:'b6', part:'基礎知識', name:'文化的景観・シリアル・越境（トランスバウンダリー）'},
  {id:'b7', part:'基礎知識', name:'真正性・完全性・保全と管理計画'},
  // 日本（自然）
  {id:'jn1', part:'日本の遺産（自然）', name:'屋久島'},
  {id:'jn2', part:'日本の遺産（自然）', name:'白神山地'},
  {id:'jn3', part:'日本の遺産（自然）', name:'知床'},
  {id:'jn4', part:'日本の遺産（自然）', name:'小笠原諸島'},
  {id:'jn5', part:'日本の遺産（自然）', name:'奄美大島・徳之島・沖縄島北部及び西表島'},
  // 日本（文化）
  {id:'jc1',  part:'日本の遺産（文化）', name:'法隆寺地域の仏教建造物群'},
  {id:'jc2',  part:'日本の遺産（文化）', name:'姫路城'},
  {id:'jc3',  part:'日本の遺産（文化）', name:'古都京都の文化財'},
  {id:'jc4',  part:'日本の遺産（文化）', name:'白川郷・五箇山の合掌造り集落'},
  {id:'jc5',  part:'日本の遺産（文化）', name:'広島平和記念碑（原爆ドーム）'},
  {id:'jc6',  part:'日本の遺産（文化）', name:'厳島神社'},
  {id:'jc7',  part:'日本の遺産（文化）', name:'古都奈良の文化財'},
  {id:'jc8',  part:'日本の遺産（文化）', name:'日光の社寺'},
  {id:'jc9',  part:'日本の遺産（文化）', name:'琉球王国のグスク及び関連遺産群'},
  {id:'jc10', part:'日本の遺産（文化）', name:'紀伊山地の霊場と参詣道'},
  {id:'jc11', part:'日本の遺産（文化）', name:'石見銀山遺跡とその文化的景観'},
  {id:'jc12', part:'日本の遺産（文化）', name:'平泉'},
  {id:'jc13', part:'日本の遺産（文化）', name:'富士山'},
  {id:'jc14', part:'日本の遺産（文化）', name:'富岡製糸場と絹産業遺産群'},
  {id:'jc15', part:'日本の遺産（文化）', name:'明治日本の産業革命遺産'},
  {id:'jc16', part:'日本の遺産（文化）', name:'ル・コルビュジエの建築作品'},
  {id:'jc17', part:'日本の遺産（文化）', name:'「神宿る島」宗像・沖ノ島と関連遺産群'},
  {id:'jc18', part:'日本の遺産（文化）', name:'長崎と天草地方の潜伏キリシタン関連遺産'},
  {id:'jc19', part:'日本の遺産（文化）', name:'百舌鳥・古市古墳群'},
  {id:'jc20', part:'日本の遺産（文化）', name:'北海道・北東北の縄文遺跡群'},
  {id:'jc21', part:'日本の遺産（文化）', name:'佐渡島（さど）の金山'},
  // 世界の遺産
  {id:'wa1', part:'アジア・太平洋', name:'中国・韓国・モンゴルの遺産'},
  {id:'wa2', part:'アジア・太平洋', name:'東南アジアの遺産（カンボジア・タイ・ベトナム他）'},
  {id:'wa3', part:'アジア・太平洋', name:'南アジア・オセアニアの遺産'},
  {id:'wr1', part:'アラブ諸国', name:'アラブ諸国の遺産'},
  {id:'wf1', part:'アフリカ', name:'アフリカの遺産（前半）'},
  {id:'wf2', part:'アフリカ', name:'アフリカの遺産（後半）'},
  {id:'we1', part:'ヨーロッパ・北米', name:'ヨーロッパの遺産（前半：南欧・西欧）'},
  {id:'we2', part:'ヨーロッパ・北米', name:'ヨーロッパの遺産（中盤：中欧・東欧）'},
  {id:'we3', part:'ヨーロッパ・北米', name:'ヨーロッパの遺産（後半：北欧）・北米'},
  {id:'wl1', part:'ラテンアメリカ', name:'ラテンアメリカ・カリブ海の遺産'},
];
const PARTS = [...new Set(TOC.map(t => t.part))];
const PART_COL = {
  '基礎知識':'#1D9E75','日本の遺産（自然）':'#7F77DD','日本の遺産（文化）':'#534AB7',
  'アジア・太平洋':'#3aad82','アラブ諸国':'#D85A30','アフリカ':'#BA7517',
  'ヨーロッパ・北米':'#378ADD','ラテンアメリカ':'#E24B4A'
};

const WEEKS = [
  {n:1, s:'2026-04-03',e:'2026-04-09', ph:'1周目',  tgt:300},
  {n:2, s:'2026-04-10',e:'2026-04-16', ph:'1周目',  tgt:300},
  {n:3, s:'2026-04-17',e:'2026-04-23', ph:'2周目',  tgt:360},
  {n:4, s:'2026-04-24',e:'2026-04-30', ph:'2周目',  tgt:360},
  {n:5, s:'2026-05-01',e:'2026-05-07', ph:'3周目',  tgt:420},
  {n:6, s:'2026-05-08',e:'2026-05-14', ph:'3周目',  tgt:420},
  {n:7, s:'2026-05-15',e:'2026-05-21', ph:'3周目',  tgt:420},
  {n:8, s:'2026-05-22',e:'2026-05-28', ph:'4周目',  tgt:420},
  {n:9, s:'2026-05-29',e:'2026-06-04', ph:'4周目',  tgt:420},
  {n:10,s:'2026-06-05',e:'2026-06-11', ph:'5周目',  tgt:360},
  {n:11,s:'2026-06-12',e:'2026-06-18', ph:'弱点補強',tgt:420},
  {n:12,s:'2026-06-19',e:'2026-06-25', ph:'過去問', tgt:420},
  {n:13,s:'2026-06-26',e:'2026-07-02', ph:'過去問', tgt:420},
  {n:14,s:'2026-07-03',e:'2026-07-11', ph:'仕上げ', tgt:300},
];

// ─── STORAGE ────────────────────────────────────────────────
const get  = k => { try { return JSON.parse(localStorage.getItem(k)); } catch { return null; } };
const save = (k,v) => { try { localStorage.setItem(k,JSON.stringify(v)); } catch {} };
const getDay  = ds => get('sk2_d_'+ds) || {mins:0,text:'',sess:{},memo:''};
const saveDay_= (ds,d) => save('sk2_d_'+ds,d);
const getToc  = () => get('sk2_toc') || {};
const saveToc = t => save('sk2_toc',t);

// ─── HELPERS ────────────────────────────────────────────────
const toDay = d => {
  const [y,m,dy] = [d.getFullYear(), String(d.getMonth()+1).padStart(2,'0'), String(d.getDate()).padStart(2,'0')];
  return `${y}-${m}-${dy}`;
};
const todayStr = () => toDay(new Date());
const dayLabel = ds => {
  const d = new Date(ds+'T00:00:00');
  return ['日','月','火','水','木','金','土'][d.getDay()]+'('+( d.getMonth()+1)+'/'+d.getDate()+')';
};
const dateRange = (s,e) => {
  const out=[], d=new Date(s+'T00:00:00'), ed=new Date(e+'T00:00:00');
  while(d<=ed){ out.push(toDay(d)); d.setDate(d.getDate()+1); }
  return out;
};
const weekOf = ds => {
  const d = new Date(ds+'T00:00:00');
  return WEEKS.find(w => d>=new Date(w.s+'T00:00:00') && d<=new Date(w.e+'T00:00:00'));
};
const totalMins = () => {
  let t=0;
  for(let i=0;i<localStorage.length;i++){
    const k=localStorage.key(i);
    if(k&&k.startsWith('sk2_d_')){const d=get(k);if(d)t+=d.mins||0;}
  }
  return t;
};
const allDays = () => {
  const out=[];
  for(let i=0;i<localStorage.length;i++){
    const k=localStorage.key(i);
    if(k&&k.startsWith('sk2_d_'))out.push(k.replace('sk2_d_',''));
  }
  return out.sort();
};
const catAccTrend = cat => {
  return allDays()
    .map(ds=>{const d=getDay(ds);return d.sess&&d.sess[cat]!=null?{ds,pct:d.sess[cat]}:null;})
    .filter(Boolean);
};
const latestAcc = () => {
  const r={};
  for(const cat of CATS){
    const tr=catAccTrend(cat);
    if(tr.length)r[cat]=tr[tr.length-1].pct;
  }
  return r;
};

// ─── HEADER ─────────────────────────────────────────────────
function renderHeader(){
  const td=todayStr();
  const [y,m,d]=td.split('-');
  document.getElementById('hdr-day').textContent=`${y}/${m}/${d}`;
  const tm=totalMins(), th=(tm/60).toFixed(1);
  const toc=getToc(), done=TOC.filter(t=>toc[t.id]).length;
  const cw=weekOf(td);
  const la=latestAcc();
  const overallAcc=Object.values(la).length?Math.round(Object.values(la).reduce((a,b)=>a+b,0)/Object.values(la).length):null;
  document.getElementById('pills').innerHTML=[
    `<div class="pill">累計 <b>${th}h</b> / 90h</div>`,
    `<div class="pill">テキスト <b>${done}/${TOC.length}</b> 節</div>`,
    overallAcc!=null?`<div class="pill">アプリ平均 <b>${overallAcc}%</b></div>`:'',
    cw?`<div class="pill"><b>${cw.ph}</b> W${cw.n}</div>`:'',
  ].join('');
}

// ─── TAB SWITCHING ──────────────────────────────────────────
let curTab='rec', curWk=1;
function go(tab){
  curTab=tab;
  document.querySelectorAll('.tab').forEach((t,i)=>t.classList.toggle('on',['rec','toc','wk','ch'][i]===tab));
  document.querySelectorAll('.panel').forEach(p=>p.classList.remove('on'));
  document.getElementById('panel-'+tab).classList.add('on');
  if(tab==='toc')renderToc();
  if(tab==='wk')renderWk();
  if(tab==='ch')renderCharts();
}

// ─── RECORD TAB ─────────────────────────────────────────────
function initRec(){
  const td=todayStr();
  document.getElementById('r-date').value=td;
  loadDay(td);
  document.getElementById('r-date').addEventListener('change',e=>loadDay(e.target.value));
}
function loadDay(ds){
  const d=getDay(ds);
  document.getElementById('r-mins').value=d.mins||0;
  document.getElementById('r-mins-d').textContent=d.mins||0;
  document.getElementById('r-text').value=d.text||'';
  document.getElementById('r-memo').value=d.memo||'';
  renderSessInputs(d.sess||{});
  const w=weekOf(ds);
  document.getElementById('phase-badge').textContent=w?w.ph+' W'+w.n:'期間外';
  document.getElementById('target-badge').textContent=w?'週目標 '+Math.round(w.tgt/60)+'h':'—';
}
function renderSessInputs(sess){
  document.getElementById('sess-inputs').innerHTML=CATS.map((cat,i)=>`
    <div class="sess-grid">
      <div class="sess-cat">${cat}</div>
      <input class="mini" type="number" min="0" max="999" placeholder="—" id="sc${i}" value="${sess[i+'_c']!=null?sess[i+'_c']:''}">
      <input class="mini" type="number" min="1" max="999" placeholder="—" id="sn${i}" value="${sess[i+'_n']!=null?sess[i+'_n']:''}">
    </div>`).join('');
}
function saveDay(){
  const ds=document.getElementById('r-date').value;
  const mins=parseInt(document.getElementById('r-mins').value)||0;
  const text=document.getElementById('r-text').value;
  const memo=document.getElementById('r-memo').value;
  const sess={};
  CATS.forEach((cat,i)=>{
    const c=parseInt(document.getElementById('sc'+i)?.value);
    const n=parseInt(document.getElementById('sn'+i)?.value);
    if(!isNaN(c)&&!isNaN(n)&&n>0){
      sess[i+'_c']=c; sess[i+'_n']=n;
      sess[cat]=Math.round(c/n*100);
    }
  });
  saveDay_(ds,{mins,text,sess,memo});
  renderHeader();
  const m=document.getElementById('save-msg');
  m.textContent='✓ 保存しました';
  setTimeout(()=>m.textContent='',2200);
}

// ─── TOC TAB ────────────────────────────────────────────────
function renderToc(){
  const toc=getToc();
  const done=TOC.filter(t=>toc[t.id]).length, total=TOC.length;
  document.getElementById('toc-ttl').textContent=`${done} / ${total}`;
  document.getElementById('toc-bar').style.width=(done/total*100).toFixed(0)+'%';
  document.getElementById('part-bars').innerHTML=PARTS.map(p=>{
    const items=TOC.filter(t=>t.part===p);
    const pd=items.filter(t=>toc[t.id]).length;
    const col=PART_COL[p]||'#1D9E75';
    return `<div class="pb-wrap">
      <div class="pb-lbl"><span style="font-size:11px">${p}</span><span>${pd}/${items.length}</span></div>
      <div class="pb-track"><div class="pb-fill" style="width:${(pd/items.length*100).toFixed(0)}%;background:${col}"></div></div>
    </div>`;
  }).join('');
  document.getElementById('toc-list').innerHTML=PARTS.map(p=>{
    const items=TOC.filter(t=>t.part===p);
    const col=PART_COL[p]||'#1D9E75';
    const pd=items.filter(t=>toc[t.id]).length;
    return `<div class="toc-part">
      <div class="toc-ph" style="border-left-color:${col};background:${col}18">
        <span class="toc-ph-name">${p}</span>
        <span class="toc-ph-ct">${pd}/${items.length} 完了</span>
      </div>
      <div class="toc-items">${items.map(t=>{
        const d=!!toc[t.id];
        return `<div class="toc-item ${d?'done':''}" onclick="toggleToc('${t.id}')">
          <div class="chk">${d?'✓':''}</div>
          <div class="toc-name">${t.name}</div>
        </div>`;
      }).join('')}</div>
    </div>`;
  }).join('');
}
function toggleToc(id){
  const toc=getToc(); toc[id]=!toc[id]; saveToc(toc);
  renderToc(); renderHeader();
}

// ─── WEEK SUMMARY TAB ───────────────────────────────────────
function renderWk(){
  const td=todayStr();
  const cw=weekOf(td);
  if(cw&&curWk===1)curWk=cw.n;
  document.getElementById('wk-tabs').innerHTML=WEEKS.map(w=>`
    <div class="wk-btn ${w.n===curWk?'on':''}" onclick="pickWk(${w.n})">W${w.n}<br><span style="font-size:9px;opacity:.8">${w.ph}</span></div>`).join('');
  const w=WEEKS[curWk-1];
  const days=dateRange(w.s,w.e);
  let weekMins=0;
  const rows=days.map(ds=>{
    const d=getDay(ds); weekMins+=d.mins||0;
    const has=d.mins>0||d.memo;
    const accParts=CATS.map((cat,i)=>d.sess&&d.sess[cat]!=null?`${cat}：${d.sess[cat]}%`:null).filter(Boolean);
    return `<div class="day-row ${has?'has':''}">
      <div class="day-row-hd">
        <div class="day-name">${dayLabel(ds)}</div>
        ${d.mins>0?`<div class="day-mins">${d.mins}分（${(d.mins/60).toFixed(1)}h）</div>`:'<div class="day-empty">未記録</div>'}
      </div>
      ${d.text?`<div class="day-detail">📖 ${d.text}</div>`:''}
      ${accParts.length?`<div class="day-detail">🎯 ${accParts.join('　')}</div>`:''}
      ${d.memo?`<div class="day-detail">📝 ${d.memo}</div>`:''}
    </div>`;
  }).join('');
  const pct=Math.min(100,weekMins/w.tgt*100).toFixed(0);
  document.getElementById('wk-content').innerHTML=`
    <div class="card">
      <div class="card-title">W${w.n}（${w.s.slice(5).replace('-','/')}〜${w.e.slice(5).replace('-','/')}）${w.ph}</div>
      <div class="pb-wrap">
        <div class="pb-lbl"><span>週合計 ${weekMins}分（${(weekMins/60).toFixed(1)}h）</span><span>目標 ${Math.round(w.tgt/60)}h</span></div>
        <div class="pb-track"><div class="pb-fill" style="width:${pct}%;background:${weekMins>=w.tgt?'var(--green)':'var(--amber)'}"></div></div>
      </div>
    </div>${rows}`;
}
function pickWk(n){ curWk=n; renderWk(); }

// ─── CHARTS ─────────────────────────────────────────────────
let chDaily=null, chAcc=null;
function renderCharts(){
  const tm=totalMins(), th=(tm/60).toFixed(1);
  document.getElementById('ch-hrs-lbl').textContent=`${th}h / 90h`;
  document.getElementById('ch-hrs-bar').style.width=Math.min(100,tm/5400*100).toFixed(0)+'%';

  // Build date series from plan start to today
  const start=new Date('2026-04-03T00:00:00');
  const stop=new Date(Math.min(new Date(),new Date('2026-07-11T00:00:00')));
  const labels=[],bars=[],line=[];
  let cum=0; const d=new Date(start);
  while(d<=stop){
    const ds=toDay(d);
    const rec=getDay(ds); const m=rec.mins||0; cum+=m;
    if(d.getDay()===0||d.getDate()===1)labels.push((d.getMonth()+1)+'/'+d.getDate());
    else labels.push('');
    bars.push(+(m/60).toFixed(2));
    line.push(+(cum/60).toFixed(2));
    d.setDate(d.getDate()+1);
  }

  if(chDaily)chDaily.destroy();
  chDaily=new Chart(document.getElementById('chart-daily').getContext('2d'),{
    data:{labels,datasets:[
      {type:'bar',label:'日別(h)',data:bars,backgroundColor:'#9FE1CB',order:2},
      {type:'line',label:'累計(h)',data:line,borderColor:'#1D9E75',backgroundColor:'transparent',borderWidth:2,pointRadius:0,order:1},
    ]},
    options:{responsive:true,maintainAspectRatio:false,
      plugins:{legend:{display:false}},
      scales:{x:{ticks:{font:{size:9}},grid:{display:false}},y:{ticks:{font:{size:9}},grid:{color:'#ece9e0'}}}}
  });

  // Accuracy table
  const la=latestAcc();
  document.getElementById('acc-tbody').innerHTML=CATS.map(cat=>{
    const pct=la[cat];
    if(pct==null)return`<tr><td>${cat}</td><td colspan="2" style="color:var(--t3);font-size:11px">未記録</td></tr>`;
    const col=pct>=80?'var(--green)':pct>=60?'var(--amber)':'var(--red)';
    return`<tr><td>${cat}</td><td>
      <div class="acc-bar-wrap"><div class="acc-bar-bg"><div class="acc-bar-fill" style="width:${pct}%;background:${col}"></div></div>
      <span class="acc-pct" style="color:${col}">${pct}%</span></div></td></tr>`;
  }).join('');

  // Accuracy trend
  const colors=['#1D9E75','#7F77DD','#534AB7','#3aad82','#D85A30','#BA7517','#378ADD','#E24B4A'];
  const datasets=CATS.map((cat,i)=>{
    const tr=catAccTrend(cat);
    if(!tr.length)return null;
    return{label:cat,data:tr.map(a=>({x:a.ds.slice(5).replace('-','/'),y:a.pct})),
      borderColor:colors[i],backgroundColor:'transparent',borderWidth:2,pointRadius:3,tension:.3};
  }).filter(Boolean);

  if(chAcc)chAcc.destroy();
  const ctx=document.getElementById('chart-acc').getContext('2d');
  if(datasets.length){
    chAcc=new Chart(ctx,{type:'line',data:{datasets},
      options:{responsive:true,maintainAspectRatio:false,
        plugins:{legend:{position:'bottom',labels:{font:{size:9},boxWidth:8,padding:8}}},
        scales:{x:{type:'category',ticks:{font:{size:9},maxTicksLimit:6},grid:{display:false}},
                y:{min:0,max:100,ticks:{font:{size:9},callback:v=>v+'%'},grid:{color:'#ece9e0'}}}}});
  } else {
    ctx.canvas.parentElement.innerHTML='<div style="text-align:center;padding:50px 0;color:var(--t3);font-size:12px">演習データを入力するとグラフが表示されます</div>';
  }
}

// ─── INIT ───────────────────────────────────────────────────
renderHeader();
initRec();
const cw=weekOf(todayStr());
if(cw)curWk=cw.n;
</script>
</body>
</html>
