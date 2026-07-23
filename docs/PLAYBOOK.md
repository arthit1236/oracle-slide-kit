# PLAYBOOK: สร้าง iTraining HTML Slide Deck
> Step-by-step ทำซ้ำได้ ตั้งแต่ outline จนถึง deck เสร็จ
> Quill Oracle | nobi#102 quill#60 | 2026-07-23
> เป้าหมาย: oracle อื่นอ่านแล้วทำ deck เองได้ ไม่ต้องถาม Nobi

---

## สารบัญ

1. [ภาพรวม workflow](#1-ภาพรวม-workflow)
2. [Phase 1: Content Text-First](#2-phase-1-content-text-first)
3. [Phase 2: Dream Review](#3-phase-2-dream-review)
4. [Phase 3: Build HTML](#4-phase-3-build-html)
5. [Phase 4: QA + Deliver](#5-phase-4-qa--deliver)
6. [Prompt / Tooling ที่ใช้จริง](#6-prompt--tooling-ที่ใช้จริง)
7. [เวลาโดยประมาณ](#7-เวลาโดยประมาณ)
8. [กฎทอง 7 ข้อ](#8-กฎทอง-7-ข้อ)
9. [อ้างอิง](#9-อ้างอิง)

---

## 1. ภาพรวม workflow

```
outline → content text → Dream review → build HTML → QA → deliver
   (1)        (2)            (3)            (4)       (5)    (6)
```

**หลักการหลัก: content text-first, HTML last**

ห้าม build HTML ก่อน content นิ่ง (CAR-4: เสีย rebuild ซ้ำหลายรอบ). ส่งเนื้อหาเป็นข้อความ/markdown ให้ Dream approve structure + content ก่อน แล้วค่อย build HTML รอบเดียว.

**แบ่งหน้าที่:**
- **Content oracle** (Quill หรือ oracle อื่น): เขียน content text + ตัวอย่าง + script คำพูด
- **Slide oracle** (Prism): integrate content เข้า HTML template, จัด layout + animation
- **Dream**: approve structure + content + final deck
- **Nobi**: coordinate, QA

oracle เดียวทำได้ทั้ง content + HTML ถ้ามีความรู้ทั้ง 2 ด้าน

---

## 2. Phase 1: Content Text-First

### 2.1 รับ brief / outline

**Input ที่ต้องมี:**
- หัวข้อหลัก (เช่น T.2/6 เทคนิคการขายประกันชีวิต)
- Outline / agenda (กี่ section, หัวข้อแต่ละ section)
- Gold standard deck สำหรับอ้างอิง format (T.1/6 Mindset)
- CDT-TRAIN-001 conduct (ถ้ามี)

**ขั้นตอน:**
1. อ่าน outline/agenda ทั้งหมด นับจำนวน section
2. อ่าน gold standard deck เพื่อดู format, จำนวนคำถามฝึกคิด, สัดส่วน Q/R/Note
3. สร้างโครงร่างว่าแต่ละ section จะมีอะไรบ้าง

### 2.2 เขียน content

**Output format: markdown อ่านง่าย** ไม่ใช่ HTML

**โครงสร้างต่อ section:**
```markdown
### Section N: [ชื่อหัวข้อ]

*คำถามฝึกคิดนำ:*
> "[คำถาม]?"
> ตัวเลือก: A / B / C
> เฉลย: "[แนวคิดหลัก]"

**[หัวข้อย่อย 1]**
[เนื้อหา 2-3 ประโยค]

**[หัวข้อย่อย 2]**
[เนื้อหา 2-3 ประโยค]
```

**กฎการเขียน content:**
- em-dash / en-dash: ห้ามเด็ดขาด ใช้จุลภาค, ทวิภาค, เว้นวรรค แทน
- ข้อมูลประกัน/กฎหมายที่ไม่ชัวร์ mark `[รอยืนยัน]` ไว้ให้ Dream confirm
- ภาษาไทยพูดง่าย ไม่ใช้ศัพท์เทคนิคที่ผู้เรียนไม่คุ้น
- ตัวอย่างสถานการณ์จริง + ผลของปัญหา ทำให้เห็นภาพ
- script คำพูดตัวอย่าง ใช้ลงท้าย ครับ/ค่ะ

**สัดส่วน interactive:**
- Target: ~30% ของสไลด์เป็นคำถาม/เฉลย (1 คำถามต่อ 2-3 สไลด์ content)
- T.1/6 มี 11 คำถามใน 37 สไลด์ = 1:3.4 เป็น benchmark

### 2.3 Deliver content

- Save ลง `~/.maw/inbox/` เป็น `.md`
- CC Nobi + Tempo ว่าเสร็จ พร้อม absolute path
- รอ Dream review

---

## 3. Phase 2: Dream Review

**ทำอะไร:** Dream อ่าน content text ที่ระดับข้อความ

**Oracle ทำ:**
1. รอ feedback จาก Dream (อาจผ่าน Nobi)
2. Dream feedback = additive (เพิ่มเข้าไปในโครง) ไม่ใช่ replace (รื้อโครง) (CAR-2)
3. เช็คจำนวน section ก่อน/หลังทุกครั้งว่าครบ (outline เดิม = โครงตายตัว)
4. แก้ตาม feedback แล้วส่ง content อัปเดตกลับ
5. วน review จนกว่า Dream approve

**เวลาที่ใช้:** ขึ้นกับ Dream (ปกติ 1-3 วัน)

---

## 4. Phase 3: Build HTML

### 4.1 เตรียมไฟล์

1. Clone template: `cp ~/.maw/inbox/slide-kit/deck-template.html ~/.maw/inbox/itraining-tN-TOPIC-draft.html`
2. เปลี่ยน `<title>` เป็นชื่อ deck
3. เปลี่ยน cover slide: title, subtitle

### 4.2 สร้าง slides

**Slide types ที่มีใน template** (อ้างอิง deck-template.html):

| Type | Background | ใช้ทำอะไร | Class |
|------|-----------|-----------|-------|
| Cover | dark | หน้าปก, iTRAINING kicker | `slide active` |
| Section Header | dark | เปิด part ใหม่, orb effects | `slide` |
| Q (คำถามฝึกคิด) | light | คำถาม + ตัวเลือก + prompt | `slide light` |
| R (เฉลย) | dark | เผยคำตอบ + อธิบาย | `slide` |
| Content Cards | light | grid cards (g2/g3/g4) | `slide light` |
| Content Bullets | dark | list ใน glass card | `slide` |
| Closing | dark | ปิดท้าย + mantra | `slide` |

**ทุก slide ต้องมี:**
```html
<div class="bar"></div>                    <!-- progress bar -->
<!-- logo block มุมซ้ายบน -->
<!-- footer © กลางล่าง -->
<div class="sn">N/TOTAL</div>             <!-- counter มุมขวาล่าง -->
<div class="nav">                          <!-- ปุ่ม nav กลางล่าง -->
  <button onclick="go(-1)">&larr;</button>
  <button onclick="go(1)">&rarr;</button>
</div>
```

**กฎ nav พิเศษ:**
- Slide แรก: มีแค่ปุ่ม →
- Slide สุดท้าย: มีแค่ปุ่ม ←

### 4.3 จังหวะ Q/R/Note

สำหรับทุก section ที่มีคำถามฝึกคิด:

```
[Section Header (dark)]
  ↓
[Q slide (light)] คำถาม + ตัวเลือก + prompt
  ↓
[R slide (dark)] เฉลย + อธิบาย
  ↓
[Content slide(s)] เนื้อหาหลักของ section
```

**Q slide structure:**
```html
<div class="kicker ai">คำถามฝึกคิด</div>
<h1 class="bq a d1">[คำถาม]?</h1>
<div class="opts a d3">
  <div class="opt">&#128522; [ตัวเลือก A]</div>
  <div class="opt">&#128517; [ตัวเลือก B]</div>
</div>
<p class="hint ai d5">&#128172; [prompt เช่น ยกมือเลือก 1 ข้อ]</p>
```

**R slide structure:**
```html
<div class="kicker ai">เฉลย</div>
<h1 class="bq a d1">[คำตอบหลัก]</h1>
<p class="sub a d2">[อธิบายสั้น]</p>
```

### 4.4 Animation classes

ใส่ class เหล่านี้เพื่อให้ element ขึ้นทีละจังหวะ:

| Class | Effect | ใช้กับ |
|-------|--------|--------|
| `.a` | ลอยขึ้น + fade in | text หลัก |
| `.ai` | fade in | kicker, hint |
| `.as` | zoom in | cards |
| `.d1` ถึง `.d6` | stagger delay | ลำดับ element (d1 ก่อน, d6 หลังสุด) |

**ตัวอย่าง:** card 3 ใบ ขึ้นทีละใบ
```html
<div class="glass card gl-red as d2">...</div>
<div class="glass card gl-gold as d3">...</div>
<div class="glass card gl-blue as d4">...</div>
```

### 4.5 Hero image (cover)

ถ้ามีรูป cover:
```html
<div class="hero"><img src="data:image/jpeg;base64,[BASE64]" alt="..."></div>
```
- แปลงรูปเป็น base64 (ไม่ใช้ URL ภายนอก)
- ใส่ scrim overlay ใน CSS (::after)

### 4.6 Update counter

**ทุกครั้งที่เพิ่ม/ลบ slide ต้อง update:**
- `<div class="sn">N/TOTAL</div>` ทุก slide
- Counter ไม่ dynamic ต้อง update manually

**ใช้ search-replace:**
1. นับจำนวน slide ทั้งหมด: `grep -c 'class="slide' file.html`
2. Update TOTAL ทุก slide
3. Update N ตามลำดับ

---

## 5. Phase 4: QA + Deliver

### 5.1 QA Checklist (บังคับก่อน deliver)

```bash
# 1. em-dash = 0 (บังคับ) ใช้ unicode hex pattern
grep -oP '\x{2014}|\x{2013}' file.html | wc -l
# ต้องได้ 0

# 2. นับ slides
grep -c 'class="slide' file.html

# 3. เช็ค counter ตรง
grep -oP '\d+/\d+' file.html | sort -u
# TOTAL ต้องเท่ากันทุก slide

# 4. เช็ค keyboard nav ทำงาน
# เปิดไฟล์ใน browser, กด →, ←, Spacebar, F

# 5. เช็คจำนวน section ตรงกับ outline
grep -c 'Part [0-9]' file.html

# 6. เช็คจำนวนคำถามฝึกคิด
grep -c 'คำถามฝึกคิด' file.html
# target: ~30% ของ slides

# 7. Mobile responsive
# ย่อ browser ≤820px ดูว่า cards เป็น 1 คอลัมน์, scroll ได้
```

### 5.2 Screenshot

- Screenshot cover slide (หน้าปก)
- Screenshot 1-2 สไลด์ตัวอย่าง (คำถามฝึกคิด + content card)

### 5.3 Deliver

1. Save final ไว้ที่ `~/.maw/inbox/itraining-tN-TOPIC-draft.html`
2. CC Nobi + Tempo ว่าเสร็จ, แนบ path
3. Dream review final deck
4. Dream approve แล้ว sync ขึ้น Google Drive (3 copies, md5 ตรง)

---

## 6. Prompt / Tooling ที่ใช้จริง

### 6.1 Content phase (Quill)

**เครื่องมือ:**
- Read: อ่าน outline/spec/gold standard deck
- Write: เขียน content markdown
- maw hey: CC Nobi/Tempo

**Prompt pattern (เมื่อมี spec):**
```
อ่าน spec ที่ [path]. เขียน content text ตาม spec ลง ~/.maw/inbox/[name].md
กฎ: em-dash 0, ข้อมูลไม่ชัวร์ mark [รอยืนยัน], ภาษาไทยพูดง่าย
สัดส่วน: 1 คำถามฝึกคิดต่อ 2-3 สไลด์ content
```

### 6.2 HTML phase (Prism)

**เครื่องมือ:**
- Read: อ่าน template + content ที่ approve แล้ว
- Edit: แก้ไข HTML slide
- Bash: QA checks (grep em-dash, count slides)

**Prompt pattern:**
```
อ่าน content ที่ [path] + template ที่ ~/.maw/inbox/slide-kit/deck-template.html
สร้าง HTML slides ตาม HOW-IT-WORKS.md pattern
ทุก section ต้องมี Q/R/Note, animation class, counter ถูก
QA: grep em-dash = 0, counter ตรง, keyboard nav ทำงาน
```

### 6.3 QA gate

```bash
# รัน 3 คำสั่งนี้ก่อน deliver ทุกครั้ง (ใช้ hex pattern ไม่ใช้ literal characters)
grep -oP '\x{2014}|\x{2013}' file.html | wc -l  # must = 0
grep -c 'class="slide' file.html                 # count slides
grep -oP '\d+/\d+' file.html | sort -u           # all same TOTAL
```

---

## 7. เวลาโดยประมาณ

| Phase | เวลา | หมายเหตุ |
|-------|------|----------|
| Phase 1: Content text | 1-2 ชม. | ขึ้นกับจำนวน section + ความซับซ้อนของเนื้อหา |
| Phase 2: Dream review | 1-3 วัน | ขึ้นกับ Dream, อาจวนแก้ 1-2 รอบ |
| Phase 3: Build HTML | 2-4 ชม. | ~10 นาทีต่อ slide (30-50 slides = 3-4 ชม.) |
| Phase 4: QA + deliver | 30 นาที | automated checks + manual browser test |
| **รวม (ฝั่ง oracle)** | **~4-6 ชม. hands-on** | ไม่รวม wait time ของ Dream review |

**Benchmark จริง:**
- T.1/6 Mindset: 37 slides, ~5 ชม. hands-on
- T.2/6 Sales Technique: 41 slides (v2), ~6 ชม. hands-on (มี rebuild จาก CAR-4)

---

## 8. กฎทอง 7 ข้อ

> จาก CAR/PAR จริงตอนทำ T.1/6 + T.2/6

1. **Content text-first, HTML last** ส่งเนื้อหาเป็นข้อความให้ approve ก่อน แล้วค่อย build HTML รอบเดียว (CAR-4)

2. **Outline เดิม = โครงตายตัว** feedback = additive เข้าไปในโครง ไม่ใช่รื้อโครง เช็คจำนวน section ก่อน/หลังทุกครั้ง (CAR-2)

3. **คำถามฝึกคิดบังคับ** ทุก deck ต้องมี Q/R/Note pattern, target 1 คำถามต่อ 2-3 สไลด์ ห้ามเป็นสไลด์บรรยายนิ่ง (CAR-1)

4. **em-dash = 0 ก่อน deliver** ใช้ `grep -oP '\x{2014}|\x{2013}' file | wc -l` เป็น QA gate บังคับ ทั้ง content text และ HTML (CAR-3)

5. **Counter update ทุกครั้ง** ที่เพิ่ม/ลบ slide ตรวจ N/TOTAL ทุก slide ให้ถูก (hardcoded ไม่ dynamic)

6. **ไฟล์เดียว ไม่มี external dependency** CSS + JS inline, รูปเป็น base64, ไม่มี CDN ไม่มี framework (ยกเว้น YouTube embed)

7. **CC ทุก action** ticket ก่อนเริ่ม, CC Nobi + Tempo ทุกจุดสำคัญ (รับงาน, เสร็จ content, เสร็จ HTML, deliver) + absolute path

---

## 9. อ้างอิง

| Document | ที่อยู่ | เนื้อหา |
|----------|--------|---------|
| HOW-IT-WORKS.md | `docs/HOW-IT-WORKS.md` | โครงสร้าง HTML, CSS design system, JS nav, Q/R/Note pattern |
| deck-template.html | `template/deck-template.html` | Template เต็ม, 7 slide types พร้อมใช้ |
| CAR-PAR | `docs/CAR-PAR-slide-production.md` | บทเรียนจริงจาก T.1/6 + T.2/6 |
| CDT-TRAIN-001 | conduct (ถ้ามี) | มาตรฐาน interactive training deck |
| Gold standard | T.1/6 Mindset deck | ตัวอย่างที่ดีที่สุดสำหรับอ้างอิง |

---

> oracle อ่าน playbook นี้ + HOW-IT-WORKS + template = ทำ deck ได้เอง
> ติดปัญหาถาม Prism (HTML/CSS) หรือ Quill (content/writing)
