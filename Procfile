import os
import json
import time
import re
import io
import tempfile
from flask import Flask, render_template, request, jsonify, send_file, session
from werkzeug.utils import secure_filename
import fitz  # PyMuPDF
from docx import Document
from docx.shared import Pt, Inches, Cm, RGBColor
from docx.enum.text import WD_ALIGN_PARAGRAPH
from docx.enum.section import WD_ORIENT
import anthropic
import openai

app = Flask(__name__)
app.secret_key = os.environ.get("SECRET_KEY", "generateur-cours-secret-2024")
app.config["MAX_CONTENT_LENGTH"] = 50 * 1024 * 1024  # 50 MB max

# ---------------------------------------------------------------------------
# Configuration API
# ---------------------------------------------------------------------------
def get_anthropic_client():
    key = os.environ.get("ANTHROPIC_API_KEY", "")
    if not key:
        raise ValueError("Clé API Anthropic non configurée")
    return anthropic.Anthropic(api_key=key)

def get_openai_client():
    key = os.environ.get("OPENAI_API_KEY", "")
    if not key:
        raise ValueError("Clé API OpenAI non configurée")
    return openai.OpenAI(api_key=key)

# ---------------------------------------------------------------------------
# Extraction PDF
# ---------------------------------------------------------------------------
def extract_pdf_text(file_bytes):
    """Extrait le texte d'un PDF uploadé."""
    doc = fitz.open(stream=file_bytes, filetype="pdf")
    text = ""
    for page in doc:
        text += page.get_text() + "\n"
    doc.close()
    return text.strip()

# ---------------------------------------------------------------------------
# Appels IA
# ---------------------------------------------------------------------------
PLAN_SYSTEM = """Tu es un expert en ingénierie pédagogique spécialisé dans les Titres Professionnels français et les exigences Qualiopi.

Tu génères des plans de cours structurés en exactement 11 parties.

RÈGLES:
- Chaque partie a un titre clair et 3-5 sous-sections détaillées
- Progression logique du général vers le spécifique puis la mise en pratique
- Inclure parties théoriques ET pratiques (cas d'entreprise, mises en situation)
- Adapté au référentiel Titre Professionnel fourni
- Partie 1 = Introduction/contexte professionnel
- Parties 2-9 = Développement aligné sur les compétences du référentiel
- Partie 10 = Mise en situation professionnelle / cas pratique
- Partie 11 = Synthèse et préparation à l'évaluation
- Chaque partie doit explicitement cibler des compétences du référentiel

IMPORTANT: Réponds UNIQUEMENT avec un JSON valide, sans markdown, sans backticks:
{"titre_module":"...","parties":[{"numero":1,"titre":"...","sous_sections":["...","..."]}]}"""


def get_section_system(subject, plan, idx, referentiel_text):
    ref_block = ""
    if referentiel_text:
        # Tronquer à 3000 chars pour rester dans les limites raisonnables
        ref_excerpt = referentiel_text[:3000]
        ref_block = f"""
RÉFÉRENTIEL (extrait):
{ref_excerpt}

Tu DOIS aligner le contenu sur les compétences et critères d'évaluation du référentiel ci-dessus.
"""

    return f"""Tu es un rédacteur expert en contenus pédagogiques pour les Titres Professionnels français.
Tu rédiges du contenu EXCLUSIVEMENT optimisé pour la lecture à voix haute (text-to-speech / Eleven Labs).

MODULE: "{subject}"
PLAN COMPLET:
{chr(10).join(f"{p['numero']}. {p['titre']}" for p in plan['parties'])}
{ref_block}
Tu rédiges la PARTIE {idx + 1}: "{plan['parties'][idx]['titre']}"
Sous-sections: {', '.join(plan['parties'][idx]['sous_sections'])}

RÈGLES STRICTES DE RÉDACTION TTS:
- MINIMUM 800 mots, idéalement 900-1100 mots
- Style conversationnel et pédagogique, comme un formateur qui PARLE à ses apprenants
- Utilise "vous" pour s'adresser aux apprenants
- Phrases de longueur VARIÉE: alterner courtes (impact) et longues (explication)
- Transitions naturelles entre sous-sections: "Maintenant que nous avons vu...", "Passons à présent à...", "D'ailleurs, c'est un point essentiel..."
- Connecteurs oraux: "en fait", "concrètement", "d'ailleurs", "vous l'aurez compris", "autrement dit"
- Écrire TOUS les nombres en toutes lettres (vingt-trois, pas 23)
- AUCUNE abréviation: écrire "c'est-à-dire" pas "c.-à-d.", "par exemple" pas "ex."
- Écrire les sigles en entier à la première mention puis entre parenthèses
- AUCUNE liste à puces, AUCUN tableau, AUCUN formatage visuel (pas de gras, pas de souligné)
- AUCUN titre ou sous-titre dans le texte, que des paragraphes fluides
- Respirations naturelles entre les idées (phrases de transition courtes)
- Exemples concrets d'entreprises françaises réelles (Carrefour, Décathlon, SNCF, Leroy Merlin...)
- Mises en situation: "Imaginez que vous êtes...", "Prenons le cas de..."
- Résumés intermédiaires: "Retenez bien que...", "L'essentiel ici c'est que..."
- Commencer par une phrase d'accroche reliant à la partie précédente
- Terminer par une transition douce vers la partie suivante
- NE JAMAIS utiliser de tirets, d'astérisques ou de caractères spéciaux de formatage
- Le texte doit pouvoir être lu à voix haute SANS AUCUNE modification"""


def call_anthropic(system, user_msg, model="claude-sonnet-4-20250514"):
    client = get_anthropic_client()
    response = client.messages.create(
        model=model,
        max_tokens=4000,
        system=system,
        messages=[{"role": "user", "content": user_msg}],
    )
    return response.content[0].text


def call_openai(system, user_msg, model="gpt-4o"):
    client = get_openai_client()
    response = client.chat.completions.create(
        model=model,
        max_tokens=4000,
        messages=[
            {"role": "system", "content": system},
            {"role": "user", "content": user_msg},
        ],
    )
    return response.choices[0].message.content


def call_ai(system, user_msg, provider="anthropic", model=None):
    if provider == "anthropic":
        m = model or "claude-sonnet-4-20250514"
        return call_anthropic(system, user_msg, m)
    else:
        m = model or "gpt-4o"
        return call_openai(system, user_msg, m)


# ---------------------------------------------------------------------------
# Découpage TTS (Eleven Labs compatible)
# ---------------------------------------------------------------------------
def chunk_text_for_tts(text, max_chars=5000):
    """Découpe le texte en blocs de ~5000 caractères aux limites de phrases."""
    sentences = re.split(r'(?<=[.!?])\s+', text)
    chunks = []
    current = ""

    for sentence in sentences:
        if len(current) + len(sentence) + 1 > max_chars and current:
            chunks.append(current.strip())
            current = sentence
        else:
            current = current + " " + sentence if current else sentence

    if current.strip():
        chunks.append(current.strip())

    return chunks


# ---------------------------------------------------------------------------
# Génération Word
# ---------------------------------------------------------------------------
def generate_docx(plan, sections):
    doc = Document()

    # Styles
    style = doc.styles['Normal']
    font = style.font
    font.name = 'Calibri'
    font.size = Pt(12)
    font.color.rgb = RGBColor(0x2D, 0x37, 0x48)
    style.paragraph_format.line_spacing = 1.85
    style.paragraph_format.space_after = Pt(6)

    # Marges
    for section in doc.sections:
        section.top_margin = Cm(2.5)
        section.bottom_margin = Cm(2.5)
        section.left_margin = Cm(2.5)
        section.right_margin = Cm(2.5)

    # Page de garde
    for _ in range(6):
        doc.add_paragraph("")

    title = doc.add_paragraph()
    title.alignment = WD_ALIGN_PARAGRAPH.CENTER
    run = title.add_run(plan['titre_module'])
    run.font.size = Pt(28)
    run.font.color.rgb = RGBColor(0x1A, 0x36, 0x5D)
    run.font.name = 'Georgia'
    run.bold = True

    subtitle = doc.add_paragraph()
    subtitle.alignment = WD_ALIGN_PARAGRAPH.CENTER
    run = subtitle.add_run("Module de formation — Titre Professionnel")
    run.font.size = Pt(14)
    run.font.color.rgb = RGBColor(0x71, 0x80, 0x96)

    doc.add_paragraph("")
    doc.add_paragraph("")

    gen_info = doc.add_paragraph()
    gen_info.alignment = WD_ALIGN_PARAGRAPH.CENTER
    run = gen_info.add_run("Document généré automatiquement — Contenu optimisé TTS")
    run.font.size = Pt(10)
    run.font.color.rgb = RGBColor(0xA0, 0xAE, 0xC0)

    # Sommaire
    doc.add_page_break()
    toc_title = doc.add_paragraph()
    run = toc_title.add_run("Sommaire")
    run.font.size = Pt(22)
    run.font.color.rgb = RGBColor(0x1A, 0x36, 0x5D)
    run.font.name = 'Georgia'
    run.bold = True

    doc.add_paragraph("")

    for p in plan['parties']:
        toc_entry = doc.add_paragraph()
        run_num = toc_entry.add_run(f"Partie {p['numero']}  —  ")
        run_num.font.color.rgb = RGBColor(0x2B, 0x6C, 0xB0)
        run_num.bold = True
        run_title = toc_entry.add_run(p['titre'])
        run_title.font.color.rgb = RGBColor(0x2D, 0x37, 0x48)

    # Contenu
    for s in sections:
        doc.add_page_break()

        heading = doc.add_paragraph()
        run = heading.add_run(f"Partie {s['numero']} — {s['titre']}")
        run.font.size = Pt(18)
        run.font.color.rgb = RGBColor(0x1A, 0x36, 0x5D)
        run.font.name = 'Georgia'
        run.bold = True

        doc.add_paragraph("")

        paragraphs = s['contenu'].split('\n')
        for para_text in paragraphs:
            para_text = para_text.strip()
            if para_text:
                p = doc.add_paragraph()
                p.alignment = WD_ALIGN_PARAGRAPH.JUSTIFY
                run = p.add_run(para_text)
                run.font.size = Pt(12)
                run.font.name = 'Calibri'

    return doc


# ---------------------------------------------------------------------------
# Routes Flask
# ---------------------------------------------------------------------------
@app.route("/")
def index():
    return render_template("index.html")


@app.route("/upload-pdf", methods=["POST"])
def upload_pdf():
    """Upload et extraction de texte des PDFs."""
    files = request.files.getlist("pdfs")
    if not files:
        return jsonify({"error": "Aucun fichier reçu"}), 400

    all_text = []
    file_names = []

    for f in files:
        if f.filename and f.filename.lower().endswith('.pdf'):
            try:
                file_bytes = f.read()
                text = extract_pdf_text(file_bytes)
                if text:
                    all_text.append(f"--- {f.filename} ---\n{text}")
                    file_names.append(f.filename)
            except Exception as e:
                return jsonify({"error": f"Erreur lors de la lecture de {f.filename}: {str(e)}"}), 400

    if not all_text:
        return jsonify({"error": "Aucun texte extrait des PDFs"}), 400

    combined = "\n\n".join(all_text)

    return jsonify({
        "text": combined,
        "files": file_names,
        "chars": len(combined),
    })


@app.route("/generate-plan", methods=["POST"])
def generate_plan():
    """Étape 1: Génère le plan structuré."""
    data = request.json
    subject = data.get("subject", "")
    context = data.get("context", "")
    referentiel = data.get("referentiel", "")
    provider = data.get("provider", "anthropic")

    if not subject:
        return jsonify({"error": "Sujet requis"}), 400

    ref_block = ""
    if referentiel:
        ref_excerpt = referentiel[:4000]
        ref_block = f"\n\nRÉFÉRENTIEL FOURNI (extrait):\n{ref_excerpt}"

    ctx_block = f"\nContexte: {context}" if context else ""

    try:
        # Utilise Haiku pour le plan (optimisation coût)
        if provider == "anthropic":
            model = "claude-haiku-4-5-20241022"
        else:
            model = "gpt-4o-mini"

        raw = call_ai(
            PLAN_SYSTEM,
            f"Génère un plan en 11 parties pour:\n\nSujet: {subject}{ctx_block}{ref_block}",
            provider=provider,
            model=model,
        )

        clean = raw.replace("```json", "").replace("```", "").strip()
        plan = json.loads(clean)

        return jsonify({"plan": plan})

    except json.JSONDecodeError:
        return jsonify({"error": "Le plan n'a pas pu être interprété. Relancez."}), 500
    except Exception as e:
        return jsonify({"error": str(e)}), 500


@app.route("/generate-section", methods=["POST"])
def generate_section():
    """Étape 2: Génère une section individuelle."""
    data = request.json
    subject = data.get("subject", "")
    plan = data.get("plan", {})
    section_index = data.get("section_index", 0)
    referentiel = data.get("referentiel", "")
    provider = data.get("provider", "anthropic")

    if not plan or not subject:
        return jsonify({"error": "Plan et sujet requis"}), 400

    try:
        system = get_section_system(subject, plan, section_index, referentiel)
        partie = plan['parties'][section_index]

        content = call_ai(
            system,
            f"Rédige la partie {section_index + 1}: \"{partie['titre']}\"\nSous-sections: {', '.join(partie['sous_sections'])}",
            provider=provider,
        )

        return jsonify({
            "section": {
                "numero": section_index + 1,
                "titre": partie['titre'],
                "contenu": content,
            }
        })

    except Exception as e:
        return jsonify({"error": str(e)}), 500


@app.route("/download-docx", methods=["POST"])
def download_docx():
    """Génère et télécharge le fichier Word."""
    data = request.json
    plan = data.get("plan", {})
    sections = data.get("sections", [])

    if not plan or not sections:
        return jsonify({"error": "Plan et sections requis"}), 400

    try:
        doc = generate_docx(plan, sections)
        buffer = io.BytesIO()
        doc.save(buffer)
        buffer.seek(0)

        filename = re.sub(r'[^\w\sàâäéèêëïîôùûüÿçœæ]', '', plan.get('titre_module', 'Module'), flags=re.UNICODE)
        filename = filename.strip().replace(' ', '_')[:80] + '.docx'

        return send_file(
            buffer,
            as_attachment=True,
            download_name=filename,
            mimetype='application/vnd.openxmlformats-officedocument.wordprocessingml.document'
        )
    except Exception as e:
        return jsonify({"error": str(e)}), 500


@app.route("/download-tts", methods=["POST"])
def download_tts():
    """Découpe le texte en blocs TTS et renvoie un JSON."""
    data = request.json
    sections = data.get("sections", [])

    if not sections:
        return jsonify({"error": "Sections requises"}), 400

    full_text = "\n\n".join(s['contenu'] for s in sections)
    chunks = chunk_text_for_tts(full_text, max_chars=5000)

    # Créer un fichier texte avec les blocs séparés
    output = ""
    for i, chunk in enumerate(chunks):
        output += f"=== BLOC {i + 1} ({len(chunk)} caractères) ===\n\n"
        output += chunk
        output += "\n\n\n"

    buffer = io.BytesIO(output.encode('utf-8'))
    buffer.seek(0)

    return send_file(
        buffer,
        as_attachment=True,
        download_name="cours_blocs_tts.txt",
        mimetype='text/plain; charset=utf-8'
    )


# ---------------------------------------------------------------------------
# Lancement
# ---------------------------------------------------------------------------
if __name__ == "__main__":
    port = int(os.environ.get("PORT", 5000))
    app.run(host="0.0.0.0", port=port, debug=False)
