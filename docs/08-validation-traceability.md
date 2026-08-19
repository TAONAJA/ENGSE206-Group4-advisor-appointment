# 08 — Validation, Traceability and Change Management

> **Case:** Advisor Appointment System (`advisor-appointment`)  
> **Course / Week:** ENGSE206 / Week 08  
> **Team:** ENGSE206-Group4 (Case No.9)  
> **Repository:** `https://github.com/TAONAJA/ENGSE206-Group4-advisor-appointment.git`  
> **Baseline:** `srs-v1.0`  
> **Goal:** ตรวจสอบความถูกต้องสมบูรณ์ของข้อกำหนด (Validation), สอบทานความเชื่อมโยงตลอดกระบวนการ (End-to-End Traceability), บันทึกการเปลี่ยนแปลง (Change Management) และสรุป Baseline ก่อนเข้าสู่ขั้นตอนสถาปัตยกรรมและการออกแบบระบบ

---

## 1. Validation Plan

| Validation Activity | Artefact | Participants | Criteria | Evidence / Records |
|---|---|---|---|---|
| **Stakeholder Walkthrough Simulation** | SRS v1.0 (Core Workflows), Use Case Specs | นักศึกษา (ผู้ขอเข้าพบ), อาจารย์ที่ปรึกษา, เจ้าหน้าที่ภาควิชา | **Completeness & Usability:** กระบวนการครอบคลุมตั้งแต่ค้นหาเวลาว่าง ยื่นคำขอ อนุมัติ/ปฏิเสธ/ขอเลื่อน และการแจ้งเตือน โดยไม่มีขั้นตอนตกหล่น | `../evidence/week-08/sim-walkthrough-log.md` |
| **Peer & Expert Review** | SRS v1.0, Requirement Quality Checklist | ทีมพัฒนา (ENGSE206-Group4), ทีมตรวจทาน (Peer Reviewers), ผู้สอน (อ.ธนิต เกตุแก้ว) | **Consistency & Feasibility:** ข้อกำหนดไม่ขัดแย้งกันเอง ขอบเขตสอดคล้องกับกรอบเวลา 1 ภาคการศึกษา และไม่มีข้อกำหนดเกินจริง (No Gold-plating) | `../evidence/week-08/peer-review-notes.md` |
| **Security & Constraint Audit** | NFR Specifications, Role & Permission Matrix | ผู้ดูแลระบบ IT (IT Admin), เจ้าหน้าที่ภาควิชา | **Security & Privacy:** การควบคุมสิทธิ์แบบ Role-based Access ถูกต้อง ข้อมูลเหตุผลการเข้าพบไม่รั่วไหล และสอดคล้องกับนโยบาย Data Minimization | `../evidence/week-08/security-audit-report.md` |
| **Testability & AC Verification** | Acceptance Criteria (Given-When-Then), Business Rules | Quality Observer / Test Engineer, Developers | **Testability & Verifiability:** ทุก Functional Requirement และ Business Rule มี Acceptance Measure ที่วัดผลได้และแปลงเป็น Test Case ได้ชัดเจน | `../evidence/week-08/ac-verification-matrix.md` |

---

## 2. Requirements Quality Checklist

| Check Item | Result | Evidence / Analysis Note |
|---|---|---|
| **1. Requirement มี ID และไม่ซ้ำกัน (Uniqueness)** | **Pass** | มีการกำหนดรหัสมาตรฐานแยกประเภทชัดเจน เช่น `FR-ADV-01..06`, `BR-ADV-01`, `NFR-ADV-01..04` และ `ISSUE-ADV-01..02` |
| **2. ใช้ถ้อยคำชัดเจน ไม่กำกวม (Unambiguity)** | **Pass** | ระบุ Actor, Precondition, Trigger และ Expected System Behavior ชัดเจน หลีกเลี่ยงคำว่า "รวดเร็ว" หรือ "ใช้งานง่าย" โดยไม่มีตัวชี้วัดกำกับ |
| **3. ตรวจรับหรือวัดผลได้ (Verifiability / Testability)** | **Pass** | ทุกข้อมี Acceptance Measure ชัดเจน เช่น NFR-02 ทำรายการได้ภายในไม่เกิน 4 หน้าจอ, NFR-03 โหลดหน้าตารางว่างภายใน 3 วินาที และ BR-01 บังคับกฎ 24 ชม. |
| **4. มี Source / Rationale อ้างอิง (Traceability)** | **Pass** | ทุกความต้องการเชื่อมโยงกลับไปยัง Problem Statement (`F-01..F-03`), Evidence (`E-01..E-08`), Candidate (`RC-01..RC-08`) และ Negotiation (`N-01..N-04`) |
| **5. Scope เหมาะสมและเป็น Solution-neutral** | **Pass** | ไม่ระบุเทคโนโลยีเกินความจำเป็น ขอบเขตจำกัดเฉพาะการนัดหมายในภาควิชา ส่วนฟังก์ชัน Google Calendar Sync และ LINE Notify ถูกคัดแยกไปอยู่ในส่วน Hold (Won't have) |
| **6. ครอบคลุมเคสยกเว้นและข้อผิดพลาด (Exception Handling)** | **Pass** | มีการระบุ Alternate Flows สำหรับกรณีอาจารย์ปฏิเสธ/ขอเลื่อนนัด และกรณีการส่งคำขอชนกับช่วงเวลาที่ถูกจองไปแล้ว |

---

## 3. Traceability Matrix (End-to-End Traceability)

| Need ID | Evidence / Conflict | Req ID | User Story / Use Case | Design Element / UI Component | Verification / Review Method |
|---|---|---|---|---|---|
| **UN-01** (เช็กเวลาว่างอาจารย์) | E-01, E-02 -> N-03 | **FR-ADV-01** | **US-01 / UC-01:** ดูตารางเวลาว่างและสถานะอาจารย์ | `AdvisorCalendarView`, `TimeSlotSelector`, `AvailabilityAPI` | **Simulation Test:** ตรวจสอบการแสดงผลและอัปเดตสถานะของ Time Slot ตามปฏิทินภายใน |
| **UN-02** (ส่งคำขอนัดหมาย+ไฟล์) | E-03 | **FR-ADV-02** | **US-02 / UC-02:** สร้างและส่งคำขอนัดหมาย | `AppointmentRequestForm`, `FileUploadWidget`, `RequestService` | **Form Validation Test:** ตรวจสอบ Required Fields, ขนาดไฟล์ (PDF/Docx <= 10MB) และรายชื่อผู้เข้าพบ |
| **UN-03** (พิจารณา/เลื่อนนัด) | E-04 | **FR-ADV-03** | **US-03 / UC-03:** จัดการคำขอนัดหมาย (Approve/Reject/Reschedule) | `AdvisorActionPanel`, `RescheduleModal`, `WorkflowStateMachine` | **State Transition Test:** ทดสอบการเปลี่ยน State คำขอ และบังคับกรอกเหตุผลเมื่อปฏิเสธ/เลื่อนนัด |
| **UN-04** (แจ้งเตือนสถานะ) | E-05, E-06 -> N-02 | **FR-ADV-04** | **US-04 / UC-04:** รับการแจ้งเตือนคำขอและสถานะ | `InAppNotificationBell`, `MailNotificationWorker`, `SMTPService` | **Integration Test:** ตรวจสอบการส่ง Email สถาบัน และการแจ้งเตือน Web Alert ภายใน 1 นาที |
| **UN-03** (เลือกรูปแบบเข้าพบ) | E-03, E-04 -> N-04 | **FR-ADV-05** | **US-05 / UC-05:** เลือกรูปแบบ On-site / Online | `ConsultationModeDropdown`, `MeetingLinkInput`, `LocationDetails` | **UI/Data Flow Test:** ตรวจสอบการแสดงห้องพักอาจารย์ (On-site) หรือลิงก์การประชุม (Online) |
| **PP-03** (ประวัติและสถิติภาค) | E-08 | **FR-ADV-06** | **US-06 / UC-06:** บันทึกสรุปผลและดูรายงานภาพรวม | `ConsultationSummaryForm`, `DepartmentStatsDashboard` | **Report Query Test:** ทดสอบการบันทึกสรุปผลของอาจารย์ และการดึงรายงานสรุปยอดรายภาคเรียน |
| **UN-03** (กันนัดซ้อน/ยกเลิกกระทันหัน) | E-03, E-04, C-01 -> N-01 | **BR-ADV-01** | **BR-Rule-01 / UC-02, UC-03** | `AdvanceNoticeValidator`, `CancellationLockHandler` | **Boundary Value Test:** ทดสอบกดยกเลิก/เลื่อนเวลาก่อนและหลังขีดจำกัด 24 ชั่วโมง |
| **PP-03** (ความปลอดภัยข้อมูลส่วนบุคคล) | E-08, AS-01 | **NFR-ADV-01** | **Security Scenario / All UCs** | `RolePermissionGuard`, `AuthMiddleware`, `AccessControlMatrix` | **Access Control Test:** ทดสอบการเข้าถึงข้ามสิทธิ์ระหว่าง Student, Advisor, Staff และ IT Admin |

---

## 4. Change Request Log (CR Log)

| CR-ID | Date | Requested Change | Reason / Evidence | Impacted Artefacts | Decision | Owner |
|---|---|---|---|---|---|---|
| **CR-01** | 2026-08-04 | ปรับเปลี่ยนช่องทางแจ้งเตือนจาก LINE Notify เป็น Email สถาบัน + Web Notification | ผลการเจรจา N-02 (C-02) เนื่องจาก LINE Notify มีค่าใช้จ่ายและความซับซ้อน API เกินขอบเขตโครงงาน (Out of Scope) | `FR-04`, `SRS v1.0`, `Context Diagram`, `05-requirement-backlog.md` | **Accepted** | จิราพัชร อินจันทร์ (Timekeeper/Checker) |
| **CR-02** | 2026-08-05 | ชะลอการพัฒนาระบบ Sync ตารางเวลากับ Google Calendar ส่วนตัวแบบ Two-way | ผลการเจรจา N-03 (C-03) ติดข้อจำกัดด้านความปลอดภัย Data Privacy และนโยบาย IT Admin ให้ใช้ปฏิทินจำลองภายใน | `FR-01`, `ISSUE-ADV-01`, `System Boundary`, `SRS v1.0` | **Deferred (Hold)** | จักรพงศ์ หมื่นไชยศรี (Note-taker/Analyst) |
| **CR-03** | 2026-08-08 | เพิ่มตัวเลือกระบุรูปแบบการเข้าพบทั้ง On-site และ Online (แนบลิงก์ Manual) | ผลการเจรจา N-04 (C-04) เพื่อเพิ่มความยืดหยุ่นกรณีผู้ใช้ไม่สะดวกเดินทางมาสถาบัน | `FR-05`, `FR-ADV-05`, `Request Form UI`, `SRS v1.0` | **Accepted** | ญาณวุฒิ ชวนอาจ (Presenter/Facilitator) |
| **CR-04** | 2026-08-11 | กำหนด Business Rule บังคับแจ้งยกเลิก/เลื่อนนัดล่วงหน้าอย่างน้อย 24 ชั่วโมง | ผลการเจรจา N-01 (C-01) เพื่อป้องกันการเสียเวลาปฏิบัติงานของอาจารย์ และลดอัตรา No-show | `NFR-04`, `BR-ADV-01`, `Validation Logic`, `SRS v1.0` | **Accepted** | จักรพงศ์ หมื่นไชยศรี (Note-taker/Analyst) |

---

## 5. Baseline Decision

- **Baseline Name:** `srs-v1.0-approved` (Advisor Appointment System Requirements Baseline)
- **Date:** 2026-08-18
- **Approved / Reviewed By:**
  - **Instructor:** อาจารย์ ธนิต เกตุแก้ว (ผู้ตรวจทานและกำกับมาตรฐานรายวิชา ENGSE206)
  - **Development Team (ENGSE206-Group4):**
    - นายจักรพงศ์ หมื่นไชยศรี (68543210003-8) — Note-taker
    - นายจิราพัชร อินจันทร์ (68543210004-6) — Quality & Evidence Checker
    - นายญาณวุฒิ ชวนอาจ (68543210006-1) — Facilitator & System Analyst
- **Scope Baseline Statement:** ระบบครอบคลุม Core Workflow การขอนัดหมายอาจารย์ที่ปรึกษาภายในภาควิชาบน Web Application โดยใช้ระบบยืนยันตัวตนจำลองและการแจ้งเตือนผ่าน Web + Email สถาบัน
- **Remaining Open Issues:**
  1. `ISSUE-ADV-01`: นโยบายการเชื่อมต่อ OAuth กับ Google Calendar ในระยะถัดไป (รอ IT Admin พิจารณา)
  2. `ISSUE-ADV-03`: กฎบทลงโทษกรณี No-show อย่างเป็นทางการ (รอเอกสารประกาศจากภาควิชา)
  3. `OQ-W05-02`: การกำหนดข้อยกเว้นสำหรับเงื่อนไข 24 ชั่วโมงในกรณีเหตุสุดวิสัย (ส่งมอบเป็น Alternate Flow ในขั้นตอน Design)

---

## 6. Follow-up Backlog (งานที่ต้องส่งต่อก่อนเริ่มขั้นตอน System Design & Architecture)

- [x] จัดทำ Use Case Specifications และ State Machine Diagram สำหรับ Core Workflows (`FR-ADV-01`, `FR-ADV-03`)
- [x] กำหนด Given-When-Then Acceptance Criteria สำหรับ Business Rule กฎ 24 ชั่วโมง (`BR-ADV-01`)
- [ ] นำตาราง **Role & Permission Matrix** ไปออกแบบ Data Access Layer และ Authentication Middleware ร่วมกับ UI Wireframe
- [ ] ออกแบบ **UI Component Hierarchy & Form Validation Logic** (ขนาดไฟล์ $\le$ 10MB, ประเภทไฟล์ `.pdf`, `.docx`)
- [ ] จัดทำ **Database Schema (ERD)** รองรับ Entity: `User`, `Role`, `AdvisorAvailability`, `AppointmentRequest`, `Attachment`, `ConsultationLog`
- [ ] เตรียม Mock Service สำหรับ Email Notification Worker เพื่อทดสอบจำลองบนระบบพัฒนา