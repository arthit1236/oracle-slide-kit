# CAR/PAR: HTML Slide Deck Production (จากการทำ iTraining T1/T2 จริง)

> บทเรียนจริงตอนสร้าง deck + prevention. อ้างอิงใน oracle-slide-kit + CDT-TRAIN-001 + SOP-SLIDE-001.
> เขียนโดย Nobi 2026-07-23 (nobi#102) จากประสบการณ์ T.1/6 + T.2/6.

## CAR-1: สไลด์ออกมานิ่ง ขาดความโต้ตอบ
- **อะไรพลาด:** T.2/6 draft รอบแรกออกมาเป็นสไลด์บรรยายนิ่ง 23 แผ่น 0 คำถามฝึกคิด ทั้งที่จุดแข็งของ T.1/6 คือคำถามฝึกคิด 11 จุดที่ทำให้ผู้เรียนมีส่วนร่วม
- **root cause:** ตอน spec ไม่ได้ระบุ "interactive + คำถามฝึกคิด" เป็น requirement บังคับ ผู้สร้างเลยทำเป็น deck สอนทางเดียว
- **prevention (PAR):** CDT-TRAIN-001 §2 บังคับ q/r/note pattern + template มีสไลด์คำถามฝึกคิดมาให้ default + QA checklist เช็ค "มีคำถามฝึกคิด target 1 ต่อ 2-3 สไลด์"

## CAR-2: ยุบโครงสร้าง หัวข้อหล่นหาย
- **อะไรพลาด:** ตอนเอา feedback ของ Dream (Part 1/2/3) มาใส่ ผมนึกว่าเป็นโครงใหม่ เลยยุบ agenda เดิม 7 part เหลือ 5 part ทำ 3 หัวข้อหาย (เคล็ดไม่ลับ, ขยายตลาด, เทคนิคเฉพาะ)
- **root cause:** ตีความ feedback แบบ "เพิ่มเติม" ว่าเป็น "แทนที่โครงสร้าง"
- **prevention (PAR):** ยึด outline/agenda เดิมเป็นโครงตายตัว (fixed skeleton) feedback = additive เข้าไปในโครง ไม่ใช่รื้อโครง. เช็คจำนวน section ก่อน/หลังทุกครั้งว่าครบ

## CAR-3: em-dash หลุดในงานตัวเอง
- **อะไรพลาด:** เขียน content draft มี em-dash 12 จุด ทั้งที่เพิ่งบันทึกกฎ "ห้าม em-dash ทุก surface" ไปไม่กี่นาที
- **root cause:** ไม่มี gate เช็คก่อน deliver
- **prevention (PAR):** `grep -oP '\x{2014}|\x{2013}' file | wc -l` = 0 เป็น QA gate บังคับก่อน deliver ทุก deck/doc (อยู่ใน CDT-TRAIN-001 §4 + no_em_dash_everything)

## CAR-4 (near-miss/process): ทำ HTML ก่อน content นิ่ง = ช้า
- **อะไรเกือบพลาด:** build HTML deck เต็ม (41 สไลด์ interactive) ก่อน Dream approve content ทำให้ต้อง rebuild หลายรอบ (static→interactive, 5part→7part) เสีย HTML build ซ้ำๆ
- **root cause:** เอา effort ไปทำ presentation layer ก่อน content นิ่ง
- **prevention (PAR):** **content text-first** ส่งเนื้อหาเป็นข้อความให้ approve ก่อน แล้วค่อย build HTML รอบเดียว (content_text_first_then_html rule). HTML = ขั้นสุดท้ายหลัง content ผ่าน

## สรุปกฎทองการทำ deck (สำหรับ oracle อื่น)
1. ยึด outline เดิมเป็นโครงตายตัว feedback เพิ่มเข้าไป ไม่รื้อ
2. content เป็นข้อความก่อน review ผ่านแล้วค่อย HTML
3. ต้องมีคำถามฝึกคิดแทรก (interactive) ไม่ใช่บรรยายนิ่ง
4. grep em-dash = 0 ก่อน deliver
5. verify จำนวน section + counter + keyboard nav ก่อนส่ง
