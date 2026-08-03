# Week 04 — Evidence-linked Requirement Candidates

## 1. Candidate writing rule

Candidate ที่ดีใน Week 04 ต้องมี actor/system behavior หรือ quality concern ที่ชัดพอให้วิเคราะห์ต่อ อ้าง E-ID ระบุสถานะ (Status) และระดับความเชื่อมั่น (Confidence) พร้อมระบุประเด็นที่ต้อง Verify โดยยังไม่กำหนดรายละเอียดด้าน UI เทคโนโลยี หรือแนวทางการออกแบบที่ยังไม่มี Evidence รองรับ

## 2. Requirement candidates

| RC ID | Candidate statement | Type | Evidence / Decision | Status | Confidence | Follow-up / acceptance hint |
|---|---|---|---|---|---|---|
| **RC-01** | ระบบต้องแสดงช่วงเวลาว่าง (Office Hours) ของอาจารย์ที่ปรึกษา เพื่อให้นักศึกษาสามารถเลือกวันและเวลาสำหรับการนัดหมายได้ | Functional | E-01, E-02 | Candidate | High | ยืนยันระดับรายละเอียดของตารางเวลา (รายวัน/รายชั่วโมง) |
| **RC-02** | ระบบต้องให้นักศึกษาส่งคำขอนัดหมาย โดยระบุวัตถุประสงค์ รายชื่อผู้เข้าพบ และแนบเอกสารประกอบได้ เพื่อให้อาจารย์มีข้อมูลเพียงพอสำหรับการพิจารณา | Functional | E-03 | Candidate | High | ยืนยัน Required Fields และประเภทไฟล์ที่รองรับ |
| **RC-03** | ระบบต้องให้อาจารย์สามารถอนุมัติ ปฏิเสธ หรือเสนอวันและเวลานัดหมายใหม่ได้ เมื่อไม่สามารถเข้าพบตามเวลาที่ร้องขอ | Functional / Business Rule | E-04 | Candidate | High | ยืนยันเงื่อนไขการเสนอเปลี่ยนเวลานัด |
| **RC-04** | ระบบต้องแจ้งให้ผู้เกี่ยวข้องทราบเมื่อมีคำขอนัดหมายใหม่ หรือเมื่อสถานะของคำขอนัดหมายมีการเปลี่ยนแปลง | Functional / Usability | E-05, E-06 | Candidate | High | ยืนยันเหตุการณ์และช่องทางการแจ้งเตือน |
| **RC-05** | ระบบต้องกำหนดเงื่อนไขการยกเลิกหรือเลื่อนนัดหมายให้เป็นไปตามนโยบายของภาควิชา | Functional / Business Rule | E-03, E-04, C-01 | Candidate | Medium | ยืนยันนโยบายการยกเลิก การเลื่อนนัด และกรณี No-show |
| **RC-06** | ระบบต้องรองรับการนัดหมายทั้งแบบรายบุคคลและแบบกลุ่ม พร้อมรองรับการเข้าพบแบบ On-site หรือ Online ตามที่อาจารย์กำหนด | Functional | E-03, E-04, C-04 | Candidate | Medium | ยืนยันข้อมูลเพิ่มเติมที่ต้องระบุสำหรับแต่ละประเภทการนัดหมาย |
| **RC-07** | ระบบต้องกำหนดสิทธิ์การเข้าถึงข้อมูลการนัดหมายตามบทบาทของผู้ใช้งาน เพื่อปกป้องข้อมูลส่วนบุคคลและข้อมูลการให้คำปรึกษา | NFR – Security / Access Control | E-08 | Candidate | High | จัดทำ Role & Permission Matrix |
| **RC-08** | ระบบต้องสนับสนุนการบันทึกประวัติการนัดหมายและจัดทำรายงานข้อมูลการเข้าพบ เพื่อสนับสนุนการติดตามและการบริหารจัดการของภาควิชา | Functional / Reporting | E-08 | Candidate | Medium | ยืนยันรูปแบบรายงานและสิทธิ์การเข้าถึงข้อมูล |

## 3. Coverage and traceability matrix

| Week 02 source | Week 03 objective/questions | Week 04 evidence/negotiation | Candidate |
|---|---|---|---|
| F-01, OQ-01 | EO-01; Q-01–Q-03 | E-01, E-02 | RC-01 |
| F-02, OQ-02 | EO-02; Q-04–Q-06 | E-03 | RC-02 |
| OQ-03 | EO-03; Q-07–Q-08 | E-04 | RC-03 |
| F-03, OQ-04 | EO-04; Q-09–Q-10 | E-05, E-06 | RC-04 |
| OQ-04 | EO-05; Q-11 | E-03, E-04, C-01 | RC-05 |
| F-04 | EO-06; Q-12 | E-03, E-04, C-04 | RC-06 |
| AS-01 | EO-07; Q-13 | E-08 | RC-07 |
| F-05 | EO-08; Q-14 | E-08 | RC-08 |

## 4. Quality review

| Check | Result | Note |
|---|---|---|
| Traceable | Pass | RC ทุกข้อเชื่อมโยงกับ Evidence (E-ID) และ Issue/Negotiation ที่เกี่ยวข้อง |
| No unsupported approval | Pass | ใช้สถานะ Candidate ตามหลักฐานที่มี และยังไม่สรุปประเด็นที่ต้องยืนยันเพิ่มเติม |
| Solution-neutral | Pass | ยังไม่กำหนดเทคโนโลยี การเชื่อมต่อ Google Calendar หรือช่องทางแจ้งเตือนที่ยังไม่มี Evidence รองรับ |
| Atomic enough for Week 05 | Pass | แต่ละ RC มีขอบเขตชัดเจน สามารถนำไปวิเคราะห์ต่อได้ |
| Privacy / Security | Pass | RC-07 ครอบคลุมการกำหนดสิทธิ์การเข้าถึงข้อมูลตามบทบาท |
| Testability direction | Pass | ทุก RC มี Follow-up และ Acceptance Hint สำหรับใช้จัดทำ Acceptance Criteria ใน Week 06 |

## 5. Week 05 handoff backlog

### Analysis tasks

1. จัดประเภท Functional / Business Rule / NFR / Data / Interface
2. แยก RC ที่มีหลาย Concern หากจำเป็น
3. วิเคราะห์ Dependency ระหว่าง Requirement แต่ละข้อ
4. จัด Priority โดยอ้างอิง Value / Risk / Dependency
5. ยืนยัน Requirement ที่มี Confidence ระดับ Medium กับ Stakeholder
6. จัดทำ Role & Permission Matrix สำหรับการควบคุมสิทธิ์การเข้าถึงข้อมูล

### Do not do yet

- อย่ากำหนดรายละเอียดเทคโนโลยี เช่น Google Calendar API หรือ LINE Notify หากยังไม่มี Evidence
- อย่ากำหนดรายละเอียด UI หรือ Workflow เชิงออกแบบที่ยังไม่ได้รับการยืนยัน
- อย่าเลื่อน Candidate เป็น Approved โดยไม่มีการยืนยันจาก Stakeholder ที่มีอำนาจ
- อย่ากำหนดนโยบายเพิ่มเติมที่ไม่ได้มาจาก Evidence หรือ Negotiation Record
