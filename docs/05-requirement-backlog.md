# 05 — Requirement Backlog v0.1: Advisor Appointment System

> **Case:** Advisor Appointment System (`advisor-appointment`)[cite: 3]  
> **Source:** Week 04 Deliverables: Evidence Log (`E-01..E-08`), Conflict & Negotiation Record (`N-01..N-04 / C-01..C-04`), Requirement Candidates (`RC-01..RC-08`)[cite: 3]  
> **Status:** Draft Backlog for Week 05[cite: 3]  
> **Goal:** จัดประเภท จัดลำดับความสำคัญ (MoSCoW) วิเคราะห์ Dependency และแยกสิ่งที่พร้อมใช้ต่อ Week 06 ออกจากสิ่งที่ยังต้อง Follow-up/Hold[cite: 3]

## 1. Project Metadata

| Field | Value |
|---|---|
| Course / Week | ENGSE206 / Week 05[cite: 3] |
| Team | ENGSE206-Group4[cite: 3] |
| Case | Case No.9 / Advisor Appointment (`advisor-appointment`)[cite: 3] |
| Source Week04 files | `04-requirement-candidates.md`, `04-negotiation-record.md`, `04-evidence-log.md`[cite: 3] |
| Backlog version | `v0.1`[cite: 3] |
| Date | 2026-08-11[cite: 3] |

## 2. Prioritization Method

ใช้หลักการ **MoSCoW Prioritization** โดยประเมินจาก 4 มิติหลัก (ไม่ใช่ความรู้สึกของทีม)[cite: 3]:

| Dimension | วิธีใช้ในเคส Advisor Appointment[cite: 3] |
|---|---|
| **Value** | เพิ่มความชัดเจนของเวลาว่างอาจารย์ ลดการเดินทางเก้อของนักศึกษา และลดภาระตอบแชทซ้ำ[cite: 3] |
| **Risk** | หากไม่มี จะเกิดปัญหานัดหมายซ้อนทับ (Overlapping), นัดหมายกระทันหัน หรือสิทธิ์ข้อมูลส่วนบุคคลรั่วไหล[cite: 3] |
| **Urgency** | จำเป็นต่อ Core Workflow (ค้นหาเวลา -> ขอเข้าพบ -> อนุมัติ -> แจ้งเตือน) หรือเป็นส่วนบันทึก/รายงานภายหลัง[cite: 3] |
| **Dependency** | ขึ้นอยู่กับนโยบายภาควิชา (No-show/Cancellation), IT Policy (Email/SSO/Calendar API) หรือ Role Matrix[cite: 3] |

## 3. Functional Requirements

| ID | Requirement Statement | Source / Stakeholder | Priority | Acceptance Measure | Status |
|---|---|---|---|---|---|
| **FR-01** | ระบบต้องแสดงช่วงเวลาว่าง (Office Hours) และสถานะพร้อมให้เข้าพบของอาจารย์ที่ปรึกษา เพื่อให้นักศึกษาสามารถเลือกวันและเวลาสำหรับการนัดหมายได้ | E-01, E-02 / นักศึกษา, อาจารย์ที่ปรึกษา[cite: 3] | Must | ตารางเวลาของอาจารย์แสดงผลสถานะว่าง/ไม่ว่างได้ถูกต้องตามปฏิทิน และอัปเดตสถานะทันทีเมื่อมีรายการจอง[cite: 3] | Ready for Week06 |
| **FR-02** | ระบบต้องให้นักศึกษาส่งคำขอนัดหมาย โดยต้องระบุวัตถุประสงค์ (เช่น ปรึกษาโปรเจกต์, ลงทะเบียน), รายชื่อผู้เข้าพบ (รายบุคคล/กลุ่ม) และแนบเอกสารประกอบได้[cite: 3] | E-03 / นักศึกษา[cite: 3] | Must | นักศึกษากรอกข้อมูลครบตาม Required fields แล้วกดส่งคำขอสำเร็จ ระบบบันทึกไฟล์แนบ (PDF/Docx ไม่เกิน 10MB) เข้าสู่ระบบ[cite: 3] | Needs Follow-up |
| **FR-03** | ระบบต้องให้อาจารย์ที่ปรึกษาสามารถอนุมัติ ปฏิเสธ หรือเสนอวันและเวลานัดหมายใหม่ (Reschedule) พร้อมระบุเหตุผลได้[cite: 3] | E-04 / อาจารย์ที่ปรึกษา[cite: 3] | Must | อาจารย์กดเลือกสถานะคำขอได้ถูกต้อง โดยกรณีปฏิเสธหรือขอเลื่อนเวลาต้องบังคับกรอกเหตุผลก่อนกดยืนยัน[cite: 3] | Ready for Week06 |
| **FR-04** | ระบบต้องส่งการแจ้งเตือนเมื่อมีคำขอนัดหมายใหม่หรือสถานะเปลี่ยนแปลง ผ่าน Email สถาบัน และ Web Notification ภายในระบบ[cite: 3] | E-05, E-06 / นักศึกษา, อาจารย์ที่ปรึกษา[cite: 3] | Should | ส่ง Email แจ้งเตือนไปยัง Email สถาบัน และแสดง Alert บน Web Notification ภายใน 1 นาทีหลังสถานะเปลี่ยน[cite: 3] | Ready for Week06 |
| **FR-05** | ระบบต้องรองรับรูปแบบการเข้าพบทั้งแบบ On-site (ระบุห้อง/สถานที่) และ Online (แนบลิงก์การประชุม)[cite: 3] | E-03, E-04 / นักศึกษา, อาจารย์ที่ปรึกษา[cite: 3] | Should | ในหน้ารายละเอียดการนัดหมายแสดงสถานที่หรือลิงก์ห้องประชุม (เช่น Google Meet/MS Teams) ให้นักศึกษาเปิดดูได้ถูกต้อง[cite: 3] | Ready for Week06 |
| **FR-06** | ระบบต้องสนับสนุนการบันทึกสรุปผลการเข้าพบ และจัดทำรายงานสถิติการนัดหมายภาพรวมให้ภาควิชาดูได้[cite: 3] | E-08 / อาจารย์ที่ปรึกษา, เจ้าหน้าที่ภาควิชา[cite: 3] | Could | อาจารย์สามารถบันทึกข้อความสรุปหลังการพบได้ และเจ้าหน้าที่สามารถออกรายงานสรุปยอดการนัดหมายรายภาคการศึกษาได้[cite: 3] | Needs Follow-up |

## 4. Non-functional & Business Rule Requirements

| ID | Quality Attribute / Type | Requirement Statement | Measure / Criterion | Priority | Status |
|---|---|---|---|---|---|
| **NFR-01** | Security / Privacy | ระบบต้องจำกัดสิทธิ์การเข้าถึงข้อมูลคำขอและประวัติการนัดหมายตามบทบาท (Role-based Access Control) เพื่อคุ้มครองข้อมูลส่วนบุคคล[cite: 3] | นักศึกษาทั่วไปต้องไม่สามารถเปิดดูข้อมูลคำขอนัดหมายของผู้อื่นได้ และสิทธิ์แก้ไขถูกจำกัดตาม Role Matrix 100%[cite: 3] | Must | Needs Follow-up |
| **NFR-02** | Usability | ระบบต้องถูกออกแบบให้นักศึกษาสามารถค้นหาเวลาว่างและสร้างคำขอนัดหมายได้สะดวกและรวดเร็ว[cite: 3] | นักศึกษาทำรายการค้นหาช่วงเวลาและกดส่งคำขอนัดหมายสำเร็จได้ภายในไม่เกิน 4 หน้าจอ/ขั้นตอน[cite: 3] | Should | Ready for Week06 |
| **NFR-03** | Performance | ระบบต้องสามารถประมวลผลและแสดงผลตารางเวลาว่างของอาจารย์ได้อย่างรวดเร็ว[cite: 3] | หน้าตารางแสดงผลเวลาว่างของอาจารย์โหลดเสร็จสิ้นภายในเวลาไม่เกิน 3 วินาที ในสภาวะเครือข่ายปกติ[cite: 3] | Should | Ready for Week06 |
| **BR-01** | Business Rule | ระบบต้องบังคับให้นักศึกษาแจ้งยกเลิกหรือขอเลื่อนนัดหมายล่วงหน้าอย่างน้อย 24 ชั่วโมงก่อนถึงเวลานัดหมาย[cite: 3] | ปิดกั้นไม่ให้นักศึกษากดยกเลิกหรือขอเลื่อนคำขอนัดหมายที่มีกำหนดการเข้าพบน้อยกว่า 24 ชั่วโมงล่วงหน้า[cite: 3] | Must | Needs Follow-up |

## 5. Requirement Backlog v0.1 (Traceability & Details)

| Req ID | Source RC | Evidence / Need Trace | Requirement Statement | Type | Priority | Rationale | Status | Open Question | Week06 Use |
|---|---|---|---|---|---|---|---|---|---|
| **FR-01** | RC-01[cite: 3] | E-01, E-02 -> N-03 (C-03)[cite: 3] | ระบบต้องแสดงช่วงเวลาว่าง (Office Hours) และสถานะพร้อมให้เข้าพบของอาจารย์ที่ปรึกษา เพื่อให้นักศึกษาสามารถเลือกวันและเวลาสำหรับการนัดหมายได้[cite: 3] | Functional[cite: 3] | **Must**[cite: 3] | เป็น Core Capability หลักที่แก้ปัญหาการเดินไปหาแล้วไม่เจอตัวและปัญหานัดซ้อน[cite: 3] | **Ready for Week06**[cite: 3] | ความถี่ในการอัปเดตตารางเวลาของอาจารย์ และระดับรายละเอียด (รายชั่วโมง/รายวัน)[cite: 3] | Use Case + User Story[cite: 3] |
| **FR-02** | RC-02[cite: 3] | E-03[cite: 3] | ระบบต้องให้นักศึกษาส่งคำขอนัดหมาย โดยต้องระบุวัตถุประสงค์ (เช่น ปรึกษาโปรเจกต์, ลงทะเบียน), รายชื่อผู้เข้าพบ (รายบุคคล/กลุ่ม) และแนบเอกสารประกอบได้[cite: 3] | Functional[cite: 3] | **Must**[cite: 3] | ให้อาจารย์มีข้อมูลเพียงพอในการเตรียมตัวและพิจารณาอนุมัติคำขอ[cite: 3] | **Needs Follow-up**[cite: 3] | Required fields ขั้นต่ำ, ประเภทไฟล์ และขนาดไฟล์แนบสูงสุด[cite: 3] | Use Case + AC[cite: 3] |
| **FR-03** | RC-03[cite: 3] | E-04[cite: 3] | ระบบต้องให้อาจารย์ที่ปรึกษาสามารถอนุมัติ ปฏิเสธ หรือเสนอวันและเวลานัดหมายใหม่ (Reschedule) เมื่อไม่สามารถเข้าพบตามเวลาที่ร้องขอได้[cite: 3] | Functional / Workflow[cite: 3] | **Must**[cite: 3] | เป็นจุดตัดสินใจ (Decision Point) หลักของอาจารย์ในการบริหารคิวการเข้าพบ[cite: 3] | **Ready for Week06**[cite: 3] | เงื่อนไขและข้อความระบุเหตุผลในการปฏิเสธหรือขอเปลี่ยนเวลา[cite: 3] | Use Case State Machine + AC[cite: 3] |
| **BR-01** | RC-05[cite: 3] | E-03, E-04, C-01 -> N-01[cite: 3] | ระบบต้องบังคับให้นักศึกษาแจ้งยกเลิกหรือขอเลื่อนนัดหมายล่วงหน้าอย่างน้อย 24 ชั่วโมงก่อนถึงเวลานัดหมาย[cite: 3] | Business Rule[cite: 3] | **Must**[cite: 3] | ป้องกันอาจารย์เสียเวลาปฏิบัติงานและเปิดโอกาสให้นักศึกษาคนอื่นแทรกคิวได้[cite: 3] | **Needs Follow-up**[cite: 3] | เงื่อนไขข้อยกเว้นกรณีเหตุสุดวิสัย (เช่น ป่วยกะทันหัน/อุบัติเหตุ) และ Penalty Rule[cite: 3] | Business Rule + AC Validation[cite: 3] |
| **FR-04** | RC-04[cite: 3] | E-05, E-06 -> N-02 (C-02)[cite: 3] | ระบบต้องส่งการแจ้งเตือนเมื่อมีคำขอนัดหมายใหม่หรือสถานะเปลี่ยนแปลง ผ่าน Email สถาบัน และ Web Notification ภายในระบบ[cite: 3] | Functional[cite: 3] | **Should**[cite: 3] | ช่วยลดความไม่แน่นอน แจ้งเตือนเรียลไทม์ โดยอยู่ใน Scope และงบประมาณ IT สถาบัน[cite: 3] | **Ready for Week06**[cite: 3] | รอบความถี่ (Frequency) ในการส่ง Email สรุปประจำวัน[cite: 3] | User Story + Notification Event List[cite: 3] |
| **FR-05** | RC-06[cite: 3] | E-03, E-04, C-04 -> N-04[cite: 3] | ระบบต้องรองรับรูปแบบการเข้าพบทั้งแบบ On-site และ Online โดยให้อาจารย์ระบุสถานที่ หรือแนบลิงก์ประชุมออนไลน์ได้[cite: 3] | Functional[cite: 3] | **Should**[cite: 3] | เพิ่มความยืดหยุ่นกรณีผู้ใช้ไม่สะดวกเดินทางมาสถาบัน[cite: 3] | **Ready for Week06**[cite: 3] | การแนบลิงก์ Meeting แบบ Manual (เนื่องจาก Auto-generate Out of Scope)[cite: 3] | Use Case Extension + UI Form Hint[cite: 3] |
| **NFR-01** | RC-07[cite: 3] | E-08[cite: 3] | ระบบต้องจำกัดสิทธิ์การเข้าถึงข้อมูลคำขอและประวัติการนัดหมายตามบทบาท (Role-based Access Control) เพื่อคุ้มครองข้อมูลส่วนบุคคล[cite: 3] | NFR / Security[cite: 3] | **Must**[cite: 3] | ข้อมูลเหตุผลการเข้าพบเป็นความลับส่วนบุคคล และต้องเป็นไปตามนโยบาย Data Privacy[cite: 3] | **Needs Follow-up**[cite: 3] | รายละเอียดการจัดทำ Role & Permission Matrix (Student, Advisor, Staff, IT Admin)[cite: 3] | Security Constraint + Access Matrix[cite: 3] |
| **FR-06** | RC-08[cite: 3] | E-08[cite: 3] | ระบบต้องสนับสนุนการบันทึกสรุปผลการเข้าพบ และจัดทำรายงานสถิติการนัดหมายภาพรวมให้ภาควิชาดูได้[cite: 3] | Functional / Reporting[cite: 3] | **Could**[cite: 3] | ช่วยสนับสนุนการบริหารจัดการของภาควิชา แต่ไม่ใช่ Core Workflow การนัดหมายรายวัน[cite: 3] | **Needs Follow-up**[cite: 3] | รูปแบบรายงาน สิทธิ์การดูรายงาน และประเภทสถิติที่ภาควิชาต้องการ[cite: 3] | Reporting Use Case / Mockup[cite: 3] |
| **ISSUE-01** | C-03[cite: 3] | E-01, E-02 -> N-03[cite: 3] | ยังไม่รองรับการ Sync ตารางเวลากับ Google Calendar ส่วนตัวภายนอกแบบอัตโนมัติ[cite: 3] | Technical Dependency / Constraint[cite: 3] | **Won't yet**[cite: 3] | มีความเสี่ยงด้าน Data Privacy และข้อจำกัดนโยบาย IT Admin สถาบัน (ให้ใช้ internal calendar ไปก่อน)[cite: 3] | **Hold**[cite: 3] | นโยบายการอนุญาตใช้งาน OAuth / Open API ของมหาวิทยาลัยในอนาคต[cite: 3] | Follow-up only[cite: 3] |
| **ISSUE-02** | C-02[cite: 3] | E-05, E-06 -> N-02[cite: 3] | ยังไม่รองรับการส่งแจ้งเตือนผ่าน LINE Notify หรือ Push Notification บนแอปมือถือ[cite: 3] | Out of Scope / Issue[cite: 3] | **Won't yet**[cite: 3] | มีค่าใช้จ่ายภายนอกและความซับซ้อน API ซึ่งเกินขอบเขตโครงการ (Out of Scope)[cite: 3] | **Hold**[cite: 3] | งบประมาณหรือนโยบายแอปพลิเคชันส่วนกลางของสถาบัน[cite: 3] | Follow-up only[cite: 3] |

## 6. Priority Summary

| Priority | Count | Requirement IDs | เหตุผลรวม |
|---|---:|---|---|
| **Must** | 5 | FR-01, FR-02, FR-03, BR-01, NFR-01[cite: 3] | เป็นแกนหลักของระบบนัดหมาย (Core Workflow), ควบคุมเงื่อนไขเวลาป้องกันนัดซ้อน/No-show และคุมสิทธิ์ความปลอดภัยข้อมูลส่วนบุคคล[cite: 3] |
| **Should** | 4 | FR-04, FR-05, NFR-02, NFR-03[cite: 3] | เพิ่ม Usability, Performance และความยืดหยุ่นในการสื่อสาร/เลือกรูปแบบนัดหมาย (On-site/Online)[cite: 3] |
| **Could** | 1 | FR-06[cite: 3] | มีประโยชน์ต่อการติดตามประวัติของภาควิชา แต่สามารถพัฒนาเสริมหลังจาก Core Workflow เสร็จสิ้น[cite: 3] |
| **Won't yet** | 2 | ISSUE-01, ISSUE-02[cite: 3] | เป็นข้อจำกัดทางเทคนิค นโยบายความปลอดภัย หรือ Out of Scope ห้ามยกระดับเป็น Requirement ในเฟสนี้[cite: 3] |

## 7. Status Summary: Ready / Needs Follow-up / Hold

| Status | Requirement IDs | สิ่งที่ต้องทำต่อในสัปดาห์ถัดไป |
|---|---|---|
| **Ready for Week06** | FR-01, FR-03, FR-04, FR-05, NFR-02, NFR-03[cite: 3] | นำไปจัดทำ User Story, Use Case Specification, State Machine Diagram และ Acceptance Criteria (Given-When-Then)[cite: 3] |
| **Needs Follow-up** | FR-02, BR-01, NFR-01, FR-06[cite: 3] | ยืนยัน Required/Optional Fields, ร่าง Role & Permission Matrix, ยืนยันข้อยกเว้นกฎ 24 ชม. กับ Stakeholder[cite: 3] |
| **Hold** | ISSUE-01, ISSUE-02[cite: 3] | บันทึกไว้เป็น Technical Limitation / Out of Scope Issue โดยยังไม่นำไปออกแบบหรือเขียน Code[cite: 3] |

## 8. Review Checklist

- [x] ทุก requirement มี Source RC หรือ Evidence/Conflict source อ้างอิงชัดเจน[cite: 3]
- [x] ทุก requirement อ้างอิง Traceability (E-ID / N-ID / C-ID)[cite: 3]
- [x] Type แยกประเภท Functional / Business Rule / NFR / Technical Constraint / Issue ชัดเจน[cite: 3]
- [x] Priority (MoSCoW) มี Rationale รองรับจาก Value, Risk, Urgency และ Dependency[cite: 3]
- [x] ประเด็นทางเทคนิคภายนอก (เช่น LINE Notify, Google Calendar Sync) ไม่ถูกยกระดับเป็น Requirement โดยไม่มีหลักฐานอนุมัติ[cite: 3]
- [x] มีระบุทิศทางการนำไปใช้ใน Week 06 (Week06 Use) สำหรับรายการที่พร้อม[cite: 3]

## 9. Week06 Handoff

Week06 ควรเริ่มจาก requirement ที่พร้อมก่อน[cite: 2, 3]:

| Week06 artefact | Input ที่เหมาะสม |
|---|---|
| **User Story** | FR-01, FR-04, NFR-02[cite: 3] |
| **Use Case** | FR-01, FR-02 เป็น Main Flow; FR-03 เป็น Operational Flow[cite: 3] |
| **Acceptance Criteria** | BR-01 และ FR-02 หลังยืนยัน Required fields[cite: 3] |
| **Quality Scenario** | NFR-01 (Security) และ NFR-03 (Performance)[cite: 3] |
| **Extension / Alternate Flow** | FR-03 (กรณีปฏิเสธ/เลื่อนนัด) และ FR-05 (On-site vs Online)[cite: 3] |