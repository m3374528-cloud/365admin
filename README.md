[index.html](https://github.com/user-attachments/files/27939477/index.html)
<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<title>365 관리자</title>
<style>
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',sans-serif;font-size:14px;color:#1a1a1a;background:#f5f5f0}
.tab-bar{display:flex;background:#fff;border-bottom:0.5px solid #e0e0d8;position:sticky;top:0;z-index:100}
.tab{flex:1;padding:12px 4px;text-align:center;font-size:11px;font-weight:500;color:#888;cursor:pointer;border-bottom:2px solid transparent}
.tab.on{color:#1D9E75;border-bottom:2px solid #1D9E75}
.page{display:none;padding:12px}
.page.on{display:block}
.section{background:#fff;border:0.5px solid #e0e0d8;border-radius:12px;padding:1rem;margin-bottom:12px;overflow:visible}
.sec-title{font-size:12px;font-weight:500;color:#888;margin-bottom:10px;padding-bottom:6px;border-bottom:0.5px solid #eee}
input,select,textarea{width:100%;padding:8px 10px;border:0.5px solid #ccc;border-radius:8px;font-size:13px;background:#fff;color:#1a1a1a;font-family:inherit}
.lbl{font-size:12px;color:#888;margin-bottom:4px;margin-top:8px}
.row2{display:grid;grid-template-columns:1fr 1fr;gap:8px}
.btn{padding:10px 16px;border:none;border-radius:8px;font-size:13px;font-weight:500;cursor:pointer}
.btn-green{background:#1D9E75;color:#fff}
.btn-blue{background:#185FA5;color:#fff}
.btn-gray{background:#f5f5f0;color:#555}
.btn-red{background:#FCEBEB;color:#A32D2D}
.btn-yellow{background:#FEF3E2;color:#C17D20}
.btn-full{width:100%;padding:14px;font-size:14px}
.loading{display:none;position:fixed;top:0;left:0;width:100%;height:100%;background:rgba(0,0,0,0.5);z-index:999;align-items:center;justify-content:center;flex-direction:column;gap:12px}
.loading.show{display:flex}
.loading-text{color:#fff;font-size:15px;font-weight:500}
.spinner{width:40px;height:40px;border:3px solid rgba(255,255,255,0.3);border-top:3px solid #fff;border-radius:50%;animation:spin 0.8s linear infinite}
@keyframes spin{to{transform:rotate(360deg)}}

/* 로그인 */
.login-wrap{min-height:100vh;display:flex;align-items:center;justify-content:center;padding:20px}
.login-box{background:#fff;border-radius:16px;padding:2rem;width:100%;max-width:320px;text-align:center;box-shadow:0 4px 20px rgba(0,0,0,0.08)}
.login-title{font-size:22px;font-weight:500;color:#1D9E75;margin-bottom:6px}
.login-sub{font-size:13px;color:#888;margin-bottom:24px}
.pin-wrap{display:flex;gap:10px;justify-content:center;margin-bottom:20px}
.pin-dot{width:16px;height:16px;border-radius:50%;background:#eee;border:2px solid #ddd;transition:all 0.2s}
.pin-dot.filled{background:#1D9E75;border-color:#1D9E75}
.keypad{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;margin-bottom:12px}
.key{padding:16px;background:#f5f5f0;border:none;border-radius:12px;font-size:18px;font-weight:500;cursor:pointer;color:#1a1a1a;transition:all 0.1s}
.key:active{background:#e0e0d8;transform:scale(0.95)}
.key-del{background:#FCEBEB;color:#A32D2D}
.login-err{color:#A32D2D;font-size:12px;min-height:18px;margin-top:4px}

/* 달력 */
.cal-header{display:flex;align-items:center;justify-content:space-between;margin-bottom:12px}
.cal-nav{background:none;border:none;font-size:20px;cursor:pointer;color:#1D9E75;padding:4px 10px}
.cal-title{font-size:16px;font-weight:500}
.cal-grid{display:grid;grid-template-columns:repeat(7,1fr);gap:3px}
.cal-dow{text-align:center;font-size:11px;color:#888;padding:4px 0}
.cal-day{min-height:60px;background:#fff;border:0.5px solid #eee;border-radius:6px;padding:4px;cursor:pointer;transition:all 0.15s;overflow:hidden}
.cal-day:hover{background:#f0fbf7}
.cal-day.other-month{opacity:0.3}
.cal-day.today{border-color:#1D9E75;border-width:1.5px}
.cal-date{font-size:11px;font-weight:500;margin-bottom:3px}
.cal-item{font-size:9px;padding:2px 4px;border-radius:4px;margin-bottom:1px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.cal-item.red{background:#FCEBEB;color:#A32D2D}
.cal-item.yellow{background:#FEF3E2;color:#C17D20}
.cal-item.green{background:#E1F5EE;color:#0F6E56}
.cal-item.gray{background:#f5f5f0;color:#888}

/* 팝업 */
.popup-overlay{display:none;position:fixed;top:0;left:0;width:100%;height:100%;background:rgba(0,0,0,0.5);z-index:200;align-items:flex-end;justify-content:center}
.popup-overlay.show{display:flex}
.popup-box{background:#fff;border-radius:16px 16px 0 0;padding:1.5rem;width:100%;max-width:500px;max-height:85vh;overflow-y:auto}
.popup-title{font-size:15px;font-weight:500;margin-bottom:16px;padding-bottom:10px;border-bottom:0.5px solid #eee;display:flex;justify-content:space-between;align-items:center}
.popup-close{background:none;border:none;font-size:22px;color:#888;cursor:pointer}
.record-card{background:#f5f5f0;border-radius:10px;padding:12px;margin-bottom:10px}
.record-title{font-size:13px;font-weight:500;margin-bottom:6px;color:#1a1a1a}
.record-row{display:flex;justify-content:space-between;font-size:12px;color:#666;padding:2px 0}
.status-btns{display:flex;gap:6px;margin-top:10px}
.status-btn{flex:1;padding:8px;border:none;border-radius:8px;font-size:12px;font-weight:500;cursor:pointer}
.status-btn.expense-ok{background:#E1F5EE;color:#0F6E56}
.status-btn.expense-done{background:#1D9E75;color:#fff}
.status-btn.equip-ok{background:#E6F1FB;color:#0C447C}
.status-btn.equip-done{background:#185FA5;color:#fff}

/* 미제출 */
.unsub-card{background:#fff;border:0.5px solid #e0e0d8;border-radius:10px;padding:12px;margin-bottom:8px;display:flex;justify-content:space-between;align-items:center}
.unsub-info{flex:1}
.unsub-title{font-size:13px;font-weight:500;color:#1a1a1a}
.unsub-sub{font-size:11px;color:#888;margin-top:2px}
.unsub-days{font-size:11px;color:#A32D2D;font-weight:500}
.empty{text-align:center;padding:40px 20px;color:#888;font-size:13px}

/* 대리작성 */
.chip{padding:7px 12px;border-radius:20px;border:0.5px solid #ccc;font-size:12px;cursor:pointer;background:#fff;color:#1a1a1a;transition:all 0.15s;white-space:nowrap}
.chip.on{background:#1D9E75;border-color:#1D9E75;color:#fff}
.chip-wrap{display:flex;flex-wrap:wrap;gap:6px}
.card-chip{padding:8px 10px;border-radius:8px;border:0.5px solid #ccc;font-size:12px;cursor:pointer;background:#fff;color:#1a1a1a;text-align:center}
.card-chip.on{background:#185FA5;border-color:#185FA5;color:#fff}
.add-btn{width:100%;padding:8px;border:0.5px dashed #ccc;border-radius:8px;background:transparent;color:#888;font-size:13px;cursor:pointer;margin-top:8px}
.item-box{border:0.5px solid #eee;border-radius:8px;padding:10px;margin-top:8px;position:relative}
.del-btn{position:absolute;top:8px;right:8px;background:none;border:none;color:#bbb;cursor:pointer;font-size:18px;line-height:1;padding:0}
.vat-box{margin-top:8px;padding:10px 12px;background:#f5f5f0;border-radius:8px;display:none}
.vat-row{display:flex;justify-content:space-between;align-items:center;padding:3px 0;font-size:12px}
.vat-total{border-top:0.5px solid #ddd;margin-top:4px;padding-top:6px;font-weight:500}
.time-row{display:flex;align-items:center;gap:6px}
.time-row span{color:#888;font-size:13px;flex-shrink:0}
.check-row{display:flex;align-items:center;gap:8px;margin:8px 0}
.check-row label{font-size:13px;color:#555;cursor:pointer}
input[type=checkbox]{width:16px!important;height:16px;cursor:pointer;flex-shrink:0}
.complete-box{display:none;background:#E1F5EE;border:0.5px solid #1D9E75;border-radius:12px;padding:1.5rem;margin-bottom:12px;text-align:center}
.complete-box.show{display:block}
.new-btn{width:100%;padding:12px;background:#1D9E75;color:#fff;border:none;border-radius:10px;font-size:14px;font-weight:500;cursor:pointer;margin-top:12px}
.req{color:#E24B4A;margin-left:2px}
</style>
</head>
<body>

<div class="loading" id="loading">
  <div class="spinner"></div>
  <div class="loading-text" id="loading-text">불러오는 중...</div>
</div>

<!-- 관리자 메인 -->
<div id="admin-wrap">
  <div class="tab-bar">
    <div class="tab on" id="tab-cal" onclick="switchTab('cal')">📅 달력</div>
    <div class="tab" id="tab-unsub" onclick="switchTab('unsub')">⚠️ 미제출</div>
    <div class="tab" id="tab-write" onclick="switchTab('write')">✏️ 대리작성</div>
    <div class="tab" id="tab-status" onclick="switchTab('status')">📊 현황</div>
  </div>

  <!-- 달력 탭 -->
  <div class="page on" id="page-cal">
    <div style="padding:12px 0 8px;display:flex;justify-content:space-between;align-items:center">
      <p style="font-size:16px;font-weight:500">경비 달력</p>
      <button onclick="loadCalendar()" class="btn btn-green" style="padding:6px 12px;font-size:12px">새로고침</button>
    </div>
    <div class="section" style="padding:0.8rem;min-height:400px">
      <div class="cal-header">
        <button class="cal-nav" onclick="changeMonth(-1)">‹</button>
        <div class="cal-title" id="cal-title"></div>
        <button class="cal-nav" onclick="changeMonth(1)">›</button>
      </div>
      <div class="cal-grid" id="cal-dow">
        <div class="cal-dow">일</div><div class="cal-dow">월</div><div class="cal-dow">화</div>
        <div class="cal-dow">수</div><div class="cal-dow">목</div><div class="cal-dow">금</div>
        <div class="cal-dow">토</div>
      </div>
      <div class="cal-grid" id="cal-grid"></div>
    </div>
    <div style="display:flex;gap:6px;flex-wrap:wrap;margin-bottom:12px">
      <span style="font-size:11px;background:#FCEBEB;color:#A32D2D;padding:3px 8px;border-radius:6px">🔴 미확인</span>
      <span style="font-size:11px;background:#FEF3E2;color:#C17D20;padding:3px 8px;border-radius:6px">🟡 부분완료</span>
      <span style="font-size:11px;background:#E1F5EE;color:#0F6E56;padding:3px 8px;border-radius:6px">🟢 완료</span>
      <span style="font-size:11px;background:#f5f5f0;color:#888;padding:3px 8px;border-radius:6px">⬜ 경비없음</span>
    </div>
  </div>

  <!-- 미제출 탭 -->
  <div class="page" id="page-unsub">
    <div style="padding:12px 0 8px;display:flex;justify-content:space-between;align-items:center">
      <p style="font-size:16px;font-weight:500">⚠️ 미제출 현장</p>
      <button onclick="loadUnsubmitted()" class="btn btn-green" style="padding:6px 12px;font-size:12px">새로고침</button>
    </div>
    <div id="unsub-list"></div>
  </div>

  <!-- 대리작성 탭 -->
  <div class="page" id="page-write">
    <div style="padding:12px 0 4px"><p style="font-size:16px;font-weight:500">✏️ 대리 작성</p></div>
    <div class="complete-box" id="write-complete">
      <div style="font-size:18px;font-weight:500;color:#0F6E56;margin-bottom:8px">✅ 제출 완료!</div>
      <div style="font-size:13px;color:#1D9E75" id="write-complete-desc"></div>
      <button class="new-btn" onclick="resetWriteForm()">새로 작성하기</button>
    </div>
    <div id="write-form">
      <div class="section">
        <div class="sec-title">작업 날짜 <span class="req">*</span></div>
        <input type="date" id="w-date">
      </div>
      <div class="section">
        <div class="sec-title">프로젝트 <span class="req">*</span></div>
        <select id="w-proj"><option value="">— 프로젝트 선택 —</option></select>
      </div>
      <div class="section">
        <div class="sec-title">투입 작업자</div>
        <div class="chip-wrap" id="w-workers"></div>
        <div class="lbl">추가 인원</div>
        <input type="text" id="w-extra" placeholder="추가 작업자 이름 (쉼표로 구분)">
      </div>
      <div class="section">
        <div class="sec-title">작업 시간</div>
        <div class="time-row">
          <select id="w-tstart" style="flex:1"></select>
          <span>~</span>
          <select id="w-tend" style="flex:1"></select>
        </div>
        <div class="check-row" style="margin-top:8px">
          <input type="checkbox" id="w-ot" onchange="toggleWriteOT(this)">
          <label for="w-ot">잔업 있음</label>
        </div>
        <div id="w-ot-wrap" style="display:none">
          <div class="time-row">
            <select id="w-otstart" style="flex:1"></select>
            <span>~</span>
            <select id="w-otend" style="flex:1"></select>
          </div>
        </div>
      </div>
      <div class="section">
        <div class="sec-title">경비 사용 내역</div>
        <div class="check-row">
          <input type="checkbox" id="w-noexp" onchange="toggleWriteNoExp(this)">
          <label for="w-noexp">경비 사용 없음</label>
        </div>
        <div id="w-exp-body">
          <div class="lbl">사용 카드</div>
          <div style="display:grid;grid-template-columns:1fr 1fr;gap:6px;margin-top:6px" id="w-cards"></div>
          <div class="lbl" style="margin-top:10px">경비 내역</div>
          <div id="w-exp-list"></div>
          <button class="add-btn" onclick="addWriteExp()">+ 경비 항목 추가</button>
        </div>
      </div>
      <div class="section">
        <div class="sec-title">장비 / 외주</div>
        <div id="w-equip-list"></div>
        <button class="add-btn" onclick="addWriteEquip()">+ 항목 추가</button>
        <div class="check-row" style="margin-top:8px">
          <input type="checkbox" id="w-noinv">
          <label for="w-noinv">거래명세서 없음</label>
        </div>
      </div>
      <div class="section">
        <div class="sec-title">작성자 <span class="req">*</span></div>
        <input type="text" id="w-writer" placeholder="작성자 이름">
      </div>
      <div style="padding-bottom:30px">
        <button class="btn btn-green btn-full" onclick="submitWrite()">제출하기</button>
      </div>
    </div>
  </div>

  <!-- 현황 탭 -->
  <div class="page" id="page-status">
    <div style="padding:12px 0 8px;display:flex;justify-content:space-between;align-items:center">
      <p style="font-size:16px;font-weight:500">📊 현황</p>
      <button onclick="loadTodayStatus()" class="btn btn-green" style="padding:6px 12px;font-size:12px">새로고침</button>
    </div>
    <div class="section">
      <div class="sec-title" style="display:flex;justify-content:space-between;align-items:center">
        날짜별 조회
        <input type="date" id="status-date" style="width:auto;font-size:12px;padding:4px 8px" onchange="loadDateStatus()">
      </div>
      <div id="date-status"></div>
    </div>
    <div class="section">
      <div class="sec-title" style="display:flex;justify-content:space-between;align-items:center">
        월별 경비 합계
        <input type="month" id="status-month" style="width:auto;font-size:12px;padding:4px 8px" onchange="loadMonthStatus()">
      </div>
      <div id="month-status"></div>
    </div>
  </div>
</div>

<!-- 팝업 -->
<div class="popup-overlay" id="popup" onclick="closePopup(event)">
  <div class="popup-box">
    <div class="popup-title">
      <span id="popup-title-text"></span>
      <button class="popup-close" onclick="closePopupDirect()">×</button>
    </div>
    <div id="popup-content"></div>
  </div>
</div>

<script>
const SCRIPT_URL='https://script.google.com/macros/s/AKfycbzNI4xmJT7kaA06gosQ2BE6kg8i5i1M-z_4tq3jsr32-nftkN0sH86ox9xEmVo0oe9IoQ/exec';

let masterData={projects:[],workers:[],cards:[],expenseItems:[],equipments:[]};
let calYear=new Date().getFullYear();
let calMonth=new Date().getMonth();
let calData={};
let wExpCount=0,wEqCount=0;

// 로그인 없이 바로 시작
window.onload = function(){ initAdmin(); }

// ========== 초기화 ==========
async function initAdmin(){
  showLoading('데이터 불러오는 중...');
  try {
    const [proj,workers,cards,items,equip]=await Promise.all([
      fetch(`${SCRIPT_URL}?action=getProjects`).then(r=>r.json()),
      fetch(`${SCRIPT_URL}?action=getWorkers`).then(r=>r.json()),
      fetch(`${SCRIPT_URL}?action=getCards`).then(r=>r.json()),
      fetch(`${SCRIPT_URL}?action=getExpenseItems`).then(r=>r.json()),
      fetch(`${SCRIPT_URL}?action=getEquipments`).then(r=>r.json()),
    ]);
    masterData.projects=proj.data||[];
    masterData.workers=workers.data||[];
    masterData.cards=(cards.data||[]).map(c=>({...c,last4:String(c.last4).padStart(4,'0')}));
    masterData.expenseItems=items.data||[];
    masterData.equipments=equip.data||[];
    buildWriteForm();
  } catch(e){console.error(e);}
  hideLoading();
  loadCalendar();
  loadUnsubmitted();
  loadTodayStatus();
}

function switchTab(tab){
  document.querySelectorAll('.tab').forEach(t=>t.classList.remove('on'));
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('on'));
  document.getElementById('tab-'+tab).classList.add('on');
  document.getElementById('page-'+tab).classList.add('on');
}

function showLoading(msg){document.getElementById('loading-text').textContent=msg||'처리 중...';document.getElementById('loading').classList.add('show');}
function hideLoading(){document.getElementById('loading').classList.remove('show');}

// ========== 달력 ==========
async function loadCalendar(){
  showLoading('달력 불러오는 중...');
  try {
    // 해당 월의 작업일보 데이터 로드
    const monthStr=calYear+'.'+String(calMonth+1).padStart(2,'0');
    const res=await fetch(`${SCRIPT_URL}?action=getMonthRecords&month=${encodeURIComponent(monthStr)}`).then(r=>r.json());
    calData=res.data||{};
  } catch(e){}
  hideLoading();
  renderCalendar();
}

function renderCalendar(){
  const title=calYear+'년 '+(calMonth+1)+'월';
  document.getElementById('cal-title').textContent=title;
  const grid=document.getElementById('cal-grid');
  grid.innerHTML='';
  const firstDay=new Date(calYear,calMonth,1).getDay();
  const lastDate=new Date(calYear,calMonth+1,0).getDate();
  const today=new Date();

  // 이전 달 빈칸
  for(let i=0;i<firstDay;i++){
    const div=document.createElement('div');div.className='cal-day other-month';grid.appendChild(div);
  }

  for(let d=1;d<=lastDate;d++){
    const dateStr=`${calYear}.${String(calMonth+1).padStart(2,'0')}.${String(d).padStart(2,'0')}`;
    const div=document.createElement('div');div.className='cal-day';
    const isToday=today.getFullYear()===calYear&&today.getMonth()===calMonth&&today.getDate()===d;
    if(isToday)div.classList.add('today');

    const dateLabel=document.createElement('div');
    dateLabel.className='cal-date';
    dateLabel.style.color=isToday?'#1D9E75':'#1a1a1a';
    dateLabel.textContent=d;
    div.appendChild(dateLabel);

    const records=calData[dateStr]||[];
    records.forEach(r=>{
      const item=document.createElement('div');
      item.className='cal-item';
      // 상태에 따라 색상 결정
      if(r.expenseConfirmed==='Y'&&r.equipConfirmed==='Y'){item.classList.add('green');}
      else if(r.expenseConfirmed==='Y'||r.equipConfirmed==='Y'){item.classList.add('yellow');}
      else if(r.noExpense==='Y'&&(!r.hasEquip||r.equipConfirmed==='Y')){item.classList.add('gray');}
      else{item.classList.add('red');}
      item.textContent=r.projNum;
      div.appendChild(item);
    });

    if(records.length>0){
      div.onclick=()=>showDayPopup(dateStr,records);
    }
    grid.appendChild(div);
  }
}

function changeMonth(dir){
  calMonth+=dir;
  if(calMonth>11){calMonth=0;calYear++;}
  if(calMonth<0){calMonth=11;calYear--;}
  loadCalendar();
}

async function showDayPopup(dateStr,records){
  document.getElementById('popup-title-text').textContent='📅 '+dateStr;
  document.getElementById('popup-content').innerHTML='<p style="text-align:center;color:#888;padding:20px">불러오는 중...</p>';
  document.getElementById('popup').classList.add('show');

  // 상세 경비/장비 내역 조회
  let expenseMap={}, equipMap={};
  try {
    const res=await fetch(SCRIPT_URL+'?action=getSubmitData&date='+encodeURIComponent(dateStr)+'&projNum='+encodeURIComponent(records[0].projNum)).then(r=>r.json());
    // 여러 현장이면 각각 조회
  } catch(e){}

  let html='';
  for(const r of records){
    const expDone=r.expenseConfirmed==='Y';
    const eqDone=r.equipConfirmed==='Y';
    const hasEquip=r.hasEquip==='Y';

    // 상세 데이터 조회
    let expenses=[], equips=[];
    try {
      const detail=await fetch(SCRIPT_URL+'?action=getSubmitData&date='+encodeURIComponent(dateStr)+'&projNum='+encodeURIComponent(r.projNum)).then(res=>res.json());
      expenses=detail.expenses||[];
      equips=detail.equips||[];
    } catch(e){}

    let expHtml='';
    if(r.noExpense==='Y'){
      expHtml='<div style="font-size:11px;color:#888;padding:4px 0">경비 사용 없음</div>';
    } else if(expenses.length>0){
      let total=0;
      expenses.forEach(e=>{
        total+=Number(e.amount||0);
        const badge=e.isPersonal?'<span style="font-size:10px;background:#FAEEDA;color:#633806;padding:1px 5px;border-radius:4px">개인</span>':'<span style="font-size:10px;background:#E6F1FB;color:#0C447C;padding:1px 5px;border-radius:4px">법인</span>';
        expHtml+='<div style="display:flex;justify-content:space-between;font-size:11px;padding:3px 0;border-bottom:0.5px solid #f0f0f0">'+
          '<span>'+e.item+' '+badge+'</span>'+
          '<span style="font-weight:500">'+Number(e.amount||0).toLocaleString()+'원</span></div>';
      });
      expHtml+='<div style="display:flex;justify-content:space-between;font-size:12px;font-weight:500;color:#1D9E75;padding:4px 0;margin-top:2px">'+
        '<span>합계</span><span>'+total.toLocaleString()+'원</span></div>';
    }

    let eqHtml='';
    if(equips.length>0){
      let total=0;
      equips.forEach(e=>{
        total+=Number(e.supplyAmt||0);
        eqHtml+='<div style="display:flex;justify-content:space-between;font-size:11px;padding:3px 0;border-bottom:0.5px solid #f0f0f0">'+
          '<span>'+e.type+(e.company?' / '+e.company:'')+'</span>'+
          '<span style="font-weight:500">'+Number(e.supplyAmt||0).toLocaleString()+'원</span></div>';
      });
      eqHtml+='<div style="display:flex;justify-content:space-between;font-size:12px;font-weight:500;color:#185FA5;padding:4px 0;margin-top:2px">'+
        '<span>합계(공급가)</span><span>'+total.toLocaleString()+'원</span></div>';
    }

    html+='<div class="record-card">'+
      '<div class="record-title">'+r.projNum+' '+r.projName+'</div>'+
      '<div class="record-row"><span>작업자</span><span>'+r.workers+' ('+r.workerCount+'명)</span></div>'+
      '<div class="record-row"><span>작업시간</span><span>'+r.timeRange+'</span></div>'+
      '<div class="record-row"><span>작성자</span><span>'+r.writer+'</span></div>';

    if(expHtml){
      html+='<div style="margin-top:8px;padding-top:8px;border-top:0.5px dashed #eee">'+
        '<div style="font-size:11px;font-weight:500;color:#888;margin-bottom:4px">💳 경비 내역</div>'+expHtml+'</div>';
    }
    if(eqHtml){
      html+='<div style="margin-top:8px;padding-top:8px;border-top:0.5px dashed #eee">'+
        '<div style="font-size:11px;font-weight:500;color:#888;margin-bottom:4px">🚜 장비/외주 내역</div>'+eqHtml+'</div>';
    }

    html+='<div class="status-btns">'+
      '<button class="status-btn '+(expDone?'expense-done':'expense-ok')+'" onclick="confirmExpense(''+dateStr+'',''+r.projNum+'','+expDone+')">'+
      (expDone?'✅ 경비확인완료':'💳 경비 확인')+'</button>'+
      (hasEquip?'<button class="status-btn '+(eqDone?'equip-done':'equip-ok')+'" onclick="confirmEquip(''+dateStr+'',''+r.projNum+'','+eqDone+')">'+
      (eqDone?'✅ 장비결제완료':'🚜 장비 결제')+'</button>':'')+
      '</div></div>';
  }
  document.getElementById('popup-content').innerHTML=html;
}

async function confirmExpense(date,projNum,isDone){
  if(isDone){if(!confirm('경비 확인을 취소하시겠어요?'))return;}
  showLoading('처리 중...');
  try {
    await fetch(SCRIPT_URL,{method:'POST',body:JSON.stringify({type:'confirmExpense',date,projNum,value:isDone?'N':'Y',confirmTime:new Date().toLocaleString('ko-KR')})});
    hideLoading();closePopupDirect();loadCalendar();
  } catch(e){hideLoading();alert('오류가 발생했습니다.');}
}

async function confirmEquip(date,projNum,isDone){
  if(isDone){if(!confirm('장비 결제 확인을 취소하시겠어요?'))return;}
  showLoading('처리 중...');
  try {
    await fetch(SCRIPT_URL,{method:'POST',body:JSON.stringify({type:'confirmEquip',date,projNum,value:isDone?'N':'Y',confirmTime:new Date().toLocaleString('ko-KR')})});
    hideLoading();closePopupDirect();loadCalendar();
  } catch(e){hideLoading();alert('오류가 발생했습니다.');}
}

function closePopup(e){if(e.target===document.getElementById('popup'))closePopupDirect();}
function closePopupDirect(){document.getElementById('popup').classList.remove('show');}

// ========== 미제출 ==========
async function loadUnsubmitted(){
  showLoading('미제출 현황 불러오는 중...');
  try {
    const res=await fetch(`${SCRIPT_URL}?action=checkUnsubmitted`).then(r=>r.json());
    hideLoading();
    const list=document.getElementById('unsub-list');
    if(!res.data||res.data.length===0){
      list.innerHTML=`<div class="empty">✅ 미제출 현장이 없어요!</div>`;return;
    }
    list.innerHTML='';
    res.data.forEach(r=>{
      const div=document.createElement('div');div.className='unsub-card';
      div.innerHTML=`
        <div class="unsub-info">
          <div class="unsub-title">${r.projName}</div>
          <div class="unsub-sub">${r.date} / ${r.receiver}</div>
        </div>
        <div class="unsub-days">${r.diffDays}일 경과</div>`;
      list.appendChild(div);
    });
  } catch(e){hideLoading();}
}

// ========== 현황 ==========
async function loadTodayStatus(){
  const today=new Date();
  // 날짜 입력 초기값 설정
  document.getElementById('status-date').value=today.toISOString().split('T')[0];
  document.getElementById('status-month').value=today.getFullYear()+'-'+String(today.getMonth()+1).padStart(2,'0');
  await loadDateStatus();
  await loadMonthStatus();
}

async function loadDateStatus(){
  const val=document.getElementById('status-date').value;
  if(!val)return;
  const d=new Date(val+'T00:00:00');
  const dateStr=d.getFullYear()+'.'+String(d.getMonth()+1).padStart(2,'0')+'.'+String(d.getDate()).padStart(2,'0');
  const el=document.getElementById('date-status');
  el.innerHTML='<p style="font-size:12px;color:#888;padding:8px 0">불러오는 중...</p>';
  try {
    const res=await fetch(SCRIPT_URL+'?action=getRecordsByDate&date='+encodeURIComponent(dateStr)).then(r=>r.json());
    if(!res.data||res.data.length===0){
      el.innerHTML='<p style="font-size:13px;color:#888;padding:8px 0">'+dateStr+' 제출된 작업일보가 없어요</p>';return;
    }
    let html='';let total=0;
    res.data.forEach(r=>{
      total+=Number(r.totalAmt||0);
      html+='<div style="display:flex;justify-content:space-between;padding:6px 0;border-bottom:0.5px solid #eee;font-size:12px;cursor:pointer" onclick="switchTab('cal')">'+
        '<span>'+r.projNum+' '+r.projName+'</span>'+
        '<span style="font-weight:500">'+Number(r.totalAmt||0).toLocaleString()+'원</span></div>';
    });
    html+='<div style="display:flex;justify-content:space-between;padding:8px 0;font-size:13px;font-weight:500;color:#1D9E75">'+
      '<span>합계 ('+res.data.length+'개 현장)</span><span>'+total.toLocaleString()+'원</span></div>';
    el.innerHTML=html;
  } catch(e){el.innerHTML='<p style="font-size:12px;color:#888;padding:8px 0">불러오지 못했어요</p>';}
}

async function loadMonthStatus(){
  const val=document.getElementById('status-month').value;
  if(!val)return;
  const parts=val.split('-');
  const monthStr=parts[0]+'.'+parts[1];
  const mel=document.getElementById('month-status');
  mel.innerHTML='<p style="font-size:12px;color:#888;padding:8px 0">불러오는 중...</p>';
  try {
    const mres=await fetch(SCRIPT_URL+'?action=getMonthTotal&month='+encodeURIComponent(monthStr)).then(r=>r.json());
    if(mres.data){
      mel.innerHTML=
        '<div style="display:flex;justify-content:space-between;padding:6px 0;font-size:13px"><span>법인카드</span><span>'+Number(mres.data.corp||0).toLocaleString()+'원</span></div>'+
        '<div style="display:flex;justify-content:space-between;padding:6px 0;font-size:13px"><span>개인카드</span><span>'+Number(mres.data.personal||0).toLocaleString()+'원</span></div>'+
        '<div style="display:flex;justify-content:space-between;padding:6px 0;font-size:13px"><span>장비/외주</span><span>'+Number(mres.data.equip||0).toLocaleString()+'원</span></div>'+
        '<div style="display:flex;justify-content:space-between;padding:8px 0;font-size:14px;font-weight:500;color:#1D9E75;border-top:0.5px solid #eee;margin-top:4px">'+
        '<span>총 합계</span><span>'+Number(mres.data.total||0).toLocaleString()+'원</span></div>';
    }
  } catch(e){mel.innerHTML='<p style="font-size:12px;color:#888;padding:8px 0">불러오지 못했어요</p>';}
}

// ========== 대리 작성 ==========
function buildWriteForm(){
  // 날짜
  document.getElementById('w-date').value=new Date().toISOString().split('T')[0];
  // 프로젝트
  const psel=document.getElementById('w-proj');
  psel.innerHTML='<option value="">— 프로젝트 선택 —</option>';
  masterData.projects.forEach(p=>{
    const opt=document.createElement('option');
    opt.value=`${p.biz}|${p.projNum}|${p.projName}`;
    opt.textContent=`[${p.biz} ${p.projNum}] ${p.projName}`;
    psel.appendChild(opt);
  });
  // 작업자
  const wrap=document.getElementById('w-workers');wrap.innerHTML='';
  masterData.workers.forEach(w=>{
    const div=document.createElement('div');div.className='chip';div.textContent=w.name;
    div.onclick=()=>div.classList.toggle('on');wrap.appendChild(div);
  });
  // 카드
  const cwrap=document.getElementById('w-cards');cwrap.innerHTML='';
  masterData.cards.forEach(c=>{
    const div=document.createElement('div');div.className='card-chip';
    div.textContent=`${c.cardCo}(${c.last4})`;
    div.dataset.cardco=c.cardCo;div.dataset.last4=c.last4;div.dataset.biz=c.biz;div.dataset.personal='false';
    div.onclick=()=>{document.querySelectorAll('#w-cards .card-chip').forEach(x=>x.classList.remove('on'));div.classList.add('on');};
    cwrap.appendChild(div);
  });
  const personal=document.createElement('div');personal.className='card-chip';
  personal.textContent='개인카드';personal.dataset.cardco='개인';personal.dataset.last4='-';personal.dataset.biz='개인';personal.dataset.personal='true';
  personal.onclick=()=>{document.querySelectorAll('#w-cards .card-chip').forEach(x=>x.classList.remove('on'));personal.classList.add('on');};
  cwrap.appendChild(personal);
  // 시간
  makeTimes('w-tstart',5,18,'07:00');makeTimes('w-tend',5,18,'16:00');
  makeTimes('w-otstart',15,24,'18:00');makeTimes('w-otend',15,24,'21:00');
}

function makeTimes(selId,from,to,defVal){
  const sel=document.getElementById(selId);sel.innerHTML='';
  for(let h=from;h<=to;h++)for(let m=0;m<60;m+=30){
    if(h===to&&m>0)break;
    const t=`${String(h).padStart(2,'0')}:${String(m).padStart(2,'0')}`;
    sel.innerHTML+=`<option>${t}</option>`;
  }
  sel.value=defVal;
}

function toggleWriteOT(cb){document.getElementById('w-ot-wrap').style.display=cb.checked?'block':'none';}
function toggleWriteNoExp(cb){document.getElementById('w-exp-body').style.opacity=cb.checked?'0.4':'1';document.getElementById('w-exp-body').style.pointerEvents=cb.checked?'none':'auto';}

function addWriteExp(){
  wExpCount++;const id=wExpCount;
  const itemHtml=masterData.expenseItems.map(i=>`<option>${i}</option>`).join('');
  const div=document.createElement('div');div.className='item-box';div.id='wexp-'+id;
  div.innerHTML=`
    <button class="del-btn" onclick="document.getElementById('wexp-${id}').remove()">×</button>
    <div class="row2" style="margin-top:0">
      <div><div class="lbl" style="margin-top:0">금액</div><input type="number" id="wexp-amt-${id}" placeholder="0" style="text-align:right"></div>
      <div><div class="lbl" style="margin-top:0">항목</div><select id="wexp-item-${id}"><option value="">선택</option>${itemHtml}</select></div>
    </div>`;
  document.getElementById('w-exp-list').appendChild(div);
}

function addWriteEquip(){
  wEqCount++;const id=wEqCount;
  const eqHtml=masterData.equipments.map(e=>`<div class="chip" style="font-size:11px" onclick="selEq(this,'${id}')">${e}</div>`).join('');
  const div=document.createElement('div');div.className='item-box';div.id='weq-'+id;
  div.innerHTML=`
    <button class="del-btn" onclick="document.getElementById('weq-${id}').remove()">×</button>
    <div class="chip-wrap" id="weq-chips-${id}" style="margin-top:0">${eqHtml}</div>
    <div class="row2" style="margin-top:8px">
      <div><div class="lbl" style="margin-top:0">업체명</div><input type="text" id="weq-co-${id}" placeholder="업체명"></div>
      <div><div class="lbl" style="margin-top:0">공급가액</div><input type="number" id="weq-amt-${id}" placeholder="0" style="text-align:right" oninput="calcWeqVat('${id}')"></div>
    </div>
    <div class="vat-box" id="weq-vat-${id}">
      <div class="vat-row"><span>공급가액</span><span id="weq-s-${id}">0원</span></div>
      <div class="vat-row"><span>부가세(10%)</span><span id="weq-t-${id}">0원</span></div>
      <div class="vat-row vat-total"><span>합계</span><span id="weq-tot-${id}">0원</span></div>
    </div>`;
  document.getElementById('w-equip-list').appendChild(div);
}

function selEq(el,id){document.querySelectorAll(`#weq-chips-${id} .chip`).forEach(c=>c.classList.remove('on'));el.classList.add('on');}
function calcWeqVat(id){
  const s=parseInt(document.getElementById('weq-amt-'+id).value)||0;
  const v=Math.round(s*0.1),tot=s+v;
  const box=document.getElementById('weq-vat-'+id);
  if(s>0){box.style.display='block';document.getElementById('weq-s-'+id).textContent=s.toLocaleString()+'원';document.getElementById('weq-t-'+id).textContent=v.toLocaleString()+'원';document.getElementById('weq-tot-'+id).textContent=tot.toLocaleString()+'원';}
  else box.style.display='none';
}

async function submitWrite(){
  const proj=document.getElementById('w-proj').value;
  const writer=document.getElementById('w-writer').value.trim();
  const dateVal=document.getElementById('w-date').value;
  if(!proj){alert('프로젝트를 선택해주세요.');return;}
  if(!writer){alert('작성자를 입력해주세요.');return;}
  if(!dateVal){alert('날짜를 선택해주세요.');return;}

  const d=new Date(dateVal+'T00:00:00');
  const dateStr=`${d.getFullYear()}.${String(d.getMonth()+1).padStart(2,'0')}.${String(d.getDate()).padStart(2,'0')}`;
  const projParts=proj.split('|');
  const selectedWorkers=Array.from(document.querySelectorAll('#w-workers .chip.on')).map(c=>c.textContent);
  const extra=document.getElementById('w-extra').value.trim();
  if(extra)selectedWorkers.push(...extra.split(',').map(s=>s.trim()).filter(Boolean));
  const otChk=document.getElementById('w-ot').checked;
  const noExpense=document.getElementById('w-noexp').checked;
  const cardEl=document.querySelector('#w-cards .card-chip.on');
  const expenses=[];
  document.querySelectorAll('.item-box[id^="wexp-"]').forEach(box=>{
    const id=box.id.replace('wexp-','');
    const amt=parseInt(document.getElementById('wexp-amt-'+id)?.value)||0;
    const item=document.getElementById('wexp-item-'+id)?.value||'';
    if(amt>0&&cardEl)expenses.push({cardCo:cardEl.dataset.cardco,last4:cardEl.dataset.last4,biz:cardEl.dataset.biz,isPersonal:cardEl.dataset.personal==='true',userName:'',item,amount:amt});
  });
  const equips=[];
  document.querySelectorAll('.item-box[id^="weq-"]').forEach(box=>{
    const id=box.id.replace('weq-','');
    const typeEl=box.querySelector('.chip.on');
    const supply=parseInt(document.getElementById('weq-amt-'+id)?.value)||0;
    if(typeEl)equips.push({type:typeEl.textContent,company:document.getElementById('weq-co-'+id)?.value||'',supplyAmt:supply,vatAmt:Math.round(supply*0.1),totalAmt:supply+Math.round(supply*0.1)});
  });

  const payload={type:'expense',date:dateStr,projNum:projParts[1]||'',projName:projParts[2]||'',projBiz:projParts[0]||'',
    workers:selectedWorkers.join(', '),workerCount:selectedWorkers.length,
    timeStart:document.getElementById('w-tstart').value,timeEnd:document.getElementById('w-tend').value,
    overtime:otChk?`${document.getElementById('w-otstart').value}~${document.getElementById('w-otend').value}`:'',
    otWorkers:'',extraNote:'[관리자 대리작성]',
    expenses,equips,noExpense,noInvoice:document.getElementById('w-noinv').checked,
    receiptCount:0,invoiceCount:0,writer,submitTime:new Date().toLocaleString('ko-KR'),seq:1,isRevision:false};

  showLoading('저장 중...');
  try {
    await fetch(SCRIPT_URL,{method:'POST',body:JSON.stringify(payload)});
    hideLoading();
    document.getElementById('write-form').style.display='none';
    document.getElementById('write-complete').classList.add('show');
    document.getElementById('write-complete-desc').textContent=`${projParts[2]} / ${writer}`;
    loadCalendar();loadUnsubmitted();
  } catch(e){hideLoading();alert('오류가 발생했습니다.');}
}

function resetWriteForm(){
  document.getElementById('write-complete').classList.remove('show');
  document.getElementById('write-form').style.display='block';
  document.getElementById('w-proj').value='';
  document.querySelectorAll('#w-workers .chip.on').forEach(c=>c.classList.remove('on'));
  document.querySelectorAll('#w-cards .card-chip.on').forEach(c=>c.classList.remove('on'));
  document.getElementById('w-extra').value='';
  document.getElementById('w-exp-list').innerHTML='';
  document.getElementById('w-equip-list').innerHTML='';
  document.getElementById('w-ot').checked=false;
  document.getElementById('w-ot-wrap').style.display='none';
  document.getElementById('w-noexp').checked=false;
  document.getElementById('w-noinv').checked=false;
  document.getElementById('w-writer').value='';
  wExpCount=0;wEqCount=0;
  makeTimes('w-tstart',5,18,'07:00');makeTimes('w-tend',5,18,'16:00');
  window.scrollTo(0,0);
}
</script>
</body>
</html>
