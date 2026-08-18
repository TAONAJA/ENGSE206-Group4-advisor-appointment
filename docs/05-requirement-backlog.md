# 05 — Requirement Backlog v0.1: Advisor Appointment System

> **Case:** Advisor Appointment System (`advisor-appointment`)  
> **Source:** Week 04 Deliverables: Evidence Log (`E-01..E-08`), Conflict & Negotiation Record (`N-01..N-04 / C-01..C-04`), Requirement Candidates (`RC-01..RC-08`)  
> **Status:** Draft Backlog for Week 05  
> **Goal:** จัดประเภท จัดลำดับความสำคัญ (MoSCoW) วิเคราะห์ Dependency และแยกสิ่งที่พร้อมใช้ต่อ Week 06 ออกจากสิ่งที่ยังต้อง Follow-up/Hold

## 1. Project Metadata

| Field | Value |
|---|---|
| Course / Week | ENGSE206 / Week 05 |
| Team | ENGSE206-Group4 |
| Case | Case No.9 / Advisor Appointment (`advisor-appointment`) |
| Source Week04 files | `04-requirement-candidates.md`, `04-negotiation-record.md`, `04-evidence-log.md` |
| Backlog version | `v0.1` |
| Date | 2026-08-11 |

## 2. Prioritization Method

ใช้หลักการ **MoSCoW Prioritization** โดยประเมินจาก 4 มิติหลัก (ไม่ใช่ความรู้สึกของทีม):

| Dimension | วิธีใช้ในเคส Advisor Appointment |
|---|---|
| **Value** | เพิ่มความชัดเจนของเวลาว่างอาจารย์ ลดการเดินทางเก้อของนักศึกษา และลดภาระตอบแชทซ้ำ |
| **Risk** | หากไม่มี จะเกิดปัญหานัดหมายซ้อนทับ (Overlapping), นัดหมายกระทันหัน หรือสิทธิ์ข้อมูลส่วนบุคคลรั่วไหล |
| **Urgency** | จำเป็นต่อ Core Workflow (ค้นหาเวลา -> ขอเข้าพบ -> อนุมัติ -> แจ้งเตือน) หรือเป็นส่วนบันทึก/รายงานภายหลัง |
| **Dependency** | ขึ้นอยู่กับนโยบายภาควิชา (No-show/Cancellation), IT Policy (Email/SSO/Calendar API) หรือ Role Matrix |

## 3. Functional Requirements

| ID | Requirement Statement | Source / Stakeholder | Priority | Acceptance Measure | Status |
|---|---|---|---|---|---|
| **FR-ADV-01** | ระบบต้องแสดงช่วงเวลาว่าง (Office Hours) และสถานะพร้อมให้เข้าพบของอาจารย์ที่ปรึกษา เพื่อให้นักศึกษาสามารถเลือกวันและเวลาสำหรับการนัดหมายได้ | E-01, E-02 / นักศึกษา, อาจารย์ที่ปรึกษา | Must | ตารางเวลาของอาจารย์แสดงผลสถานะว่าง/ไม่ว่างได้ถูกต้องตามปฏิทิน และอัปเดตสถานะทันทีเมื่อมีรายการจอง | Ready for Week06 |
| **FR-ADV-02** | ระบบต้องให้นักศึกษาส่งคำขอนัดหมาย โดยต้องระบุวัตถุประสงค์ (เช่น ปรึกษาโปรเจกต์, ลงทะเบียน), รายชื่อผู้เข้าพบ (รายบุคคล/กลุ่ม) และแนบเอกสารประกอบได้ | E-03 / นักศึกษา | Must | นักศึกษากรอกข้อมูลครบตาม Required fields แล้วกดส่งคำขอสำเร็จ ระบบบันทึกไฟล์แนบ (PDF/Docx ไม่เกิน 10MB) เข้าสู่ระบบ | Needs Follow-up |
| **FR-ADV-03** | ระบบต้องให้อาจารย์ที่ปรึกษาสามารถอนุมัติ ปฏิเสธ หรือเสนอวันและเวลานัดหมายใหม่ (Reschedule) พร้อมระบุเหตุผลได้ | E-04 / อาจารย์ที่ปรึกษา | Must | อาจารย์กดเลือกสถานะคำขอได้ถูกต้อง โดยกรณีปฏิเสธหรือขอเลื่อนเวลาต้องบังคับกรอกเหตุผลก่อนกดยืนยัน | Ready for Week06 |
| **FR-ADV-04** | ระบบต้องส่งการแจ้งเตือนเมื่อมีคำขอนัดหมายใหม่หรือสถานะเปลี่ยนแปลง ผ่าน Email สถาบัน และ Web Notification ภายในระบบ | E-05, E-06 / นักศึกษา, อาจารย์ที่ปรึกษา | Should | ส่ง Email แจ้งเตือนไปยัง Email สถาบัน และแสดง Alert บน Web Notification ภายใน 1 นาทีหลังสถานะเปลี่ยน | Ready for Week06 |
| **FR-ADV-05** | ระบบต้องรองรับรูปแบบการเข้าพบทั้งแบบ On-site (ระบุห้อง/สถานที่) และ Online (แนบลิงก์การประชุม) | E-03, E-04 / นักศึกษา, อาจารย์ที่ปรึกษา | Should | ในหน้ารายละเอียดการนัดหมายแสดงสถานที่หรือลิงก์ห้องประชุม (เช่น Google Meet/MS Teams) ให้นักศึกษาเปิดดูได้ถูกต้อง | Ready for Week06 |
| **FR-ADV-06** | ระบบต้องสนับสนุนการบันทึกสรุปผลการเข้าพบ และจัดทำรายงานสถิติการนัดหมายภาพรวมให้ภาควิชาดูได้ | E-08 / อาจารย์ที่ปรึกษา, เจ้าหน้าที่ภาควิชา | Could | อาจารย์สามารถบันทึกข้อความสรุปหลังการพบได้ และเจ้าหน้าที่สามารถออกรายงานสรุปยอดการนัดหมายรายภาคการศึกษาได้ | Needs Follow-up |

## 4. Non-functional & Business Rule Requirements

| ID | Quality Attribute / Type | Requirement Statement | Measure / Criterion | Priority | Status |
|---|---|---|---|---|---|
| **NFR-ADV-01** | Security / Privacy | ระบบต้องจำกัดสิทธิ์การเข้าถึงข้อมูลคำขอและประวัติการนัดหมายตามบทบาท (Role-based Access Control) เพื่อคุ้มครองข้อมูลส่วนบุคคล | นักศึกษาทั่วไปต้องไม่สามารถเปิดดูข้อมูลคำขอนัดหมายของผู้อื่นได้ และสิทธิ์แก้ไขถูกจำกัดตาม Role Matrix 100% | Must | Needs Follow-up |
| **NFR-ADV-02** | Usability | ระบบต้องถูกออกแบบให้นักศึกษาสามารถค้นหาเวลาว่างและสร้างคำขอนัดหมายได้สะดวกและรวดเร็ว | นักศึกษาทำรายการค้นหาช่วงเวลาและกดส่งคำขอนัดหมายสำเร็จได้ภายในไม่เกิน 4 หน้าจอ/ขั้นตอน | Should | Ready for Week06 |
| **NFR-ADV-03** | Performance | ระบบต้องสามารถประมวลผลและแสดงผลตารางเวลาว่างของอาจารย์ได้อย่างรวดเร็ว | หน้าตารางแสดงผลเวลาว่างของอาจารย์โหลดเสร็จสิ้นภายในเวลาไม่เกิน 3 วินาที ในสภาวะเครือข่ายปกติ | Should | Ready for Week06 |
| **BR-ADV-01** | Business Rule | ระบบต้องบังคับให้นักศึกษาแจ้งยกเลิกหรือขอเลื่อนนัดหมายล่วงหน้าอย่างน้อย 24 ชั่วโมงก่อนถึงเวลานัดหมาย | ปิดกั้นไม่ให้นักศึกษากดยกเลิกหรือขอเลื่อนคำขอนัดหมายที่มีกำหนดการเข้าพบน้อยกว่า 24 ชั่วโมงล่วงหน้า | Must | Needs Follow-up |

## 5. Requirement Backlog v0.1 (Traceability & Details)

| Req ID | Source RC | Evidence / Need Trace | Requirement Statement | Type | Priority | Rationale | Status | Open Question | Week06 Use |
|---|---|---|---|---|---|---|---|---|---|
| **FR-ADV-01** | RC-01 | E-01, E-02 -> N-03 (C-03) | ระบบต้องแสดงช่วงเวลาว่าง (Office Hours) และสถานะพร้อมให้เข้าพบของอาจารย์ที่ปรึกษา เพื่อให้นักศึกษาสามารถเลือกวันและเวลาสำหรับการนัดหมายได้ | Functional | **Must** | เป็น Core Capability หลักที่แก้ปัญหาการเดินไปหาแล้วไม่เจอตัวและปัญหานัดซ้อน | **Ready for Week06** | ความถี่ในการอัปเดตตารางเวลาของอาจารย์ และระดับรายละเอียด (รายชั่วโมง/รายวัน) | Use Case + User Story |
| **FR-ADV-02** | RC-02 | E-03 | ระบบต้องให้นักศึกษาส่งคำขอนัดหมาย โดยต้องระบุวัตถุประสงค์ (เช่น ปรึกษาโปรเจกต์, ลงทะเบียน), รายชื่อผู้เข้าพบ (รายบุคคล/กลุ่ม) และแนบเอกสารประกอบได้ | Functional | **Must** | ให้อาจารย์มีข้อมูลเพียงพอในการเตรียมตัวและพิจารณาอนุมัติคำขอ | **Needs Follow-up** | Required fields ขั้นต่ำ, ประเภทไฟล์ และขนาดไฟล์แนบสูงสุด | Use Case + AC |
| **FR-ADV-03** | RC-03 | E-04 | ระบบต้องให้อาจารย์ที่ปรึกษาสามารถอนุมัติ ปฏิเสธ หรือเสนอวันและเวลานัดหมายใหม่ (Reschedule) เมื่อไม่สามารถเข้าพบตามเวลาที่ร้องขอได้ | Functional / Workflow | **Must** | เป็นจุดตัดสินใจ (Decision Point) หลักของอาจารย์ในการบริหารคิวการเข้าพบ | **Ready for Week06** | เงื่อนไขและข้อความระบุเหตุผลในการปฏิเสธหรือขอเปลี่ยนเวลา | Use Case State Machine + AC |
| **BR-ADV-01** | RC-05 | E-03, E-04, C-01 -> N-01 | ระบบต้องบังคับให้นักศึกษาแจ้งยกเลิกหรือขอเลื่อนนัดหมายล่วงหน้าอย่างน้อย 24 ชั่วโมงก่อนถึงเวลานัดหมาย | Business Rule | **Must** | ป้องกันอาจารย์เสียเวลาปฏิบัติงานและเปิดโอกาสให้นักศึกษาคนอื่นแทรกคิวได้ | **Needs Follow-up** | เงื่อนไขข้อยกเว้นกรณีเหตุสุดวิสัย (เช่น ป่วยกะทันหัน/อุบัติเหตุ) และ Penalty Rule | Business Rule + AC Validation |
| **FR-ADV-04** | RC-04 | E-05, E-06 -> N-02 (C-02) | ระบบต้องส่งการแจ้งเตือนเมื่อมีคำขอนัดหมายใหม่หรือสถานะเปลี่ยนแปลง ผ่าน Email สถาบัน และ Web Notification ภายในระบบ | Functional | **Should** | ช่วยลดความไม่แน่นอน แจ้งเตือนเรียลไทม์ โดยอยู่ใน Scope และงบประมาณ IT สถาบัน | **Ready for Week06** | รอบความถี่ (Frequency) ในการส่ง Email สรุปประจำวัน | User Story + Notification Event List |
| **FR-ADV-05** | RC-06 | E-03, E-04, C-04 -> N-04 | ระบบต้องรองรับรูปแบบการเข้าพบทั้งแบบ On-site และ Online โดยให้อาจารย์ระบุสถานที่ หรือแนบลิงก์ประชุมออนไลน์ได้ | Functional | **Should** | เพิ่มความยืดหยุ่นกรณีผู้ใช้ไม่สะดวกเดินทางมาสถาบัน | **Ready for Week06** | การแนบลิงก์ Meeting แบบ Manual (เนื่องจาก Auto-generate Out of Scope) | Use Case Extension + UI Form Hint |
| **NFR-ADV-01** | RC-07 | E-08 | ระบบต้องจำกัดสิทธิ์การเข้าถึงข้อมูลคำขอและประวัติการนัดหมายตามบทบาท (Role-based Access Control) เพื่อคุ้มครองข้อมูลส่วนบุคคล | NFR / Security | **Must** | ข้อมูลเหตุผลการเข้าพบเป็นความลับส่วนบุคคล และต้องเป็นไปตามนโยบาย Data Privacy | **Needs Follow-up** | รายละเอียดการจัดทำ Role & Permission Matrix (Student, Advisor, Staff, IT Admin) | Security Constraint + Access Matrix |
| **FR-ADV-06** | RC-08 | E-08 | ระบบต้องสนับสนุนการบันทึกสรุปผลการเข้าพบ และจัดทำรายงานสถิติการนัดหมายภาพรวมให้ภาควิชาดูได้ | Functional / Reporting | **Could** | ช่วยสนับสนุนการบริหารจัดการของภาควิชา แต่ไม่ใช่ Core Workflow การนัดหมายรายวัน | **Needs Follow-up** | รูปแบบรายงาน สิทธิ์การดูรายงาน และประเภทสถิติที่ภาควิชาต้องการ | Reporting Use Case / Mockup |
| **ISSUE-ADV-01** | C-03 | E-01, E-02 -> N-03 | ยังไม่รองรับการ Sync ตารางเวลากับ Google Calendar ส่วนตัวภายนอกแบบอัตโนมัติ | Technical Dependency / Constraint | **Won't yet** | มีความเสี่ยงด้าน Data Privacy และข้อจำกัดนโยบาย IT Admin สถาบัน (ให้ใช้ internal calendar ไปก่อน) | **Hold** | นโยบายการอนุญาตใช้งาน OAuth / Open API ของมหาวิทยาลัยในอนาคต | Follow-up only |
| **ISSUE-ADV-02** | C-02 | E-05, E-06 -> N-02 | ยังไม่รองรับการส่งแจ้งเตือนผ่าน LINE Notify หรือ Push Notification บนแอปมือถือ | Out of Scope / Issue | **Won't yet** | มีค่าใช้จ่ายภายนอกและความซับซ้อน API ซึ่งเกินขอบเขตโครงการ (Out of Scope) | **Hold** | งบประมาณหรือนโยบายแอปพลิเคชันส่วนกลางของสถาบัน | Follow-up only |

## 6. Priority Summary

| Priority | Count | Requirement IDs | เหตุผลรวม |
|---|---:|---|---|
| **Must** | 5 | FR-ADV-01, FR-ADV-02, FR-ADV-03, BR-ADV-01, NFR-ADV-01 | เป็นแกนหลักของระบบนัดหมาย (Core Workflow), ควบคุมเงื่อนไขเวลาป้องกันนัดซ้อน/No-show และคุมสิทธิ์ความปลอดภัยข้อมูลส่วนบุคคล |
| **Should** | 4 | FR-ADV-04, FR-ADV-05, NFR-ADV-02, NFR-ADV-03 | เพิ่ม Usability, Performance และความยืดหยุ่นในการสื่อสาร/เลือกรูปแบบนัดหมาย (On-site/Online) |
| **Could** | 1 | FR-ADV-06 | มีประโยชน์ต่อการติดตามประวัติของภาควิชา แต่สามารถพัฒนาเสริมหลังจาก Core Workflow เสร็จสิ้น |
| **Won't yet** | 2 | ISSUE-ADV-01, ISSUE-ADV-02 | เป็นข้อจำกัดทางเทคนิค นโยบายความปลอดภัย หรือ Out of Scope ห้ามยกระดับเป็น Requirement ในเฟสนี้ |

## 7. Status Summary: Ready / Needs Follow-up / Hold

| Status | Requirement IDs | สิ่งที่ต้องทำต่อในสัปดาห์ถัดไป |
|---|---|---|
| **Ready for Week06** | FR-ADV-01, FR-ADV-03, FR-ADV-04, FR-ADV-05, NFR-ADV-02, NFR-ADV-03 | นำไปจัดทำ User Story, Use Case Specification, State Machine Diagram และ Acceptance Criteria (Given-When-Then) |
| **Needs Follow-up** | FR-ADV-02, BR-ADV-01, NFR-ADV-01, FR-ADV-06 | ยืนยัน Required/Optional Fields, ร่าง Role & Permission Matrix, ยืนยันข้อยกเว้นกฎ 24 ชม. กับ Stakeholder |
| **Hold** | ISSUE-ADV-01, ISSUE-ADV-02 | บันทึกไว้เป็น Technical Limitation / Out of Scope Issue โดยยังไม่นำไปออกแบบหรือเขียน Code |

## 8. Review Checklist

- [x] ทุก requirement มี Source RC หรือ Evidence/Conflict source อ้างอิงชัดเจน
- [x] ทุก requirement อ้างอิง Traceability (E-ID / N-ID / C-ID)
- [x] Type แยกประเภท Functional / Business Rule / NFR / Technical Constraint / Issue ชัดเจน
- [x] Priority (MoSCoW) มี Rationale รองรับจาก Value, Risk, Urgency และ Dependency
- [x] ประเด็นทางเทคนิคภายนอก (เช่น LINE Notify, Google Calendar Sync) ไม่ถูกยกระดับเป็น Requirement โดยไม่มีหลักฐานอนุมัติ
- [x] มีระบุทิศทางการนำไปใช้ใน Week 06 (Week06 Use) สำหรับรายการที่พร้อม

## 9. Week06 Handoff

Week06 ควรเริ่มจาก requirement ที่พร้อมก่อน:

| Week06 artefact | Input ที่เหมาะสม |
|---|---|
| **User Story** | FR-ADV-01, FR-ADV-04, NFR-ADV-02 |
| **Use Case** | FR-ADV-01, FR-ADV-02 เป็น Main Flow; FR-ADV-03 เป็น Operational Flow |
| **Acceptance Criteria** | BR-ADV-01 และ FR-ADV-02 หลังยืนยัน Required fields |
| **Quality Scenario** | NFR-ADV-01 (Security) และ NFR-ADV-03 (Performance) |
| **Extension / Alternate Flow** | FR-ADV-03 (กรณีปฏิเสธ/เลื่อนนัด) และ FR-ADV-05 (On-site vs Online) |