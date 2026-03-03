<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Générateur de Cours IA</title>
    <link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700&family=Playfair+Display:wght@700;800&display=swap" rel="stylesheet">
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }

        body {
            font-family: 'DM Sans', 'Segoe UI', sans-serif;
            background: #f7f8fc;
            color: #2d3748;
            min-height: 100vh;
        }

        /* Header */
        .header {
            background: linear-gradient(135deg, #0f172a 0%, #1e3a5f 60%, #1a365d 100%);
            padding: 40px 24px 36px;
            position: relative;
            overflow: hidden;
        }
        .header::before {
            content: '';
            position: absolute;
            top: 0; left: 0; right: 0; bottom: 0;
            background: radial-gradient(circle at 80% 20%, rgba(59,130,246,0.15) 0%, transparent 50%);
        }
        .header-inner {
            max-width: 780px;
            margin: 0 auto;
            position: relative;
        }
        .header-row {
            display: flex;
            align-items: center;
            gap: 14px;
            margin-bottom: 8px;
        }
        .header-icon {
            width: 44px; height: 44px;
            border-radius: 11px;
            background: linear-gradient(135deg, #3b82f6, #6366f1);
            display: flex; align-items: center; justify-content: center;
            font-size: 22px;
            box-shadow: 0 4px 14px rgba(59,130,246,0.4);
        }
        .header h1 {
            font-family: 'Playfair Display', Georgia, serif;
            font-size: 28px;
            font-weight: 800;
            color: #fff;
            letter-spacing: -0.5px;
        }
        .header p {
            color: #94a3b8;
            font-size: 15px;
            padding-left: 58px;
        }

        /* Main */
        .main {
            max-width: 780px;
            margin: 0 auto;
            padding: 28px 24px 80px;
        }

        /* Cards */
        .card {
            background: #fff;
            border-radius: 14px;
            padding: 28px;
            box-shadow: 0 1px 3px rgba(0,0,0,0.06), 0 4px 16px rgba(0,0,0,0.04);
            border: 1px solid #e8eaf0;
            margin-bottom: 20px;
        }

        /* Labels */
        label, .label {
            display: block;
            font-size: 13px;
            font-weight: 600;
            color: #374151;
            margin-bottom: 8px;
            letter-spacing: 0.3px;
            text-transform: uppercase;
        }
        .label-sub {
            font-weight: 400;
            color: #9ca3af;
            text-transform: none;
        }

        /* Inputs */
        input[type="text"], textarea, select {
            width: 100%;
            padding: 13px 16px;
            border: 1.5px solid #d1d5db;
            border-radius: 10px;
            font-size: 15px;
            font-family: inherit;
            outline: none;
            transition: border-color 0.2s;
            background: #fff;
        }
        input:focus, textarea:focus, select:focus {
            border-color: #3b82f6;
        }
        textarea { resize: none; font-size: 14px; }
        select { cursor: pointer; appearance: auto; }

        .input-group { margin-bottom: 18px; }

        /* PDF Upload Zone */
        .upload-zone {
            border: 2px dashed #d1d5db;
            border-radius: 12px;
            padding: 32px 20px;
            text-align: center;
            cursor: pointer;
            transition: all 0.2s;
            background: #fafbfc;
            margin-bottom: 18px;
        }
        .upload-zone:hover, .upload-zone.dragover {
            border-color: #3b82f6;
            background: #eff6ff;
        }
        .upload-zone .icon { font-size: 36px; margin-bottom: 8px; }
        .upload-zone .text { font-size: 14px; color: #64748b; }
        .upload-zone .hint { font-size: 12px; color: #94a3b8; margin-top: 4px; }
        .upload-zone input[type="file"] { display: none; }

        /* File Tags */
        .file-tags {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
            margin-bottom: 18px;
        }
        .file-tag {
            display: flex;
            align-items: center;
            gap: 8px;
            padding: 8px 14px;
            background: #eff6ff;
            border: 1px solid #bfdbfe;
            border-radius: 8px;
            font-size: 13px;
            color: #1e40af;
        }
        .file-tag .remove {
            cursor: pointer;
            color: #93c5fd;
            font-weight: 700;
            font-size: 16px;
            transition: color 0.15s;
        }
        .file-tag .remove:hover { color: #dc2626; }

        /* Provider Toggle */
        .provider-row {
            display: flex;
            gap: 10px;
            margin-bottom: 18px;
        }
        .provider-btn {
            flex: 1;
            padding: 12px 16px;
            border: 1.5px solid #d1d5db;
            border-radius: 10px;
            background: #fff;
            cursor: pointer;
            font-family: inherit;
            font-size: 14px;
            font-weight: 500;
            color: #64748b;
            transition: all 0.2s;
            text-align: center;
        }
        .provider-btn.active {
            border-color: #3b82f6;
            background: #eff6ff;
            color: #1d4ed8;
            font-weight: 600;
        }

        /* Button */
        .btn-primary {
            width: 100%;
            padding: 14px 24px;
            border-radius: 10px;
            border: none;
            font-size: 15px;
            font-weight: 600;
            cursor: pointer;
            background: linear-gradient(135deg, #2563eb, #4f46e5);
            color: #fff;
            box-shadow: 0 4px 14px rgba(37,99,235,0.35);
            transition: all 0.2s;
            letter-spacing: 0.3px;
            font-family: inherit;
        }
        .btn-primary:hover { transform: translateY(-1px); box-shadow: 0 6px 20px rgba(37,99,235,0.4); }
        .btn-primary:disabled {
            background: #d1d5db;
            box-shadow: none;
            cursor: not-allowed;
            transform: none;
        }

        .btn-success {
            padding: 14px 36px;
            border-radius: 10px;
            border: none;
            background: linear-gradient(135deg, #16a34a, #15803d);
            color: #fff;
            font-size: 15px;
            font-weight: 600;
            cursor: pointer;
            box-shadow: 0 4px 14px rgba(22,163,74,0.35);
            transition: all 0.15s;
            font-family: inherit;
            margin: 6px;
        }
        .btn-success:hover { transform: translateY(-1px); }

        .btn-outline {
            padding: 14px 36px;
            border-radius: 10px;
            border: 1.5px solid #6366f1;
            background: #fff;
            color: #6366f1;
            font-size: 15px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.15s;
            font-family: inherit;
            margin: 6px;
        }
        .btn-outline:hover { background: #eef2ff; }

        /* Progress */
        .progress-bar-bg {
            width: 100%;
            background: #e5e7eb;
            border-radius: 8px;
            height: 8px;
            overflow: hidden;
        }
        .progress-bar-fill {
            height: 100%;
            border-radius: 8px;
            background: linear-gradient(90deg, #3b82f6, #6366f1);
            transition: width 0.6s ease;
        }
        .progress-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 12px;
        }
        .progress-label { font-size: 14px; font-weight: 600; color: #1e293b; }
        .progress-pct {
            font-size: 12px; font-weight: 600; color: #3b82f6;
            background: #eff6ff; padding: 4px 10px; border-radius: 20px;
        }
        .progress-info { margin-top: 10px; font-size: 13px; color: #64748b; }
        .progress-info strong { color: #1e293b; font-weight: 500; }

        .pulse-dot {
            display: inline-block;
            width: 7px; height: 7px;
            border-radius: 50%;
            background: #3b82f6;
            animation: pulse 1.5s ease-in-out infinite;
            margin-right: 8px;
            vertical-align: middle;
        }
        @keyframes pulse { 0%,100% { opacity: 1; } 50% { opacity: 0.3; } }

        /* Plan */
        .plan-title {
            font-family: 'Playfair Display', Georgia, serif;
            font-size: 19px;
            font-weight: 700;
            color: #1a365d;
            margin-bottom: 4px;
        }
        .plan-subtitle { font-size: 13px; color: #94a3b8; margin-bottom: 20px; }
        .plan-item {
            display: flex;
            align-items: center;
            gap: 12px;
            padding: 7px 0;
        }
        .plan-num {
            width: 30px; height: 30px;
            border-radius: 8px;
            display: flex; align-items: center; justify-content: center;
            font-size: 12px; font-weight: 700;
            flex-shrink: 0;
            transition: all 0.3s;
        }
        .plan-num.pending { background: #f1f5f9; color: #94a3b8; }
        .plan-num.active { background: #dbeafe; color: #2563eb; animation: pulse 1.5s ease-in-out infinite; }
        .plan-num.done { background: #dcfce7; color: #16a34a; }
        .plan-text { font-size: 14px; }
        .plan-text.pending { color: #64748b; }
        .plan-text.active { color: #1e293b; font-weight: 500; }
        .plan-text.done { color: #1e293b; font-weight: 500; }

        /* Sections preview */
        .section-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 18px;
        }
        .section-header h3 { font-size: 17px; font-weight: 700; color: #1e293b; }
        .word-badge {
            font-size: 13px; font-weight: 600; color: #6366f1;
            background: #eef2ff; padding: 5px 14px; border-radius: 20px;
        }

        .accordion {
            border: 1px solid #e8eaf0;
            border-radius: 10px;
            margin-bottom: 8px;
            overflow: hidden;
        }
        .accordion-trigger {
            width: 100%;
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 13px 16px;
            background: #fff;
            border: none;
            cursor: pointer;
            text-align: left;
            font-family: inherit;
            transition: background 0.15s;
        }
        .accordion-trigger:hover { background: #f8fafc; }
        .accordion-trigger .num { color: #3b82f6; font-weight: 700; }
        .accordion-trigger .title { font-size: 14px; font-weight: 500; color: #334155; }
        .accordion-trigger .toggle {
            color: #94a3b8; font-size: 20px; font-weight: 300;
            transition: transform 0.2s;
        }
        .accordion-trigger.open .toggle { transform: rotate(45deg); }
        .accordion-body {
            padding: 0 16px 16px;
            font-size: 14px; line-height: 1.75; color: #475569;
            border-top: 1px solid #f1f5f9;
            max-height: 400px; overflow-y: auto;
            display: none;
        }
        .accordion-body.open { display: block; }
        .accordion-body p { margin: 12px 0; }

        /* Complete */
        .complete-card {
            background: linear-gradient(135deg, #f0fdf4 0%, #ecfdf5 100%);
            border: 1.5px solid #86efac;
            border-radius: 14px;
            padding: 36px 28px;
            text-align: center;
        }
        .complete-card .emoji { font-size: 44px; margin-bottom: 10px; }
        .complete-card h3 {
            font-family: 'Playfair Display', Georgia, serif;
            font-size: 20px; font-weight: 700; color: #14532d;
            margin-bottom: 6px;
        }
        .complete-card .stats {
            font-size: 14px; color: #16a34a; margin-bottom: 24px;
        }

        /* Error */
        .error-box {
            background: #fef2f2;
            border: 1px solid #fecaca;
            border-radius: 12px;
            padding: 16px 20px;
            color: #991b1b;
            font-size: 14px;
            margin-bottom: 20px;
        }

        /* Info */
        .info-box {
            margin-top: 12px;
            padding: 20px 24px;
            background: #f8fafc;
            border-radius: 12px;
            border: 1px solid #e8eaf0;
        }
        .info-box p {
            font-size: 13px; color: #64748b; line-height: 1.7;
        }
        .info-box strong { color: #475569; }

        .hidden { display: none; }

        /* Cost indicator */
        .cost-hint {
            font-size: 12px;
            color: #94a3b8;
            margin-top: 8px;
            text-align: center;
        }
    </style>
</head>
<body>

<div class="header">
    <div class="header-inner">
        <div class="header-row">
            <div class="header-icon">📘</div>
            <h1>Générateur de Cours IA</h1>
        </div>
        <p>Automatisation de modules pédagogiques — Titres Professionnels — Qualiopi</p>
    </div>
</div>

<div class="main">

    <!-- INPUT CARD -->
    <div class="card" id="inputCard">

        <!-- PDF Upload -->
        <div class="input-group">
            <label>Référentiels et documents <span class="label-sub">(REAC, RC, notes internes...)</span></label>
            <div class="upload-zone" id="uploadZone" onclick="document.getElementById('pdfInput').click()">
                <div class="icon">📄</div>
                <div class="text">Cliquez ou glissez vos fichiers PDF ici</div>
                <div class="hint">Plusieurs fichiers acceptés — REAC, RC, documents internes</div>
                <input type="file" id="pdfInput" accept=".pdf" multiple>
            </div>
            <div class="file-tags" id="fileTags"></div>
        </div>

        <!-- Subject -->
        <div class="input-group">
            <label>Sujet du module</label>
            <input type="text" id="subject" placeholder="Ex : Gestion des réclamations clients dans le commerce de détail">
        </div>

        <!-- Context -->
        <div class="input-group">
            <label>Contexte <span class="label-sub">(optionnel)</span></label>
            <textarea id="context" rows="2" placeholder="Ex : Niveau BEP/CAP, secteur alimentaire, public adulte en reconversion..."></textarea>
        </div>

        <!-- Provider -->
        <div class="input-group">
            <label>Modèle IA</label>
            <div class="provider-row">
                <button class="provider-btn active" data-provider="anthropic" onclick="selectProvider('anthropic')">
                    🟣 Claude (Anthropic)
                </button>
                <button class="provider-btn" data-provider="openai" onclick="selectProvider('openai')">
                    🟢 GPT-4o (OpenAI)
                </button>
            </div>
            <div class="cost-hint">Plan généré avec le modèle léger (économique), contenu avec le modèle standard</div>
        </div>

        <!-- Generate -->
        <button class="btn-primary" id="generateBtn" onclick="startGeneration()">
            Générer le module complet
        </button>
    </div>

    <!-- ERROR -->
    <div class="error-box hidden" id="errorBox"></div>

    <!-- PROGRESS -->
    <div class="card hidden" id="progressCard">
        <div class="progress-header">
            <span class="progress-label" id="progressLabel">Structuration du plan...</span>
            <span class="progress-pct" id="progressPct">0%</span>
        </div>
        <div class="progress-bar-bg">
            <div class="progress-bar-fill" id="progressFill" style="width: 0%"></div>
        </div>
        <div class="progress-info" id="progressInfo">
            <span class="pulse-dot"></span>
            L'IA structure le plan du module...
        </div>
    </div>

    <!-- PLAN -->
    <div class="card hidden" id="planCard">
        <div class="plan-title" id="planTitle"></div>
        <div class="plan-subtitle" id="planSubtitle"></div>
        <div id="planItems"></div>
    </div>

    <!-- SECTIONS PREVIEW -->
    <div class="card hidden" id="sectionsCard">
        <div class="section-header">
            <h3>Aperçu du contenu</h3>
            <span class="word-badge" id="wordCount">0 mots</span>
        </div>
        <div id="sectionsAccordion"></div>
    </div>

    <!-- COMPLETE -->
    <div class="complete-card hidden" id="completeCard">
        <div class="emoji">✅</div>
        <h3>Module généré avec succès</h3>
        <p class="stats" id="completeStats"></p>
        <button class="btn-success" onclick="downloadDocx()">📥 Télécharger en Word (.docx)</button>
        <button class="btn-outline" onclick="downloadTTS()">🎙️ Télécharger blocs TTS</button>
    </div>

    <!-- INFO (idle) -->
    <div class="info-box" id="infoBox">
        <p>
            <strong>Comment ça marche :</strong> Uploadez vos référentiels PDF → Entrez le sujet →
            L'IA crée un plan en 11 parties aligné sur le référentiel →
            Chaque partie est rédigée en style fluide optimisé TTS (~900 mots) →
            Téléchargez en Word ou en blocs compatibles Eleven Labs.
        </p>
    </div>
</div>

<script>
// ---------------------------------------------------------------------------
// State
// ---------------------------------------------------------------------------
let state = {
    provider: 'anthropic',
    referentielText: '',
    uploadedFiles: [],
    plan: null,
    sections: [],
    generating: false,
};

// ---------------------------------------------------------------------------
// Provider selection
// ---------------------------------------------------------------------------
function selectProvider(p) {
    state.provider = p;
    document.querySelectorAll('.provider-btn').forEach(btn => {
        btn.classList.toggle('active', btn.dataset.provider === p);
    });
}

// ---------------------------------------------------------------------------
// PDF Upload
// ---------------------------------------------------------------------------
const uploadZone = document.getElementById('uploadZone');
const pdfInput = document.getElementById('pdfInput');
const fileTags = document.getElementById('fileTags');

['dragenter', 'dragover'].forEach(evt => {
    uploadZone.addEventListener(evt, e => {
        e.preventDefault();
        uploadZone.classList.add('dragover');
    });
});
['dragleave', 'drop'].forEach(evt => {
    uploadZone.addEventListener(evt, e => {
        e.preventDefault();
        uploadZone.classList.remove('dragover');
    });
});
uploadZone.addEventListener('drop', e => {
    const files = Array.from(e.dataTransfer.files).filter(f => f.name.toLowerCase().endsWith('.pdf'));
    if (files.length) handlePDFUpload(files);
});
pdfInput.addEventListener('change', () => {
    const files = Array.from(pdfInput.files);
    if (files.length) handlePDFUpload(files);
    pdfInput.value = '';
});

async function handlePDFUpload(files) {
    const formData = new FormData();
    files.forEach(f => formData.append('pdfs', f));

    uploadZone.querySelector('.text').textContent = 'Extraction en cours...';

    try {
        const res = await fetch('/upload-pdf', { method: 'POST', body: formData });
        const data = await res.json();

        if (data.error) {
            showError(data.error);
            return;
        }

        state.referentielText = data.text;
        state.uploadedFiles = data.files;
        renderFileTags();
        uploadZone.querySelector('.text').textContent = 'Cliquez ou glissez pour ajouter d\'autres fichiers';

    } catch (err) {
        showError('Erreur lors de l\'upload: ' + err.message);
        uploadZone.querySelector('.text').textContent = 'Cliquez ou glissez vos fichiers PDF ici';
    }
}

function renderFileTags() {
    fileTags.innerHTML = state.uploadedFiles.map((f, i) => `
        <div class="file-tag">
            📄 ${f}
            <span class="remove" onclick="removeFile(${i})">×</span>
        </div>
    `).join('');
}

function removeFile(i) {
    state.uploadedFiles.splice(i, 1);
    if (state.uploadedFiles.length === 0) state.referentielText = '';
    renderFileTags();
}

// ---------------------------------------------------------------------------
// Generation
// ---------------------------------------------------------------------------
async function startGeneration() {
    const subject = document.getElementById('subject').value.trim();
    if (!subject || state.generating) return;

    state.generating = true;
    state.plan = null;
    state.sections = [];

    hideError();
    show('progressCard');
    hide('planCard');
    hide('sectionsCard');
    hide('completeCard');
    hide('infoBox');
    document.getElementById('generateBtn').disabled = true;
    document.getElementById('generateBtn').textContent = '⏳ Génération en cours...';

    updateProgress('Création du plan en cours...', 5, 'L\'IA structure le plan du module...');

    try {
        // Step 1: Plan
        const planRes = await fetch('/generate-plan', {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({
                subject,
                context: document.getElementById('context').value.trim(),
                referentiel: state.referentielText,
                provider: state.provider,
            }),
        });
        const planData = await planRes.json();
        if (planData.error) throw new Error(planData.error);

        state.plan = planData.plan;
        renderPlan();
        show('planCard');

        // Step 2: Sections
        const total = state.plan.parties.length;

        for (let i = 0; i < total; i++) {
            const pct = Math.round(((i + 1) / total) * 100);
            updateProgress(
                `Rédaction : partie ${i + 1}/${total}`,
                pct,
                `En cours : <strong>${state.plan.parties[i].titre}</strong>`
            );
            updatePlanStatus(i, 'active');

            const secRes = await fetch('/generate-section', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({
                    subject,
                    plan: state.plan,
                    section_index: i,
                    referentiel: state.referentielText,
                    provider: state.provider,
                }),
            });
            const secData = await secRes.json();
            if (secData.error) throw new Error(secData.error);

            state.sections.push(secData.section);
            updatePlanStatus(i, 'done');
            renderSections();
            show('sectionsCard');
        }

        // Done
        hide('progressCard');
        renderComplete();
        show('completeCard');

    } catch (err) {
        showError(err.message);
    } finally {
        state.generating = false;
        document.getElementById('generateBtn').disabled = false;
        document.getElementById('generateBtn').textContent = 'Générer le module complet';
    }
}

// ---------------------------------------------------------------------------
// UI Helpers
// ---------------------------------------------------------------------------
function show(id) { document.getElementById(id).classList.remove('hidden'); }
function hide(id) { document.getElementById(id).classList.add('hidden'); }

function showError(msg) {
    const box = document.getElementById('errorBox');
    box.innerHTML = `<strong>Erreur :</strong> ${msg}`;
    box.classList.remove('hidden');
}
function hideError() { document.getElementById('errorBox').classList.add('hidden'); }

function updateProgress(label, pct, info) {
    document.getElementById('progressLabel').textContent = label;
    document.getElementById('progressPct').textContent = pct + '%';
    document.getElementById('progressFill').style.width = pct + '%';
    document.getElementById('progressInfo').innerHTML = `<span class="pulse-dot"></span>${info}`;
}

function renderPlan() {
    if (!state.plan) return;
    document.getElementById('planTitle').textContent = state.plan.titre_module;
    document.getElementById('planSubtitle').textContent = `Plan structuré en ${state.plan.parties.length} parties`;

    document.getElementById('planItems').innerHTML = state.plan.parties.map((p, i) => `
        <div class="plan-item" id="planItem${i}">
            <div class="plan-num pending" id="planNum${i}">${p.numero}</div>
            <span class="plan-text pending" id="planText${i}">${p.titre}</span>
        </div>
    `).join('');
}

function updatePlanStatus(i, status) {
    const num = document.getElementById(`planNum${i}`);
    const text = document.getElementById(`planText${i}`);
    if (!num || !text) return;

    num.className = `plan-num ${status}`;
    text.className = `plan-text ${status}`;
    if (status === 'done') num.textContent = '✓';
}

function renderSections() {
    const totalWords = state.sections.reduce((a, s) => a + s.contenu.split(/\s+/).length, 0);
    document.getElementById('wordCount').textContent = `~${totalWords.toLocaleString('fr-FR')} mots`;

    document.getElementById('sectionsAccordion').innerHTML = state.sections.map((s, i) => `
        <div class="accordion">
            <button class="accordion-trigger" onclick="toggleAccordion(${i})">
                <span class="title"><span class="num">${s.numero}.</span> ${s.titre}</span>
                <span class="toggle" id="toggle${i}">+</span>
            </button>
            <div class="accordion-body" id="accBody${i}">
                ${s.contenu.split('\n').filter(p => p.trim()).map(p => `<p>${p}</p>`).join('')}
            </div>
        </div>
    `).join('');
}

function toggleAccordion(i) {
    const body = document.getElementById(`accBody${i}`);
    const trigger = body.previousElementSibling;
    const isOpen = body.classList.contains('open');
    body.classList.toggle('open');
    trigger.classList.toggle('open');
}

function renderComplete() {
    const totalWords = state.sections.reduce((a, s) => a + s.contenu.split(/\s+/).length, 0);
    const pages = Math.round(totalWords / 250);
    document.getElementById('completeStats').textContent =
        `${state.sections.length} parties — ~${totalWords.toLocaleString('fr-FR')} mots — ~${pages} pages`;
}

// ---------------------------------------------------------------------------
// Downloads
// ---------------------------------------------------------------------------
async function downloadDocx() {
    try {
        const res = await fetch('/download-docx', {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({ plan: state.plan, sections: state.sections }),
        });
        if (!res.ok) throw new Error('Erreur lors du téléchargement');
        const blob = await res.blob();
        const url = URL.createObjectURL(blob);
        const a = document.createElement('a');
        a.href = url;
        a.download = (state.plan?.titre_module || 'module') + '.docx';
        document.body.appendChild(a);
        a.click();
        document.body.removeChild(a);
        URL.revokeObjectURL(url);
    } catch (err) {
        showError(err.message);
    }
}

async function downloadTTS() {
    try {
        const res = await fetch('/download-tts', {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({ sections: state.sections }),
        });
        if (!res.ok) throw new Error('Erreur lors du téléchargement');
        const blob = await res.blob();
        const url = URL.createObjectURL(blob);
        const a = document.createElement('a');
        a.href = url;
        a.download = 'cours_blocs_tts.txt';
        document.body.appendChild(a);
        a.click();
        document.body.removeChild(a);
        URL.revokeObjectURL(url);
    } catch (err) {
        showError(err.message);
    }
}
</script>

</body>
</html>
