# Week 04 — Conflict and Negotiation Record

## 1. Negotiation method

แต่ละประเด็นแยก **Position** (สิ่งที่แต่ละฝ่ายเรียกร้อง) ออกจาก **Interest** (เหตุผล/ผลลัพธ์ที่ต้องการ) ตรวจ authority/constraint แล้วเปรียบเทียบ options ด้วยเกณฑ์ร่วม ได้แก่ usability, operational effort, fairness, traceability, privacy และ feasibility

---

## 2. Negotiation register

### N-01 / C-01 — Advance Notice vs Instant Cancellation (เงื่อนไขเวลาในการยกเลิกหรือเลื่อนนัดหมาย)

| Field | Record |
|---|---|
| Evidence | E-03, E-04 |
| Position A — Student | ต้องการยกเลิกหรือขอเลื่อนนัดหมายได้ตลอดเวลาตามความสะดวก |
| Interest A | ความยืดหยุ่นในการปรับเปลี่ยนแผนการเดินทางหรือภารกิจส่วนตัว |
| Position B — Advisor | ต้องการให้แจ้งยกเลิกหรือขอเลื่อนนัดล่วงหน้าอย่างน้อย 24 ชั่วโมง |
| Interest B | การจัดสรรเวลาปฏิบัติงานที่แน่นอน ป้องกันการเสียเวลา และเปิดโอกาสให้นักศึกษาคนอื่นแทรกคิว |
| Authority/constraint | อาจารย์มีสิทธิ์ในการบริหารจัดการเวลา Office Hours ของตนเอง; ระบบต้องรักษาสิทธิ์ของทั้งสองฝ่าย |

| Option | Description | Fairness | Operational Effort | Traceability/Risk |
|---|---|---:|---:|---|
| A | อนุญาตให้ยกเลิก/เลื่อนนัดหมายได้ตลอดเวลาจนถึงนาทีสุดท้าย | Low | High | ทำให้อาจารย์เสียเวลาและนักศึกษาคนอื่นเสียโอกาส |
| B | บังคับแจ้งยกเลิก/เลื่อนนัดล่วงหน้าอย่างน้อย 24 ชั่วโมง | High | Low | สร้างเงื่อนไขที่ชัดเจน ยุติธรรม และลดสถิติการ No-show |

**Decision/status:** เลือก Option B เป็น **Decided**  
**Rationale:** การยกเลิกกระทันหันทำให้อาจารย์เสียเวลาปฏิบัติงานและทำให้นักศึกษาคนอื่นเสียคิว การกำหนดเวลาก่อน 24 ชั่วโมงมีความสมดุลและสร้างความเป็นธรรมต่อทุกฝ่าย (E-03, E-04)  
**Unresolved:** เงื่อนไขข้อยกเว้นสำหรับกรณีเหตุสุดวิสัย (เช่น อุบัติเหตุ/ป่วยกะทันหัน)  
**Derived candidates:** RC-04

---

### N-02 / C-02 — External Messaging Application vs Institutional Channels (ช่องทางการส่งแจ้งเตือนสถานะคำขอ)

| Field | Record |
|---|---|
| Evidence | E-05, E-06 |
| Position A — Student/Advisor | ต้องการรับแจ้งเตือนผ่าน LINE Notify หรือ Push Notification บนมือถือ |
| Interest A | ได้รับข่าวสารทันที ตอบสนองได้รวดเร็วตามความคุ้นเคยของผู้ใช้งาน |
| Position B — IT Admin | ให้ใช้การแจ้งเตือนผ่าน Web Notification และ Email สถาบันเท่านั้น |
| Interest B | ควบคุมค่าใช้จ่าย ป้องกันปัญหาความซับซ้อนของ API ภายนอก และอยู่ในขอบเขตโครงการ (Scope) |
| Authority/constraint | นโยบาย IT และงบประมาณระบบสถาบันเป็นข้อจำกัดหลัก (Out of Scope สำหรับ API เสียค่าใช้จ่าย) |

| Option | Description | Feasibility | Cost | Usability |
|---|---|---:|---:|---:|
| A | ส่งแจ้งเตือนผ่าน Email สถาบัน + Web Notification ภายในระบบ | High | Low | Medium |
| B | เชื่อมต่อระบบแจ้งเตือนผ่าน LINE Notify / Official Account | Low | High | High |

**Decision/status:** เลือก Option A เป็น **Decided**  
**Rationale:** ทางเลือก B มีความซับซ้อนทางเทคนิคและอาจมีค่าใช้จ่ายเพิ่มเติมซึ่ง Out of Scope การใช้ Email สถาบันร่วมกับ Web Notification เป็นมาตรฐานสถาบันที่ครอบคลุมและเพียงพอ (E-05, E-06)  
**Unresolved:** การกำหนดความถี่ในการส่ง Email สรุปรายวัน  
**Derived candidate:** RC-06

---

### N-03 / C-03 — Calendar Integration vs Data Privacy (การเชื่อมโยงตารางเวลากับปฏิทินภายนอก)

| Field | Record |
|---|---|
| Evidence | E-01, E-02 |
| Position A — Advisor | ต้องการให้ตารางเวลาในระบบ Sync กับ Google Calendar ส่วนตัวอัตโนมัติ |
| Interest A | ความสะดวกในการดูและจัดตารางงานในที่เดียว ไม่ต้องกรอกข้อมูลซ้ำซ้อน |
| Position B — IT Admin | ให้ใช้งานตารางเวลาภายในระบบจำลองเท่านั้น ห้าม Sync ภายนอก |
| Interest B | ป้องกันประเด็น Data Privacy และการรั่วไหลของข้อมูลการนัดหมายตามนโยบาย IT |
| Authority/constraint | นโยบายความปลอดภัยข้อมูลส่วนบุคคล (Data Privacy Policy) ของสถาบัน |

| Option | Description | Security | Usability | Feasibility |
|---|---|---:|---:|---:|
| A | ใช้ระบบปฏิทินภายในระบบจำลองอย่างเดียว | High | Medium | High |
| B | Sync ข้อมูลกับ Google Calendar อัตโนมัติแบบสองทาง (Two-way sync) | Low | High | Low |

**Decision/status:** เลือก Option A เป็น **Provisional**  
**Rationale:** ทางเลือก B เสี่ยงต่อประเด็น Data Privacy และอาจขัดกับนโยบาย IT ของสถาบัน จึงกำหนดให้ใช้ปฏิทินภายในระบบเป็นหลักไปก่อนในระยะนี้ (E-01, E-02)  
**Unresolved owner:** IT Admin; นำประเด็นเรื่อง Open API/OAuth ไปสอบถามเพิ่มเติมในระยะถัดไป  
**Derived candidate:** RC-01

---

### N-04 / C-04 — On-site vs Online Consultation Mode (รูปแบบและสถานที่ในการจัดนัดหมาย)

| Field | Record |
|---|---|
| Evidence | E-03, E-04 |
| Position A — Student | ต้องการขอเข้าพบแบบออนไลน์ (Zoom / MS Teams) ได้ตามสะดวก |
| Interest A | ลดระยะเวลาและค่าใช้จ่ายในการเดินทางมาสถาบัน |
| Position B — Advisor | ต้องการเน้นการให้คำปรึกษาแบบเจอตัว (On-site) ที่ห้องพักอาจารย์เป็นหลัก |
| Interest B | ประสิทธิภาพและความชัดเจนในการสื่อสาร สื่อการเรียนการสอน หรือการตรวจเอกสาร |
| Authority/constraint | อาจารย์เป็นผู้มีอำนาจตัดสินใจสุดท้ายเรื่องรูปแบบการให้คำปรึกษาตามความเหมาะสมของเนื้อหา |

| Option | Description | Flexibility | Operational Effort | Effectiveness |
|---|---|---:|---:|---:|
| A | รองรับการเข้าพบแบบ On-site เท่านั้น | Low | Low | High |
| B | รองรับทั้งแบบ On-site และ Online (โดยให้อาจารย์ระบุลิงก์ประชุม) | High | Medium | High |

**Decision/status:** เลือก Option B เป็น **Decided**  
**Rationale:** ช่วยเพิ่มความยืดหยุ่น ยินยอมให้เลือกรูปแบบได้ตามสถานการณ์สุดวิสัย โดยให้อาจารย์เป็นผู้มีสิทธิ์อนุมัติและระบุลิงก์ห้องประชุมออนไลน์ได้เองในระบบ (E-03, E-04)  
**Unresolved:** การสร้างลิงก์ประชุมอัตโนมัติ (ให้ใช้วิธีแนบลิงก์ Manual ไปก่อน)  
**Derived candidate:** RC-05

---

## 3. Decision summary

| N-ID | Status | Accepted direction | Explicitly not decided | Next owner |
|---|---|---|---|---|
| N-01 | Decided | บังคับให้นักศึกษาแจ้งเลื่อน/ยกเลิกนัดล่วงหน้าอย่างน้อย 24 ชั่วโมง | เงื่อนไขข้อยกเว้นกรณีป่วยหรือเหตุสุดวิสัยกะทันหัน | ST-01 (นักศึกษา) / ST-02 (อาจารย์) |
| N-02 | Decided | ส่งแจ้งเตือนผ่าน Email สถาบัน + Web Notification ในระบบเท่านั้น | กำหนดรอบความถี่ (Frequency) ของการสรุปผลผ่าน Email | IT Admin / Dev Team |
| N-03 | Provisional | ใช้งานระบบปฏิทินและตารางเวลาภายในระบบจำลองเท่านั้น | นโยบายการอนุญาตเชื่อมต่อ Google Calendar OAuth ในอนาคต | IT Admin |
| N-04 | Decided | เพิ่มตัวเลือกช่องทาง On-site และ Online ในฟอร์มนัดหมาย | การเชื่อมต่อ Auto-generate Link กับ Zoom/MS Teams | Dev Team |

---

## 4. Quality check

- [x] ทุก conflict มี E-ID และอย่างน้อย 2 options
- [x] แยก position/interest/authority/constraint ชัดเจน
- [x] ใช้เกณฑ์ร่วมและบันทึก rationale ตรงตาม Evidence Log
- [x] status ไม่ overclaim ว่า Approved (ใช้ Decided/Provisional ระดับ Simulation)
- [x] สิ่งที่ยังไม่รู้มี owner และไม่ถูกเติมด้วยสมมติฐาน