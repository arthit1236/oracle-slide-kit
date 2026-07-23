# oracle-slide-kit

> Fleet HTML-slide knowledge kit — Dreams Office

## Overview

Shared knowledge base and template system for creating HTML presentation slides across the Dreams Oracle fleet.

## How to Use This Kit

1. **Read the playbook** — `docs/PLAYBOOK.md` — ขั้นตอนการสร้าง slide จาก brief ถึง deliver
2. **Understand the system** — `docs/HOW-IT-WORKS.md` — architecture, tech stack, render flow
3. **Copy the template** — `template/deck-template.html` — starting point สำหรับทุก deck
4. **See examples** — `examples/` — T1 (simple) และ T2 (advanced) reference decks
5. **Follow the SOP** — `docs/SOP-SLIDE-001.md` — QA checklist ก่อน deliver

## Quick Start

```bash
cp template/deck-template.html my-deck.html
# แก้ไข placeholder ตาม brief
# ผ่าน QA checklist ใน SOP-SLIDE-001
# deliver ตาม PLAYBOOK
```

## Repo Structure

```
oracle-slide-kit/
├── README.md              # This file
├── CLAUDE.md              # Repo identity + conduct
├── DIRECTORY.md           # Full file index
├── docs/
│   ├── HOW-IT-WORKS.md    # System architecture (Prism)
│   ├── PLAYBOOK.md        # Creation workflow (Quill)
│   └── SOP-SLIDE-001.md   # QA + delivery SOP (Lens)
├── template/
│   └── deck-template.html # Master slide template (Prism)
└── examples/
    ├── T1-simple/         # Type 1 reference deck
    └── T2-advanced/       # Type 2 reference deck
```

## Owners

| File | Owner |
|------|-------|
| `docs/HOW-IT-WORKS.md` | Prism |
| `docs/PLAYBOOK.md` | Quill |
| `docs/SOP-SLIDE-001.md` | Lens |
| `template/deck-template.html` | Prism |
| Scaffold + maintenance | Forge |
