# notes-uknow-by-taha
This website is bassically use for the student welfair or thier needs
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>NoteSetu — share notes with your batch</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Kalam:wght@400;700&family=Inter:wght@400;500;600&family=JetBrains+Mono:wght@500&display=swap" rel="stylesheet">
<style>
  :root{
    --paper:#FBF8F1;
    --ink:#232019;
    --rule-blue:#35618F;
    --rule-blue-dark:#20415E;
    --margin-red:#B84A3E;
    --highlight:#F0BE3D;
    --card:#FFFFFF;
    --muted:#82796A;
    --line:#E6E0CE;
  }
  *{box-sizing:border-box;}
  body{
    margin:0;
    background:var(--paper);
    color:var(--ink);
    font-family:'Inter',sans-serif;
    background-image:
      repeating-linear-gradient(to bottom, transparent, transparent 34px, var(--line) 35px);
    background-position: 0 90px;
  }
  .binder{
    position:fixed;
    top:0; left:0; bottom:0;
    width:46px;
    background:var(--rule-blue-dark);
    z-index:5;
    display:flex;
    flex-direction:column;
    align-items:center;
    padding-top:60px;
    gap:26px;
  }
  .binder span{
    width:16px;height:16px;border-radius:50%;
    background:var(--paper);
    box-shadow: inset 0 0 0 3px var(--rule-blue-dark);
    flex-shrink:0;
  }
  .page{
    margin-left:46px;
    position:relative;
    max-width:880px;
    margin-right:auto;
    padding:0 40px 80px 56px;
  }
  .page::before{
    content:"";
    position:absolute;
    top:0; bottom:0; left:34px;
    width:2px;
    background:var(--margin-red);
    opacity:.55;
  }
  header.hero{
    padding:70px 0 40px;
  }
  .eyebrow{
    font-family:'JetBrains Mono',monospace;
    font-size:12px;
    letter-spacing:.06em;
    color:var(--rule-blue-dark);
    background:rgba(53,97,143,.1);
    display:inline-block;
    padding:4px 10px;
    border-radius:4px;
    margin-bottom:18px;
  }
  h1.headline{
    font-family:'Kalam',cursive;
    font-weight:700;
    font-size:52px;
    line-height:1.12;
    margin:0 0 18px;
  }
  h1.headline .hl{
    background:linear-gradient(transparent 60%, var(--highlight) 60%);
  }
  .sub{
    font-size:17px;
    color:var(--muted);
    max-width:520px;
    line-height:1.6;
    margin:0 0 28px;
  }
  .cta-row{display:flex; gap:12px; flex-wrap:wrap;}
  button, .btn{
    font-family:'Inter',sans-serif;
    font-weight:600;
    font-size:14px;
    border:none;
    border-radius:6px;
    padding:12px 20px;
    cursor:pointer;
    transition:transform .12s ease;
  }
  button:active, .btn:active{transform:scale(.97);}
  .btn-primary{background:var(--rule-blue-dark); color:var(--paper);}
  .btn-primary:hover{background:var(--rule-blue);}
  .btn-ghost{background:transparent; color:var(--rule-blue-dark); border:1.5px solid var(--rule-blue-dark);}

  section{padding:48px 0; border-top:1px dashed var(--line);}
  h2.section-title{
    font-family:'Kalam',cursive;
    font-size:28px;
    margin:0 0 6px;
  }
  .section-hint{color:var(--muted); font-size:14px; margin:0 0 26px;}

  form.note-form{
    background:var(--card);
    border:1px solid var(--line);
    border-radius:10px;
    padding:26px;
    display:grid;
    grid-template-columns:1fr 1fr;
    gap:16px;
  }
  form.note-form .full{grid-column:1/-1;}
  label{
    display:block;
    font-size:12px;
    font-weight:600;
    color:var(--muted);
    margin-bottom:6px;
    text-transform:uppercase;
    letter-spacing:.03em;
  }
  input, textarea{
    width:100%;
    font-family:'Inter',sans-serif;
    font-size:14px;
    padding:10px 12px;
    border:1px solid var(--line);
    border-radius:6px;
    background:var(--paper);
    color:var(--ink);
  }
  input:focus, textarea:focus{
    outline:2px solid var(--rule-blue);
    outline-offset:1px;
  }
  textarea{resize:vertical; min-height:70px;}
  .form-footer{
    grid-column:1/-1;
    display:flex;
    justify-content:space-between;
    align-items:center;
    margin-top:4px;
  }
  .form-note{font-size:12px; color:var(--muted);}

  .controls{
    display:flex;
    gap:10px;
    flex-wrap:wrap;
    margin-bottom:24px;
  }
  .controls input[type="text"]{flex:1; min-width:200px;}
  select{
    font-family:'Inter',sans-serif;
    font-size:14px;
    padding:10px 12px;
    border:1px solid var(--line);
    border-radius:6px;
    background:var(--paper);
    color:var(--ink);
  }

  .notes-grid{
    display:grid;
    grid-template-columns:repeat(auto-fill, minmax(250px, 1fr));
    gap:18px;
  }
  .note-card{
    background:var(--card);
    border:1px solid var(--line);
    border-radius:8px;
    padding:18px 18px 16px;
    position:relative;
    box-shadow:0 1px 0 var(--line);
  }
  .note-card::before{
    content:"";
    position:absolute;
    top:-8px; left:20px;
    width:44px; height:16px;
    background:rgba(240,190,61,.55);
    transform:rotate(-3deg);
    border-radius:2px;
  }
  .tag-row{display:flex; gap:6px; margin-bottom:10px; flex-wrap:wrap;}
  .tag{
    font-family:'JetBrains Mono',monospace;
    font-size:11px;
    padding:3px 8px;
    border-radius:4px;
  }
  .tag.subject{background:rgba(53,97,143,.12); color:var(--rule-blue-dark);}
  .tag.batch{background:rgba(184,74,62,.12); color:var(--margin-red);}
  .note-title{font-size:16px; font-weight:600; margin:0 0 8px;}
  .note-desc{font-size:13.5px; color:var(--muted); line-height:1.5; margin:0 0 14px; white-space:pre-wrap;}
  .note-meta{
    display:flex;
    justify-content:space-between;
    align-items:center;
    font-size:12px;
    color:var(--muted);
    border-top:1px solid var(--line);
    padding-top:10px;
  }
  .note-link{
    font-size:12.5px;
    font-weight:600;
    color:var(--rule-blue-dark);
    text-decoration:none;
  }
  .note-link:hover{text-decoration:underline;}

  .empty-state{
    text-align:center;
    padding:50px 20px;
    color:var(--muted);
    border:1px dashed var(--line);
    border-radius:8px;
  }

  .toast{
    position:fixed;
    bottom:24px; left:50%;
    transform:translateX(-50%) translateY(20px);
    background:var(--rule-blue-dark);
    color:var(--paper);
    padding:10px 18px;
    border-radius:6px;
    font-size:13px;
    opacity:0;
    pointer-events:none;
    transition:opacity .2s ease, transform .2s ease;
    z-index:20;
  }
  .toast.show{opacity:1; transform:translateX(-50%) translateY(0);}

  footer{
    padding:36px 0 10px;
    font-size:12px;
    color:var(--muted);
    text-align:center;
  }

  @media (max-width:600px){
    .binder{width:26px;}
    .page{margin-left:26px; padding:0 18px 60px 34px;}
    .page::before{left:16px;}
    h1.headline{font-size:36px;}
    form.note-form{grid-template-columns:1fr;}
  }
</style>
</head>
<body>

<div class="binder" aria-hidden="true" id="binder"></div>

<div class="page">
  <header class="hero">
    <span class="eyebrow">notes, shared, on time</span>
    <h1 class="headline">Never scramble<br>for <span class="hl">someone else's</span><br>notes again.</h1>
    <p class="sub">Post the notes you already have. Find what a batchmate already uploaded. One page for your whole batch to stop re-writing the same class notes five times over.</p>
    <div class="cta-row">
      <button class="btn-primary" onclick="document.getElementById('share').scrollIntoView({behavior:'smooth'})">Share a note</button>
      <button class="btn-ghost" onclick="document.getElementById('browse').scrollIntoView({behavior:'smooth'})">Browse notes</button>
    </div>
  </header>

  <section id="share">
    <h2 class="section-title">Share a note</h2>
    <p class="section-hint">Add a link to your notes (Google Drive, a PDF, anything with view access) so classmates can open them straight away.</p>
    <form class="note-form" id="noteForm">
      <div>
        <label for="f-title">Note title</label>
        <input id="f-title" type="text" placeholder="Unit 3 — Thermodynamics" required>
      </div>
      <div>
        <label for="f-subject">Subject</label>
        <input id="f-subject" type="text" placeholder="Physics" required>
      </div>
      <div>
        <label for="f-batch">Batch / semester</label>
        <input id="f-batch" type="text" placeholder="2026 · Sem 3" required>
      </div>
      <div>
        <label for="f-name">Your name</label>
        <input id="f-name" type="text" placeholder="Ananya" required>
      </div>
      <div class="full">
        <label for="f-desc">What's in it</label>
        <textarea id="f-desc" placeholder="Handwritten notes covering the full syllabus + solved numericals from last year's paper"></textarea>
      </div>
      <div class="full">
        <label for="f-link">Link to notes (optional)</label>
        <input id="f-link" type="url" placeholder="https://drive.google.com/...">
      </div>
      <div class="form-footer">
        <span class="form-note">Visible to anyone who opens this page.</span>
        <button type="submit" class="btn-primary">Pin this note</button>
      </div>
    </form>
  </section>

  <section id="browse">
    <h2 class="section-title">Browse notes</h2>
    <p class="section-hint">Search by subject, title, or filter by batch.</p>
    <div class="controls">
      <input type="text" id="searchInput" placeholder="Search notes...">
      <select id="batchFilter"><option value="">All batches</option></select>
      <select id="subjectFilter"><option value="">All subjects</option></select>
    </div>
    <div class="notes-grid" id="notesGrid"></div>
    <div class="empty-state" id="emptyState" hidden>
      <p>No notes match yet. Be the first to pin one for this batch.</p>
    </div>
  </section>

  <footer>Built for batchmates. Notes posted here are visible to everyone who opens this page.</footer>
</div>

<div class="toast" id="toast">Note pinned</div>

<script>
  const binder = document.getElementById('binder');
  for (let i = 0; i < 18; i++) {
    const dot = document.createElement('span');
    binder.appendChild(dot);
  }

  const STORAGE_KEY = 'notesetu-notes';
  let notes = [];

  function seedNotes(){
    return [
      {id:'seed1', title:'Unit 2 — Data Structures (Trees & Graphs)', subject:'DSA', batch:'2026 · Sem 3', desc:'Clean handwritten notes with diagrams for BST, AVL, and graph traversal. Exam-ready.', link:'', sharedBy:'Rohit', ts: Date.now() - 86400000*2},
      {id:'seed2', title:'Thermodynamics — full unit summary', subject:'Physics', batch:'2026 · Sem 3', desc:'Typed summary + solved numericals from the last two years papers.', link:'', sharedBy:'Meera', ts: Date.now() - 86400000*6},
    ];
  }

  async function loadNotes(){
    try{
      const res = await window.storage.get(STORAGE_KEY, true);
      notes = res ? JSON.parse(res.value) : seedNotes();
      if(!res){ await saveNotes(); }
    }catch(e){
      notes = seedNotes();
      try{ await saveNotes(); }catch(e2){}
    }
    populateFilters();
    render();
  }

  async function saveNotes(){
    try{
      await window.storage.set(STORAGE_KEY, JSON.stringify(notes), true);
    }catch(e){
      console.error('Could not save notes', e);
    }
  }

  function timeAgo(ts){
    const diff = Date.now() - ts;
    const days = Math.floor(diff / 86400000);
    if(days <= 0) return 'today';
    if(days === 1) return '1 day ago';
    if(days < 30) return days + ' days ago';
    const months = Math.floor(days/30);
    return months + (months===1?' month ago':' months ago');
  }

  function populateFilters(){
    const batchSel = document.getElementById('batchFilter');
    const subjSel = document.getElementById('subjectFilter');
    const curBatch = batchSel.value, curSubj = subjSel.value;
    const batches = [...new Set(notes.map(n=>n.batch))].sort();
    const subjects = [...new Set(notes.map(n=>n.subject))].sort();
    batchSel.innerHTML = '<option value="">All batches</option>' + batches.map(b=>`<option value="${escapeHtml(b)}">${escapeHtml(b)}</option>`).join('');
    subjSel.innerHTML = '<option value="">All subjects</option>' + subjects.map(s=>`<option value="${escapeHtml(s)}">${escapeHtml(s)}</option>`).join('');
    batchSel.value = curBatch; subjSel.value = curSubj;
  }

  function escapeHtml(str){
    const d = document.createElement('div');
    d.textContent = str;
    return d.innerHTML;
  }

  function render(){
    const q = document.getElementById('searchInput').value.trim().toLowerCase();
    const batchF = document.getElementById('batchFilter').value;
    const subjF = document.getElementById('subjectFilter').value;

    const filtered = notes.filter(n=>{
      if(batchF && n.batch !== batchF) return false;
      if(subjF && n.subject !== subjF) return false;
      if(q){
        const hay = (n.title+' '+n.subject+' '+n.desc+' '+n.sharedBy).toLowerCase();
        if(!hay.includes(q)) return false;
      }
      return true;
    }).sort((a,b)=>b.ts-a.ts);

    const grid = document.getElementById('notesGrid');
    const empty = document.getElementById('emptyState');
    if(filtered.length === 0){
      grid.innerHTML = '';
      empty.hidden = false;
      return;
    }
    empty.hidden = true;
    grid.innerHTML = filtered.map(n=>`
      <div class="note-card">
        <div class="tag-row">
          <span class="tag subject">${escapeHtml(n.subject)}</span>
          <span class="tag batch">${escapeHtml(n.batch)}</span>
        </div>
        <p class="note-title">${escapeHtml(n.title)}</p>
        ${n.desc ? `<p class="note-desc">${escapeHtml(n.desc)}</p>` : ''}
        <div class="note-meta">
          <span>${escapeHtml(n.sharedBy)} · ${timeAgo(n.ts)}</span>
          ${n.link ? `<a class="note-link" href="${escapeHtml(n.link)}" target="_blank" rel="noopener">Open notes →</a>` : ''}
        </div>
      </div>
    `).join('');
  }

  function showToast(msg){
    const t = document.getElementById('toast');
    t.textContent = msg;
    t.classList.add('show');
    setTimeout(()=>t.classList.remove('show'), 1800);
  }

  document.getElementById('noteForm').addEventListener('submit', async (e)=>{
    e.preventDefault();
    const title = document.getElementById('f-title').value.trim();
    const subject = document.getElementById('f-subject').value.trim();
    const batch = document.getElementById('f-batch').value.trim();
    const name = document.getElementById('f-name').value.trim();
    const desc = document.getElementById('f-desc').value.trim();
    const link = document.getElementById('f-link').value.trim();
    if(!title || !subject || !batch || !name) return;

    const note = {
      id: 'n' + Date.now(),
      title, subject, batch, desc, link,
      sharedBy: name,
      ts: Date.now()
    };
    notes.unshift(note);
    await saveNotes();
    populateFilters();
    render();
    e.target.reset();
    showToast('Note pinned for your batch');
    document.getElementById('browse').scrollIntoView({behavior:'smooth'});
  });

  document.getElementById('searchInput').addEventListener('input', render);
  document.getElementById('batchFilter').addEventListener('change', render);
  document.getElementById('subjectFilter').addEventListener('change', render);

  loadNotes();
</script>

</body>
</html>
