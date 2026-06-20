<div align="center">

# 🌤️ Sky Tasks

### A persistent task execution system — not another to-do list.

Tasks that refuse to be forgotten. Built for people who are tired of sticky notes disappearing under coffee cups.

[![Python](https://img.shields.io/badge/Python-3.12+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![PyQt6](https://img.shields.io/badge/PyQt6-Desktop_UI-41CD52?style=for-the-badge&logo=qt&logoColor=white)](https://riverbankcomputing.com/software/pyqt/)
[![SQLite](https://img.shields.io/badge/SQLite-Local--First-003B57?style=for-the-badge&logo=sqlite&logoColor=white)](https://sqlite.org)
[![Platform](https://img.shields.io/badge/Platform-Linux_|_Windows_|_macOS-555555?style=for-the-badge)](#installation)
[![License](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)](#license)

</div>

---

## 🎯 Why This Exists

Most to-do apps let you swipe a task away and forget about it forever. **Sky Tasks doesn't.**

If you don't finish something, it carries forward to tomorrow. If it sits for 3 days, it gets highlighted. At 7 days, it escalates. At 14 days, you have to *actually acknowledge* it before it'll let you move on.

No cloud sync. No subscriptions. No account. Your tasks live in a SQLite file on your own machine, forever.

---

## ✨ Features

<table>
<tr>
<td width="50%" valign="top">

### 🗂️ Task Management
- Priority levels — Critical, High, Medium, Low
- Status tracking — Pending, In Progress, Completed, Archived
- Categories, tags, due dates, time estimates
- Instant search and multi-filter

### ☀️ Daily Focus Window
- Auto-opens at your chosen time
- Shows overdue, critical & carry-forward tasks
- Stays available until dismissed

### 🌙 Evening Planning
- Prompts you to plan tomorrow intentionally
- Gentle reminders every 30 min if skipped
- "Skip Today" option — no guilt trips

</td>
<td width="50%" valign="top">

### 🔥 Escalating Attention System
| Days Old | Behavior |
|:---:|---|
| 1 | Normal |
| 3 | 🟡 Highlighted |
| 7 | 🟠 Escalated warning |
| 14 | 🔴 Requires acknowledgement |

### 🎨 Fully Personalized
- Dark mode / Light mode toggle
- 8 preset color palettes + custom color picker
- Editable name, themes, and schedule — anytime

### 📊 Weekly Review
- Every Sunday — completed vs. unfinished
- Most-delayed tasks surfaced automatically
- Carry work forward with one click

</td>
</tr>
</table>

---


## 🚀 Quick Start

### Linux (Ubuntu / Debian / Mint / Fedora)

```bash
sudo apt install python3 python3-pip python3-venv   # Ubuntu/Debian
git clone https://github.com/yourusername/sky-tasks.git
cd sky-tasks
bash install.sh
source .venv/bin/activate
python main.py
```

### Windows

```powershell
# Install Python from python.org — check "Add Python to PATH"
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
pip install win10toast
python main.py
```

### macOS

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python main.py
```

On first launch, a setup wizard walks you through your name, theme, color palette, and preferred Focus/Planning times. Everything's editable later in **⚙ Settings**.

---

## 🏗️ Architecture

```
sky_tasks/
│
├── main.py                      # Entry point — theming, setup wizard, app boot
├── export.py                    # Strips personal data → clean shareable zip
├── requirements.txt
│
└── app/
    ├── models/
    │   └── task.py               # Task ORM — Priority, Status, attention logic
    │
    ├── database/
    │   ├── base.py                # SQLAlchemy declarative base
    │   └── manager.py             # Engine, sessions, WAL mode, auto-backup
    │
    ├── services/
    │   ├── task_service.py        # All business logic & queries
    │   ├── scheduler.py           # Configurable Focus/Planning timers
    │   ├── notification.py        # Cross-platform notifications
    │   └── settings.py            # Persisted user preferences (JSON)
    │
    ├── ui/
    │   ├── main_window.py          # App shell — sidebar, tray, navigation
    │   ├── dashboard.py            # Main task overview
    │   ├── tasks_view.py           # Full list with search/filter
    │   ├── stats_view.py           # Productivity statistics
    │   ├── task_editor.py          # Create/edit task dialog
    │   ├── focus_window.py         # ☀️ Daily focus popup
    │   ├── planning_window.py      # 🌙 Evening planning popup
    │   ├── weekly_review.py        # 📊 Sunday review
    │   ├── setup_dialog.py         # First-run wizard
    │   ├── settings_window.py      # Editable preferences panel
    │   ├── themes.py               # Dynamic stylesheet generator
    │   ├── palette_picker.py       # Color swatch picker
    │   ├── widgets.py              # Reusable components
    │   └── styles.py               # Base style constants
    │
    └── utils/
        └── autostart.py            # XDG autostart helper (Linux)
```

**Design principles:** strict separation of concerns — UI never touches the database directly, all logic flows through `TaskService`. The scheduler is just signals; `MainWindow` decides what to do with them.

---

## ⚙️ Settings — Change Anything, Anytime

Click **⚙ Settings** from the sidebar or tray menu to update:

| Setting | Options |
|---|---|
| **Name** | Anything — reflected across the whole app instantly |
| **Theme** | Dark mode / Light mode |
| **Color Palette** | 8 presets (Sky Blue, Rose Pink, Violet, Emerald, Amber, Crimson, Teal, Slate) or pick any custom color |
| **Focus Time** | When your daily review window appears |
| **Planning Time** | When your evening planning window appears |

No restarts required — everything repaints and reschedules live.

---

## 📦 Sharing a Clean Copy

Want to hand this to a friend without leaking your tasks? Run:

```bash
python export.py
```

This generates a zip stripped of your database, settings, and backups — the recipient gets a completely blank slate with their own setup wizard.

---

## 🔐 Privacy & Data

- **100% local** — no internet connection required, ever
- Database: `~/.local/share/sky_tasks/sky_tasks.db`
- Settings: `~/.local/share/sky_tasks/settings.json`
- Backups: auto-saved weekly, last 8 kept, in `~/.local/share/sky_tasks/backups/`
- To fully reset: delete the `~/.local/share/sky_tasks/` folder

---

## ⌨️ Keyboard Shortcuts

| Shortcut | Action |
|:---:|---|
| `Ctrl+1` | Dashboard |
| `Ctrl+2` | All Tasks |
| `Ctrl+3` | Statistics |
| `Ctrl+N` | New Task |

---

## 🗺️ Roadmap

- [ ] Obsidian markdown export
- [ ] Google Calendar sync
- [ ] Local LLM task prioritization (Ollama)
- [ ] Voice command task creation
- [ ] Mobile companion app

---

## 🤝 Built With AI Assistance

This project was developed with Claude (Anthropic) as a pair-programming collaborator — used as a hands-on way to learn PyQt6 architecture, SQLAlchemy ORM patterns, and cross-platform desktop development. Feature decisions, testing, debugging, and personalization were driven by real day-to-day use.

---

## 📄 License

MIT — free to use, modify, and distribute.

---

<div align="center">

**If this helped you stop forgetting things, consider starring the repo ⭐**

</div>
