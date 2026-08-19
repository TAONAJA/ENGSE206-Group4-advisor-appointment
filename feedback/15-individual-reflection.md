# 15 — Individual Reflection
> **Activity:** Requirement Baseline Review & Readiness Gate (Week 08 Consolidation / SRS Baseline v1.0)
> **Team:** ENGSE206 Group 4 | Case No.9 — advisor-appointment (ระบบนัดหมายเข้าพบอาจารย์ที่ปรึกษา)

---

## สมาชิกคนที่ 1: นายจักรพงศ์ หมื่นไชยศรี (Note-taker)

## Student Information
- **Name:** นายจักรพงศ์ หมื่นไชยศรี
- **Student ID:** 68543210003-8
- **Group:** Group 4
- **Case / Topic:** Case No.9 — ระบบนัดหมายเข้าพบอาจารย์ที่ปรึกษา (advisor-appointment)
- **Week / Deliverable:** Week 08 Consolidation / 08 — Requirement Baseline Review & Readiness Gate

### 1. My Contribution

- [commit / docs/01-problem-brief-v0.1.md] — รับผิดชอบรวบรวม Facts, Pain Points และเขียนร่าง Problem Statement เริ่มต้นของระบบนัดหมาย
- [commit / docs/02-stakeholder-context-scope.md] — ร่วมกำหนด System Boundary และวางกรอบการจัดเก็บข้อมูลตามหลัก Data Minimization และ Role-based Access
- [commit / docs/05-requirement-backlog.md] — จำแนกและสรุปสถานะความต้องการกลุ่มที่พร้อมพัฒนา (Ready for Week06) ออกจากกลุ่มที่ต้องรอข้อมูลเพิ่ม (Needs Follow-up)
### 2. What Went Well (จุดที่ทำได้ดี)
- สามารถสกัด Need และ Pain Points จากปัญหาเดิมที่ไม่มีระบบกลาง มาร้อยเรียงเชื่อมโยงเป็นชุดความต้องการเบื้องต้นได้อย่างครบถ้วน
- วางขอบเขตระบบ (System Boundary) ได้ชัดเจน ไม่ให้ฟังก์ชันส่วนเกิน เช่น Google Calendar Sync หรือ LINE Notify หลุดเข้ามาเป็นภาระงานก่อนมีหลักฐานรองรับ

### 3. What Went Wrong / Challenges (อุปสรรคหรือปัญหาที่เจอ)
- การตรวจสอบความสอดคล้องของรหัสอ้างอิงข้ามไฟล์ (E-ID, N-ID, RC-ID, FR/NFR-ID) ต้องใช้ความละเอียดรอบคอบสูงมากเพื่อไม่ให้รหัสหลุดหรือขัดแย้งกันเอง
- ยังมีข้อยกเว้นบางกรณี (เช่น เหตุสุดวิสัยของกฎ 24 ชั่วโมง) ที่ยังไม่สามารถหาข้อสรุปจากนโยบายทางการได้ทัน ต้องยกยอดเป็น Open Issue ชั่วคราว

### 4. Key Learnings & Improvements (สิ่งที่ได้เรียนรู้และจะปรับปรุง)
- เข้าใจอย่างลึกซึ้งว่าการเป็น Requirements Engineer ที่ดีต้องแยก Problem/Need ออกจาก Solution ให้ชัดเจน และต้องยึดหลักฐาน (Evidence) เป็นตัวตั้งเสมอ
- ในขั้นตอนการทำ Requirement Modeling (Use Case & State Machine) จะวางโครงสร้าง Main/Alternate Flow ให้รัดกุมตั้งแต่ร่างแรกเพื่อลดการกลับมาแก้ไขซ้ำ

---

## สมาชิกคนที่ 2: นายจิราพัชร อินจันทร์ (Evidence checker / Timekeeper)

## Student Information
- **Name:** นายจิราพัชร อินจันทร์
- **Student ID:** 68543210004-6
- **Group:** Group 4
- **Case / Topic:** Case No.9 — ระบบนัดหมายเข้าพบอาจารย์ที่ปรึกษา (advisor-appointment)
- **Week / Deliverable:** Week 08 Consolidation / 08 — Requirement Baseline Review & Readiness Gate

### 1. My Contribution
- [commit / docs/01-problem-brief-v0.1.md] — ตรวจสอบ Evidence ความถูกต้องของข้อมูล Stakeholder เริ่มต้น และควบคุมเวลาการทำงาน
- [commit / docs/04-evidence-log.md] — บันทึกข้อเท็จจริง Evidence Log (E-01..E-08) และร่วมเจรจาผลักดันกฎการยกเลิกนัดล่วงหน้า 24 ชม.
- [commit / docs/05-prioritization-rationale.md] — ตรวจสอบและให้เหตุผลการจัดลำดับ MoSCoW โดยอิงเกณฑ์ 4 มิติ (Value, Risk, Urgency, Dependency)

### 2. What Went Well (จุดที่ทำได้ดี)
- ควบคุมคุณภาพความต้องการให้สามารถตรวจรับได้จริง (Verifiable) โดยผลักดันให้มีตัวชี้วัดที่ชัดเจน เช่น ขนาดไฟล์แนบไม่เกิน 10MB และเวลาโหลดหน้าจอไม่เกิน 3 วินาที
- ช่วยตรวจทานความถูกต้องของหลักฐานและเหตุผลการจัดลำดับความสำคัญในเอกสาร Backlog และ Negotiation Record
### 3. What Went Wrong / Challenges (อุปสรรคหรือปัญหาที่เจอ)
- การประเมินเกณฑ์เรื่อง Performance และ Security Matrix ในระดับเริ่มต้นต้องอาศัยการเทียบเคียงมาตรฐานกลาง เนื่องจากยังไม่ได้เริ่มเขียนโค้ดและเชื่อมต่อระบบจริง[cite: 1]
- การตรวจเช็กความเชื่อมโยงของไฟล์ Backlog กับเอกสารการเจรจาในสัปดาห์ก่อนหน้าต้องใช้เวลาตรวจสอบย้อนกลับหลายรอบ

### 4. Key Learnings & Improvements (สิ่งที่ได้เรียนรู้และจะปรับปรุง)
- ได้เห็นความสำคัญของการทำ Cross-Review และการมีเกณฑ์ Acceptance Criteria ที่ชัดเจน เพราะช่วยให้ทีมพัฒนาและผู้ตรวจรับเข้าใจตรงกันตั้งแต่วันแรก
- ในสัปดาห์ถัดไปจะโฟกัสที่การร่าง Test Scenarios และเงื่อนไข Given-When-Then สำหรับ Use Case แต่ละตัวให้ครอบคลุมทุก Exception Flow

---

## สมาชิกคนที่ 3: นายญาณวุฒิ ชวนอาจ (Presenter / Facilitator)

## Student Information
- **Name:** นายญาณวุฒิ ชวนอาจ
- **Student ID:** 68543210006-1
- **Group:** Group 4
- **Case / Topic:** Case No.9 — ระบบนัดหมายเข้าพบอาจารย์ที่ปรึกษา (advisor-appointment)
- **Week / Deliverable:** Week 08 Consolidation / 08 — Requirement Baseline Review & Readiness Gate

### 1. My Contribution
- [commit / docs/02-stakeholder-context-scope.md] — จัดทำ Stakeholder Profiles ละเอียด 4 บทบาท วางผัง Data Flow และกำหนดขอบเขต In/Out Scope
- [commit / project-management/ai-use-log.md] — บันทึกประวัติการใช้งาน AI และร่วมอัปเดต Decision Log บันทึกการล็อก Baseline srs-v1.0 (D-04)

- [commit / docs/04-negotiation-record.md] — วิเคราะห์ Position/Interest และเปรียบเทียบ Options ทางเลือกในการเจรจาข้อขัดแย้งประเด็นช่องทางสื่อสารและสถานที่ (N-02, N-04)
### 2. What Went Well (จุดที่ทำได้ดี)
- ประสานงานภายในทีมได้อย่างราบรื่น มีการแบ่งหน้าที่ชัดเจนตามความถนัด และสามารถส่งมอบเอกสารได้ครบถ้วนตามเกณฑ์ Readiness Gate ทุกข้อ
- สามารถเจรจาและหาจุดสมดุลระหว่างความต้องการของผู้ใช้งานที่หลากหลาย (นักศึกษา vs อาจารย์ vs ผู้ดูแลระบบ IT) ให้ออกมาเป็นข้อกำหนดที่ทำได้จริง

### 3. What Went Wrong / Challenges (อุปสรรคหรือปัญหาที่เจอ)
- มีประเด็นทางเทคนิคภายนอก (เช่น ข้อจำกัด SSO และ API นโยบายสถาบัน) ที่ต้องประสานงานกับผู้เกี่ยวข้องหลายฝ่าย ทำให้ต้องใช้การตัดสินใจแบบ Provisional ไปก่อน
- การบริหารจัดการเวลาในการประชุมทีมเพื่อสรุปข้อขัดแย้งของเอกสารที่มีปริมาณมาก

### 4. Key Learnings & Improvements (สิ่งที่ได้เรียนรู้และจะปรับปรุง)
- ได้เรียนรู้ว่ากระบวนการ Software Process ที่เป็นระบบและการบันทึก Decision Log อย่างต่อเนื่อง ช่วยลดความสับสนและป้องกันการตัดสินใจซ้ำซ้อนได้อย่างมีประสิทธิภาพ 
- ในสัปดาห์ถัดไปจะนำทีมจัดทำ Use Case Diagram และออกแบบ Interaction ระหว่าง Actor กับ System ให้ชัดเจนเพื่อเตรียมความพร้อมสำหรับ Architecture Design