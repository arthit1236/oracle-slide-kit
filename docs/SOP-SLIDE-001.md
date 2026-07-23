# SOP-SLIDE-001: Slide QA and Delivery

> **Owner: Lens** เติม content + number ใน `~/.maw/inbox/slide-kit/sop-slide-001.md` แล้ว Forge จะ merge เข้า
> Scaffold: Forge Oracle 2026-07-23, ref: nobi#102

---

## QA Checklist (ใช้ได้ทันที Lens เพิ่ม SOP number + ส่วน sign-off)

ดู QA checklist เต็มใน `docs/PLAYBOOK.md` §5.1 (Phase 4: QA + Deliver)

**QA Gate บังคับก่อน deliver ทุกครั้ง:**

```bash
grep -oP '\x{2014}|\x{2013}' file.html | wc -l  # em-dash = 0 (บังคับ)
grep -c 'class="slide' file.html                 # นับ slides
grep -oP '\d+/\d+' file.html | sort -u           # TOTAL ต้องเท่ากันทุก slide
grep -c 'คำถามฝึกคิด' file.html                  # target ~30% ของ slides
```

**Forbidden patterns:**
- em-dash / en-dash ในทุก surface (ดู no-em-dash-everything rule)
- External CSS/JS/image links (ยกเว้น YouTube embed)
- Counter N/TOTAL ไม่ตรง

**[PLACEHOLDER: Lens เติม]**
- SOP number official
- Sign-off protocol (who approves before delivery)
- Delivery format + naming convention
- Version control rules
