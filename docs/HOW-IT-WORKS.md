# iTraining HTML Slide: How It Works

> Office knowledge: โครงสร้าง, เทคนิค, และเหตุผลเบื้องหลัง HTML slide ของ iAgencyAIA
> Owner: Prism Oracle (UI/UX) | Ref: CDT-TRAIN-001 | Gold standard: T.1/6 Mindset

## 1. ทำไมเลือก Single-File Inline HTML

**ปัญหาที่แก้:** slide deck ต้องเปิดได้ทุกที่ (browser, LINE, AirDrop, Google Drive preview) โดยไม่ต้องติดตั้งอะไร

**ทำไมไม่ใช้ PowerPoint / Google Slides:**
- ต้องมี app เปิด, font หาย, animation ต่างเครื่องต่างผล
- ไม่ interactive (ไม่มี keyboard nav, ไม่มี responsive)

**ทำไมไม่ใช้ framework (Reveal.js, Slidev):**
- ต้อง build step, CDN dependency, node_modules
- เปิดจาก Google Drive / LINE ไม่ได้

**Single-File HTML ดีตรงไหน:**
- เปิด browser ตรง ไม่ต้องติดตั้ง ไม่ต้อง server
- ส่ง LINE / AirDrop / Google Drive ได้เลย, preview ได้
- CSS + JS inline ทั้งหมด, ไม่มี external dependency
- รูปฝัง base64 (ถ้ามี) อยู่ในไฟล์เดียว
- ไม่เกี่ยวกับ MWE/TinyMCE (slide เปิด browser ตรง ไม่ผ่าน CMS)

## 2. โครงสร้าง HTML

```
<html>
  <head>
    <style> /* CSS ทั้งหมด inline */ </style>
  </head>
  <body>
    <div class="slide active"> ... </div>   <!-- slide 1 (cover) -->
    <div class="slide light"> ... </div>     <!-- slide 2 -->
    <div class="slide "> ... </div>          <!-- slide 3 -->
    ...
    <script> /* keyboard nav */ </script>
  </body>
</html>
```

**แต่ละ slide มี:**
- `<div class="bar">` : progress bar (แถบบนสุด gradient แดง-ทอง)
- Logo block (มุมซ้ายบน): iAgencyAIA + tagline
- Footer (กลางล่าง): © 2026 iAgencyAIA Confidential
- `<div class="sn">N/TOTAL</div>` : ตัวนับสไลด์ (มุมขวาล่าง)
- `<div class="nav">` : ปุ่ม ← → (กลางล่าง)
- เนื้อหาตรงกลาง (z-index 2)

**สไลด์ 2 แบบหลัก:**
- **Dark** (`class="slide "`): พื้นดำ #0d0d10, text ขาว, orb effects
- **Light** (`class="slide light"`): พื้นครีม #FFFDF8, text เข้ม, glass cards

## 3. CSS Design System

### 3.1 Typography

| Element | CSS class | ขนาด | ลักษณะ |
|---------|-----------|------|--------|
| Kicker | `.kicker` | 13-17px | ตัวพิมพ์ใหญ่, letter-spacing 5px, สีจาง |
| Title | `h1.big` | 30-62px | gradient text (ขาว→เทา dark, น้ำตาล→เทา light) |
| Accent | `.accent` | inherit | gradient แดง→ทอง (สำหรับคำเน้น) |
| Subtitle | `.sub` | 15-21px | สีเทา, line-height 1.7 |
| Big quote | `.bq` | 26-54px | bold, line-height 1.45, max-width 900px |

ทุก font ใช้ `clamp()` ให้ responsive อัตโนมัติ

### 3.2 Visual Effects

**Orbs:** วงกลม blur ลอยตัว สร้างบรรยากาศ (`.orb .o-red / .o-gold / .o-blue`)
- `filter: blur(90px)`, `opacity: .45` (dark) / `.16` (light)
- Animation `drift` 14s ขยับเบาๆ

**Glass cards:** `.glass .card`
- Dark: `background: rgba(255,255,255,.055)`, `backdrop-filter: blur(18px)`, `border-radius: 24px`
- Light: `background: rgba(255,255,255,.75)`, `box-shadow` subtle
- Hover: `translateY(-8px)` ลอยขึ้นเมื่อชี้

**Card accent colors:** `.gl-red`, `.gl-gold`, `.gl-blue` เปลี่ยนสี h3

### 3.3 Hero Image (cover slide)

- `object-fit: cover` + `object-position: center N%` สำหรับ crop
- `::after` pseudo-element เป็น scrim gradient overlay
- รูปฝัง base64 (`data:image/jpeg;base64,...`)
- รูปสว่าง: ใช้ multi-layer scrim (top-edge + top-right corner + left-to-right)

### 3.4 Grid Layout

| Class | Columns | ใช้กับ |
|-------|---------|--------|
| `.g2` | 2 คอลัมน์ | card คู่ |
| `.g3` | 3 คอลัมน์ | card 3 ใบ |
| `.g4` | 4 คอลัมน์ | card 4 ใบ |

Mobile (≤820px): ทุก grid เป็น 1 คอลัมน์, slide scroll ได้

## 4. JavaScript Navigation

```javascript
var c=0, s=document.querySelectorAll('.slide'), t=s.length;

function sh(n) {
  // ซ่อนทุก slide, แสดง slide n, อัป progress bar
  s.forEach(x => x.classList.remove('active'));
  s[n].classList.add('active');
  var b = s[n].querySelector('.bar');
  if (b) b.style.width = ((n/(t-1))*100) + '%';
}

function go(d) {
  c = Math.max(0, Math.min(t-1, c+d));
  sh(c);
}
```

**Keyboard:**
- `→` หรือ `Spacebar` : ไปหน้าถัดไป
- `←` : ย้อนกลับ
- `F` : fullscreen

**Touch:** swipe ซ้าย/ขวา (threshold 50px)

**Progress bar:** gradient แดง-ทอง, width ตาม % ของ slide ปัจจุบัน

**Counter:** ตัวนับเป็น hardcoded N/TOTAL ใน HTML แต่ละ slide (ไม่ dynamic, ต้อง update เมื่อเพิ่ม/ลบ slide)

## 5. เทคนิคคำถามฝึกคิด (Q/R/Note Pattern)

**หัวใจของ CDT-TRAIN-001:** สไลด์ต้องโต้ตอบ ไม่ใช่บรรยายนิ่ง

### จังหวะ Q/R/Note

| Step | Kicker | Background | หน้าที่ |
|------|--------|------------|---------|
| Q | คำถามฝึกคิด | light | โยนคำถาม + ตัวเลือก + prompt ให้ตอบ |
| R | เฉลย | dark | เผยแนวคิด, อภิปราย |
| Note | (ต่อเนื่อง) | ตามบริบท | สรุป takeaway |

### Q slide ประกอบด้วย:
1. **คำถาม** (`.bq`): คำถามเปิดหรือเลือก ชวนคิดก่อนเรียน
2. **ตัวเลือก** (`.opts > .opt`): emoji + ข้อความ (ไม่บังคับทุกคำถาม)
3. **Prompt** (`.hint`): 💬 บอกวิธีตอบ เช่น "ยกมือ", "เลือก 1 ข้อ", "เขียนกระดาน"
4. **บรรยากาศ**: "ไม่มีคำตอบผิด" สร้างความปลอดภัยในการตอบ

### สัดส่วน:
- T1 (37 สไลด์) มี 11 คำถาม = ~1 คำถามต่อ 2-3 สไลด์
- Target ทุก deck: ~30% ของสไลด์เป็นคำถาม/เฉลย

## 6. Animation

ทุก slide ใช้ CSS animation เมื่อ `.active`:
- `.a` : `rise` (ลอยขึ้น 30px + fade in, 0.7s)
- `.ai` : `fadeIn` (0.55s)
- `.as` : `scaleIn` (ซูมจาก 88%, 0.55s)
- `.d1` ถึง `.d6` : stagger delay (0.12s ถึง 0.8s)

## 7. Rules ที่ต้องจำ

- **em-dash / en-dash: ห้ามเด็ดขาด** ใช้เครื่องหมายจุลภาค, ทวิภาค, เว้นวรรค แทน
- **ไฟล์เดียว** ไม่มี external CSS/JS/image (ยกเว้น YouTube embed)
- **Kicker** ของ cover: `iTRAINING` (i เล็ก, text-transform:none)
- **Counter** ต้อง update ทุกครั้งที่เพิ่ม/ลบ slide (hardcoded)
- **Navigation** slide แรก: → only, slide สุดท้าย: ← only

## 8. Workflow สร้าง Deck ใหม่

1. Clone `deck-template.html` เปลี่ยนชื่อเป็น `itraining-tN-TOPIC.html`
2. แก้ cover: title `T.N/6 <หัวข้อ>`, subtitle
3. เขียน content text ก่อน (Quill), Dream approve
4. Prism integrate เข้า HTML: สร้าง slide ตาม pattern, แทรก Q/R/Note
5. Update counter N/TOTAL ทุก slide
6. QA: `grep -oP '\x{2014}|\x{2013}' file | wc -l` = 0, keyboard nav ทำงาน, counter ถูก
7. Screenshot cover + ตัวอย่างคำถาม
8. Deliver: inbox → Dream review → Drive sync (3 copies md5 ตรง)
