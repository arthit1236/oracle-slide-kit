# SOP-SLIDE-001: Slide QA and Delivery

> **Owner: Lens** เติม content + number ใน `~/.maw/inbox/slide-kit/sop-slide-001.md` แล้ว Forge จะ merge เข้า
> Scaffold: Forge Oracle 2026-07-23, ref: nobi#102

---

## QA Checklist (ใช้ได้ทันที Lens เพิ่ม SOP number + ส่วน sign-off)

ดู QA checklist เต็มใน `docs/PLAYBOOK.md` §5.1 (Phase 4: QA + Deliver)

**QA Gate บังคับก่อน deliver ทุกครั้ง:**

```bash
# 1. em-dash = 0: ต้องเช็คทั้ง literal UTF-8 AND HTML entities
grep -cP '\xe2\x80\x93|\xe2\x80\x94' file.html          # literal em/en-dash
grep -ciE '&#8212;|&#8211;|&mdash;|&ndash;' file.html    # HTML entity forms
# ทั้ง 2 บรรทัดต้องได้ 0 (literal grep อย่างเดียวไม่พอ)

# 2-4. Structural checks
grep -c 'class="slide' file.html                 # นับ slides
grep -oP '\d+/\d+' file.html | sort -u           # TOTAL ต้องเท่ากันทุก slide
grep -c 'คำถามฝึกคิด' file.html                  # target ~30% ของ slides
```

**Forbidden patterns:**
- em-dash / en-dash ในทุก surface: ทั้ง literal character AND HTML entities (&#8212; &#8211; &mdash; &ndash;)
- External CSS/JS/image links (ยกเว้น YouTube embed)
- Counter N/TOTAL ไม่ตรง

**[PLACEHOLDER: Lens เติม]**
- SOP number official
- Sign-off protocol (who approves before delivery)
- Delivery format + naming convention
- Version control rules
