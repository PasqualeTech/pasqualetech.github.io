"""
pastech Telegram Bot
--------------------
Permette agli utenti di sfogliare le guide tech di pastech
direttamente su Telegram.

Requisiti:
  pip install python-telegram-bot==20.*

Avvio:
  1. Crea un bot su @BotFather -> ottieni il TOKEN
  2. Sostituisci BOT_TOKEN con il tuo token
  3. python pastech_bot.py
"""

import logging
from telegram import Update, InlineKeyboardButton, InlineKeyboardMarkup
from telegram.ext import (
    Application, CommandHandler, CallbackQueryHandler,
    MessageHandler, filters, ContextTypes
)

# ── Config ────────────────────────────────────────────────────────────────────
BOT_TOKEN = "IL_TUO_TOKEN_QUI"   # <-- sostituisci con il token di @BotFather

logging.basicConfig(
    format="%(asctime)s | %(levelname)s | %(message)s",
    level=logging.INFO
)
log = logging.getLogger(__name__)

# ── Database guide ─────────────────────────────────────────────────────────────
# Struttura: { id: { title, category, level, description, url } }
GUIDES = {
    "l1": {
        "title": "Bash scripting completo",
        "category": "linux",
        "level": "intermedio",
        "description": "Variabili, cicli, funzioni, redirect e best practice per scrivere script bash robusti.",
        "url": "https://pastech.github.io/#guide-list"
    },
    "l2": {
        "title": "Firewall con iptables",
        "category": "linux",
        "level": "avanzato",
        "description": "Configurazione completa di iptables: regole INPUT/OUTPUT, NAT, logging e persistenza.",
        "url": "https://pastech.github.io/#guide-list"
    },
    "l3": {
        "title": "Cron job: automazione su Linux",
        "category": "linux",
        "level": "base",
        "description": "Sintassi crontab, variabili d'ambiente, log e debugging dei job schedulati.",
        "url": "https://pastech.github.io/#guide-list"
    },
    "l4": {
        "title": "SSH hardening",
        "category": "linux",
        "level": "intermedio",
        "description": "Disabilitare root login, chiavi pubbliche, Fail2Ban, port knocking e 2FA.",
        "url": "https://pastech.github.io/#guide-list"
    },
    "l5": {
        "title": "File system Linux",
        "category": "linux",
        "level": "base",
        "description": "Gerarchia FHS, mount, permessi, inode, link simbolici e hard link.",
        "url": "https://pastech.github.io/#guide-list"
    },
    "s1": {
        "title": "Intro al penetration testing",
        "category": "security",
        "level": "base",
        "description": "Fasi di un pentest, strumenti base (Nmap, Metasploit), report e aspetti legali.",
        "url": "https://pastech.github.io/#guide-list"
    },
    "s2": {
        "title": "OSINT: raccogliere info legalmente",
        "category": "security",
        "level": "intermedio",
        "description": "Shodan, Maltego, Google Dorks, TheHarvester e tecniche di ricerca passiva.",
        "url": "https://pastech.github.io/#guide-list"
    },
    "s3": {
        "title": "CTF writeup: buffer overflow",
        "category": "security",
        "level": "avanzato",
        "description": "Analisi di un binario vulnerabile, sfruttamento dello stack e shellcode.",
        "url": "https://pastech.github.io/#guide-list"
    },
    "s4": {
        "title": "Nmap in profondità",
        "category": "security",
        "level": "intermedio",
        "description": "Scanning avanzato, NSE scripts, evasione IDS e output XML per reporting.",
        "url": "https://pastech.github.io/#guide-list"
    },
    "a1": {
        "title": "Prompt engineering per dev",
        "category": "ai",
        "level": "base",
        "description": "Tecniche di prompting, chain-of-thought, few-shot e integrazione nelle app.",
        "url": "https://pastech.github.io/#guide-list"
    },
    "a2": {
        "title": "Automazione con Python + AI",
        "category": "ai",
        "level": "intermedio",
        "description": "Pipeline con LLM API, parsing output, gestione errori e logging.",
        "url": "https://pastech.github.io/#guide-list"
    },
    "a3": {
        "title": "LLM locali con Ollama",
        "category": "ai",
        "level": "intermedio",
        "description": "Installazione, modelli disponibili, API REST locale e benchmark.",
        "url": "https://pastech.github.io/#guide-list"
    },
    "c1": {
        "title": "VPN self-hosted con WireGuard",
        "category": "cloud",
        "level": "intermedio",
        "description": "Setup server/client WireGuard, routing, split tunneling e DNS privato.",
        "url": "https://pastech.github.io/#guide-list"
    },
    "c2": {
        "title": "AWS per chi inizia",
        "category": "cloud",
        "level": "base",
        "description": "EC2, S3, IAM, VPC e cost management: i fondamentali senza sprechi.",
        "url": "https://pastech.github.io/#guide-list"
    },
    "d1": {
        "title": "Docker da zero",
        "category": "dev",
        "level": "base",
        "description": "Immagini, container, volumi, network e docker-compose in pratica.",
        "url": "https://pastech.github.io/#guide-list"
    },
    "d2": {
        "title": "Git workflow professionale",
        "category": "dev",
        "level": "intermedio",
        "description": "Branching strategy, rebase vs merge, hook, tag semantici e CI/CD.",
        "url": "https://pastech.github.io/#guide-list"
    },
    "d3": {
        "title": "Python: gestione errori avanzata",
        "category": "dev",
        "level": "avanzato",
        "description": "Eccezioni custom, context manager, logging strutturato e debugging.",
        "url": "https://pastech.github.io/#guide-list"
    },
    "d4": {
        "title": "REST API con FastAPI",
        "category": "dev",
        "level": "intermedio",
        "description": "Setup, routing, validazione Pydantic, auth JWT e deploy con Docker.",
        "url": "https://pastech.github.io/#guide-list"
    },
}

CATEGORIES = {
    "linux":    ("🐧", "Linux & Bash"),
    "security": ("🔐", "Cybersecurity"),
    "ai":       ("🤖", "AI & Automazione"),
    "cloud":    ("☁️",  "Cloud & Networking"),
    "dev":      ("💻", "Programmazione"),
}

LEVELS = {"base": "🟢", "intermedio": "🟡", "avanzato": "🔴"}

SOCIAL_LINKS = {
    "Instagram":  "https://instagram.com/_pastech_",
    "TikTok":     "https://tiktok.com/@_pastech_",
    "YouTube":    "https://youtube.com/@pastech",
    "LinkedIn":   "https://linkedin.com/in/pastech",
    "Sito web":   "https://pastech.github.io",
}

# ── Helpers ────────────────────────────────────────────────────────────────────

def guides_by_cat(cat: str) -> list:
    return [(gid, g) for gid, g in GUIDES.items() if g["category"] == cat]

def main_menu_keyboard() -> InlineKeyboardMarkup:
    buttons = []
    for cat, (icon, label) in CATEGORIES.items():
        buttons.append([InlineKeyboardButton(f"{icon} {label}", callback_data=f"cat:{cat}")])
    buttons.append([InlineKeyboardButton("🔍 Cerca per parola chiave", callback_data="search")])
    buttons.append([InlineKeyboardButton("📡 Canali social", callback_data="social")])
    return InlineKeyboardMarkup(buttons)

def guide_list_keyboard(cat: str) -> InlineKeyboardMarkup:
    guides = guides_by_cat(cat)
    buttons = []
    for gid, g in guides:
        level_icon = LEVELS.get(g["level"], "")
        buttons.append([InlineKeyboardButton(
            f"{level_icon} {g['title']}", callback_data=f"guide:{gid}"
        )])
    buttons.append([InlineKeyboardButton("◀️ Indietro", callback_data="menu")])
    return InlineKeyboardMarkup(buttons)

def guide_detail_keyboard(gid: str, cat: str) -> InlineKeyboardMarkup:
    g = GUIDES[gid]
    return InlineKeyboardMarkup([
        [InlineKeyboardButton("📖 Leggi la guida", url=g["url"])],
        [InlineKeyboardButton("◀️ Torna alla categoria", callback_data=f"cat:{cat}")],
        [InlineKeyboardButton("🏠 Menu principale", callback_data="menu")],
    ])

# ── Handlers ───────────────────────────────────────────────────────────────────

async def start(update: Update, ctx: ContextTypes.DEFAULT_TYPE):
    name = update.effective_user.first_name or "hacker"
    text = (
        f"👾 <b>Benvenuto/a su pastech, {name}!</b>\n\n"
        "Qui trovi tutte le guide tech su:\n"
        "🐧 Linux · 🔐 Security · 🤖 AI · ☁️ Cloud · 💻 Dev\n\n"
        "Scegli una categoria o cerca per parola chiave:"
    )
    await update.message.reply_text(text, parse_mode="HTML", reply_markup=main_menu_keyboard())

async def help_cmd(update: Update, ctx: ContextTypes.DEFAULT_TYPE):
    text = (
        "📚 <b>Come usare il bot</b>\n\n"
        "/start — menu principale\n"
        "/guide — lista tutte le guide\n"
        "/cerca [parola] — cerca nelle guide\n"
        "/social — link ai canali\n"
        "/help — questo messaggio\n\n"
        "Oppure scrivi qualsiasi parola e il bot la cerca nelle guide!"
    )
    await update.message.reply_text(text, parse_mode="HTML")

async def list_all(update: Update, ctx: ContextTypes.DEFAULT_TYPE):
    buttons = []
    for cat, (icon, label) in CATEGORIES.items():
        g_list = guides_by_cat(cat)
        buttons.append([InlineKeyboardButton(
            f"{icon} {label} ({len(g_list)})", callback_data=f"cat:{cat}"
        )])
    buttons.append([InlineKeyboardButton("🏠 Menu principale", callback_data="menu")])
    await update.message.reply_text(
        f"📚 <b>Tutte le guide</b> — {len(GUIDES)} disponibili\nScegli una categoria:",
        parse_mode="HTML",
        reply_markup=InlineKeyboardMarkup(buttons)
    )

async def search_cmd(update: Update, ctx: ContextTypes.DEFAULT_TYPE):
    query = " ".join(ctx.args).lower().strip() if ctx.args else ""
    if not query:
        await update.message.reply_text("✍️ Scrivi: /cerca [parola]\nEsempio: /cerca docker")
        return
    await _do_search(update, query)

async def social_cmd(update: Update, ctx: ContextTypes.DEFAULT_TYPE):
    lines = ["📡 <b>Segui pastech su:</b>\n"]
    for platform, url in SOCIAL_LINKS.items():
        lines.append(f"• <a href='{url}'>{platform}</a>")
    await update.message.reply_text("\n".join(lines), parse_mode="HTML", disable_web_page_preview=True)

async def free_text(update: Update, ctx: ContextTypes.DEFAULT_TYPE):
    query = update.message.text.strip().lower()
    await _do_search(update, query)

async def _do_search(update: Update, query: str):
    results = [
        (gid, g) for gid, g in GUIDES.items()
        if query in g["title"].lower() or query in g["description"].lower() or query in g["category"]
    ]
    if not results:
        await update.message.reply_text(
            f"🔍 Nessuna guida trovata per <b>{query}</b>\n\nProva con parole come: bash, docker, nmap, LLM, aws…",
            parse_mode="HTML",
            reply_markup=InlineKeyboardMarkup([[InlineKeyboardButton("🏠 Menu", callback_data="menu")]])
        )
        return
    buttons = []
    for gid, g in results[:10]:
        icon = LEVELS.get(g["level"], "")
        buttons.append([InlineKeyboardButton(f"{icon} {g['title']}", callback_data=f"guide:{gid}")])
    buttons.append([InlineKeyboardButton("🏠 Menu principale", callback_data="menu")])
    await update.message.reply_text(
        f"🔍 <b>{len(results)}</b> risultati per <b>{query}</b>:",
        parse_mode="HTML",
        reply_markup=InlineKeyboardMarkup(buttons)
    )

# ── Callback query ─────────────────────────────────────────────────────────────

async def button(update: Update, ctx: ContextTypes.DEFAULT_TYPE):
    q = update.callback_query
    await q.answer()
    data = q.data

    if data == "menu":
        await q.edit_message_text(
            "🏠 <b>Menu principale</b>\nScegli una categoria:",
            parse_mode="HTML",
            reply_markup=main_menu_keyboard()
        )

    elif data.startswith("cat:"):
        cat = data.split(":")[1]
        icon, label = CATEGORIES[cat]
        count = len(guides_by_cat(cat))
        await q.edit_message_text(
            f"{icon} <b>{label}</b> — {count} guide disponibili\n\n"
            f"🟢 base  🟡 intermedio  🔴 avanzato",
            parse_mode="HTML",
            reply_markup=guide_list_keyboard(cat)
        )

    elif data.startswith("guide:"):
        gid = data.split(":")[1]
        g = GUIDES.get(gid)
        if not g:
            await q.edit_message_text("❌ Guida non trovata.")
            return
        icon, _ = CATEGORIES[g["category"]]
        level_icon = LEVELS.get(g["level"], "")
        text = (
            f"{icon} <b>{g['title']}</b>\n\n"
            f"📂 Categoria: {g['category'].capitalize()}\n"
            f"{level_icon} Livello: {g['level'].capitalize()}\n\n"
            f"📝 {g['description']}"
        )
        await q.edit_message_text(
            text, parse_mode="HTML",
            reply_markup=guide_detail_keyboard(gid, g["category"])
        )

    elif data == "search":
        await q.edit_message_text(
            "🔍 <b>Ricerca guide</b>\n\nScrivi direttamente nel chat la parola che cerchi.\nEsempio: <code>docker</code>, <code>nmap</code>, <code>bash</code>",
            parse_mode="HTML",
            reply_markup=InlineKeyboardMarkup([[InlineKeyboardButton("◀️ Indietro", callback_data="menu")]])
        )

    elif data == "social":
        lines = ["📡 <b>Canali pastech</b>\n"]
        for platform, url in SOCIAL_LINKS.items():
            lines.append(f"• <a href='{url}'>{platform}</a>")
        await q.edit_message_text(
            "\n".join(lines), parse_mode="HTML", disable_web_page_preview=True,
            reply_markup=InlineKeyboardMarkup([[InlineKeyboardButton("◀️ Indietro", callback_data="menu")]])
        )

# ── Main ───────────────────────────────────────────────────────────────────────

def main():
    app = Application.builder().token(BOT_TOKEN).build()

    app.add_handler(CommandHandler("start", start))
    app.add_handler(CommandHandler("help", help_cmd))
    app.add_handler(CommandHandler("guide", list_all))
    app.add_handler(CommandHandler("cerca", search_cmd))
    app.add_handler(CommandHandler("social", social_cmd))
    app.add_handler(CallbackQueryHandler(button))
    app.add_handler(MessageHandler(filters.TEXT & ~filters.COMMAND, free_text))

    log.info("🤖 pastech bot avviato")
    app.run_polling(allowed_updates=Update.ALL_TYPES)

if __name__ == "__main__":
    main()
