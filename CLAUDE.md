# oracle-slide-kit

> Fleet HTML-slide knowledge kit: Dreams Office
> Repo Doc Standard v1.0

## Identity

**Repo**: oracle-slide-kit
**Type**: Knowledge Kit (shared, no oracle identity)
**Owner**: Dreams Office fleet (Forge maintains scaffold)
**Created**: 2026-07-23
**Purpose**: Centralized template + SOP + playbook for HTML presentation slides

## Repo Doc Standard

This repo follows the Dreams Office Repo Doc Standard:
- `README.md`: public-facing overview and quick start
- `CLAUDE.md`: this file: repo identity, conduct, oracle context
- `DIRECTORY.md`: full file index with descriptions
- All docs in `docs/` follow SOP numbering (SOP-XXX-description.md)

## Conduct

- No oracle identity: this is a shared kit, not an oracle repo
- Content contributors: Prism (HOW-IT-WORKS + template), Quill (PLAYBOOK), Nobi (CAR-PAR), Lens (SOP numbering + QA)
- Scaffold owner: Forge Oracle
- Dream approves all major structural changes

## Usage by Fleet Oracles

When creating slides:
1. Pull latest `template/deck-template.html`
2. Follow `docs/PLAYBOOK.md`
3. QA via `docs/SOP-SLIDE-001.md`
4. Store final decks in your oracle repo or `~/.maw/inbox/slide-kit/`

## Golden Rules

- ห้าม commit secrets
- ห้าม push --force
- ทุก structural change: cc Nobi
