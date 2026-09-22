# ระบบนัดหมายเข้าพบอาจารย์ที่ปรึกษา (Advisor Appointment System) — Software Requirements Specification Draft v1

## 0. Document Control

| Field | Value |
|---|---|
| Case ID | `Case No.9 / advisor-appointment` |
| Document ID | `ADV-SRS-W07-v1` |
| Version | `1.0-draft` |
| Status | Baseline Candidate |
| Team/Owner | `ENGSE206-Group4` (จักรพงศ์ หมื่นไชยศรี, จิราพัชร อินจันทร์, ญาณวุฒิ ชวนอาจ) |
| W05 source snapshot | `05-requirement-backlog.md (v0.1)`, `05-prioritization-rationale.md`, `05-open-questions-issues.md` |
| W06 source snapshot | `06-requirement-models.md (v0.1)` |

## 1. Introduction

### 1.1 Purpose

เอกสารฉบับนี้จัดทำขึ้นเพื่อกำหนดข้อกำหนดความต้องการซอฟต์แวร์ (SRS) ขั้นสมบูรณ์สำหรับ "ระบบนัดหมายเข้าพบอาจารย์ที่ปรึกษา (Advisor Appointment System)" โดยใช้เป็นเกณฑ์อ้างอิงพื้นฐาน (Baseline) ร่วมกันระหว่างอาจารย์ผู้สอน, ผู้มีส่วนได้ส่วนเสีย, นักวิเคราะห์ระบบ และทีมพัฒนา เพื่อนำไปใช้เป็นกรอบในการออกแบบสถาปัตยกรรม ออกแบบฐานข้อมูล ออกแบบหน้าจอ และวางแผนทดสอบระบบในขั้นตอนถัดไป

### 1.2 Problem and Goals

| Goal | Desired outcome | Source | Status |
|---|---|---|---|
| `G-01` | นักศึกษาสามารถตรวจสอบช่วงเวลาว่าง (Office Hours) ของอาจารย์ที่ปรึกษา และส่งคำขอนัดหมายเข้าพบผ่านช่องทางกลางช่องทางเดียวได้แบบเรียลไทม์ | F-01, PP-01, E-01, E-02 | Fact |
| `G-02` | อาจารย์ที่ปรึกษาสามารถบริหารจัดการคิว อนุมัติ ปฏิเสธ หรือเสนอเลื่อนเวลานัดหมายได้สะดวกในระบบเดียว ลดภาระการตอบแชทซ้ำๆ | F-02, PP-02, E-04 | Fact |
| `G-03` | มีระบบแจ้งเตือนสถานะคำขอนัดหมายผ่าน Email สถาบัน และ Web Notification ภายในระบบ เพื่อลดปัญหานัดหมายผิดพลาดหรือเวลาซ้อนทับกัน | E-05, E-06, N-02 | Decision |
| `G-04` | กำหนดกติกาการยกเลิก/เลื่อนนัดล่วงหน้าอย่างน้อย 24 ชั่วโมง เพื่อป้องกันการเสียเวลาทำงานของอาจารย์ และเปิดโอกาสให้นักศึกษาคนอื่นแทรกคิวได้ | C-01, N-01, BR-ADV-01 | Decision |

### 1.3 Product Scope

| In Scope | Out of Scope / Extension | Reason/source |
|---|---|---|
| การแสดงปฏิทินตารางเวลาว่าง (Office Hours) ของอาจารย์ภายในระบบ | การเชื่อมต่อปฏิทินภายนอกแบบอัตโนมัติ (Google Calendar Two-way Sync) | ติดเงื่อนไขด้านนโยบายความปลอดภัยและ Data Privacy ของสถาบัน (C-03, N-03, ISSUE-ADV-01) |
| การส่งคำขอนัดหมายพร้อมระบุวัตถุประสงค์ รายชื่อผู้เข้าพบ (เดี่ยว/กลุ่ม) และแนบไฟล์ประกอบ | ระบบลงทะเบียนเรียนหลัก และระบบจัดการเรียนการสอน (LMS) ของมหาวิทยาลัย | เป็นระบบขนาดใหญ่ที่มีความซับซ้อนสูงและอยู่นอกกรอบการบริหารเวลานัดหมาย |
| อาจารย์อนุมัติ, ปฏิเสธ (พร้อมระบุเหตุผล), หรือเสนอเปลี่ยนวันเวลานัดหมายใหม่ | การอนุมัติคำขอนัดหมายแบบอัตโนมัติ (Auto-approval) | อาจารย์ต้องการตรวจสอบเนื้อหาและจัดสรรเวลาด้วยตนเองก่อนเสมอ (ISSUE-ADV-04) |
| การแจ้งเตือนสถานะผ่าน Email สถาบัน และ Web Notification ภายในเว็บ | การส่งข้อความแจ้งเตือนผ่าน LINE Notify, LINE OA หรือ Mobile Push Notification | มีค่าใช้จ่ายภายนอกและความซับซ้อนด้าน API เกินขอบเขตของรายวิชา (C-02, N-02, ISSUE-ADV-02) |
| การเลือกรูปแบบการเข้าพบทั้งแบบ On-site และ Online (อาจารย์แนบลิงก์ประชุม Manual) | การสร้างห้องประชุมอัตโนมัติ (Auto-generate Meet/Teams Link) | หลีกเลี่ยงความซับซ้อนในการผูกสิทธิ์ API ระดับองค์กร (C-04, N-04) |
| การบังคับใช้กฎยกเลิก/ขอเลื่อนนัดล่วงหน้าไม่น้อยกว่า 24 ชั่วโมง | บทลงโทษกรณี No-show หรือการตัดสิทธิ์การจองคิว | ยังไม่มีเอกสารนโยบายรองรับอย่างเป็นทางการจากภาควิชา (ISSUE-ADV-03) |
| การบันทึกสรุปผลหลังการเข้าพบ และรายงานสถิติการนัดหมายภาพรวมภาควิชา | ระบบลาเรียน/ลาป่วยอย่างเป็นทางการของภาควิชา | อยู่นอกเหนือขอบเขตการนัดหมายอาจารย์ที่ปรึกษา |

### 1.4 Definitions

| Term | Meaning | Source/Decision |
|---|---|---|
| `Office Hours` | ช่วงเวลาที่อาจารย์ที่ปรึกษากำหนดไว้ในระบบว่าสะดวกและพร้อมให้นักศึกษาเข้าพบ | Case Card, E-02 |
| `Pending` | สถานะคำขอนัดหมายที่สร้างสำเร็จและกำลังรออาจารย์ที่ปรึกษาพิจารณา | UC-02, AC-03 |
| `Confirmed` | สถานะคำขอนัดหมายที่อาจารย์กดอนุมัติเรียบร้อยแล้ว และช่วงเวลาดังกล่าวจะถูกล็อกในปฏิทิน | UC-03, AC-06 |
| `Rejected` | สถานะคำขอนัดหมายที่อาจารย์กดปฏิเสธ พร้อมระบุเหตุผลประกอบ | UC-03, AC-07 |
| `Rescheduled` | สถานะคำขอนัดหมายที่อาจารย์ขอปรับเปลี่ยนวันหรือเวลาใหม่ เพื่อให้นักศึกษายืนยัน | UC-03, AC-08 |
| `Cancelled` | สถานะคำขอนัดหมายที่ถูกยกเลิกตามเงื่อนไขเวลาที่ระบบอนุญาต | UC-04, AC-11 |
| `Completed` | สถานะการนัดหมายที่ผ่านพ้นเวลาไปแล้วและอาจารย์ได้บันทึกสรุปผลการเข้าพบเรียบร้อย | UC-06, AC-13 |
| `No-show` | สภาพการณ์ที่นักศึกษาไม่มาตามนัดหมายที่ได้รับการยืนยันแล้ว โดยไม่มีการยกเลิกล่วงหน้า | OQ-02, ISSUE-ADV-03 |
| `RBAC` | Role-Based Access Control การควบคุมสิทธิ์การเข้าถึงข้อมูลและฟังก์ชันตามบทบาทผู้ใช้ | NFR-ADV-01, E-08 |

---

## 2. Overall Description

### 2.1 Product Context

ระบบนัดหมายเข้าพบอาจารย์ที่ปรึกษาเป็นเว็บแอปพลิเคชันส่วนกลางสำหรับภาควิชา ทำหน้าที่เป็น System of Record ในการจัดเก็บข้อมูลช่วงเวลาว่าง คำขอนัดหมาย สถานะการอนุมัติ และบันทึกประวัติการเข้าพบ โดยตัวระบบทำงานเชื่อมต่อกับระบบภายนอกเฉพาะที่จำเป็น คือ บริการยืนยันตัวตนสถาบัน (Mock/Institution Identity Service) เพื่อตรวจสอบบทบาทผู้ใช้ และระบบส่งอีเมลของสถาบัน (Mail Service) เพื่อส่งแจ้งเตือน โดยระบบจะไม่มีการซิงค์ข้อมูลกับปฏิทินส่วนตัวภายนอก (Google Calendar) เพื่อรักษาความปลอดภัยและความเป็นส่วนตัวของข้อมูล

### 2.2 User Classes and Authority

| Actor | Goal | Authorized actions | Restrictions | Source |
|---|---|---|---|---|
| `ACT-01: นักศึกษา (Student)` | ค้นหาเวลาว่างของอาจารย์ ส่งคำขอ และติดตามผลนัดหมาย | ดูตารางเวลาว่าง, ส่งคำขอเข้าพบ, แนบไฟล์, กดยกเลิกนัดหมายล่วงหน้า > 24 ชม., ดูบันทึกสรุปการเข้าพบของตนเอง | ห้ามดูคำขอหรือข้อมูลส่วนบุคคลของนักศึกษาคนอื่น, ห้ามยกเลิกนัดหมายหากเหลือน้อยกว่า 24 ชม. | 02-Stakeholder, UC-01, UC-02, UC-04 |
| `ACT-02: อาจารย์ที่ปรึกษา (Advisor)` | จัดการเวลาว่าง อนุมัติคิว และบันทึกผลการให้คำปรึกษา | กำหนด Office Hours, ดูคำขอของนักศึกษาที่ขอนัดตนเอง, อนุมัติ/ปฏิเสธ/เสนอเลื่อนนัด, บันทึกผลหลังพบ, ยกเลิกนัดกรณีด่วน | ห้ามจัดการตารางเวลาหรือคำขอนัดหมายของอาจารย์ท่านอื่น | 02-Stakeholder, UC-03, UC-06 |
| `ACT-03: เจ้าหน้าที่ภาควิชา (Staff)` | ตรวจสอบภาพรวมและสนับสนุนการทำงานของภาควิชา | ดูสถิติการนัดหมายภาพรวม, ตรวจสอบการจับคู่อาจารย์และนักศึกษา, ตรวจสอบสถานะการเข้าพบ | ไม่สามารถกดอนุมัติหรือปฏิเสธคำขอแทนนายจ้าง/อาจารย์ได้ (เว้นแต่ได้รับมอบอำนาจพิเศษ) | 02-Stakeholder, FR-ADV-06 |
| `ACT-04: ผู้ดูแลระบบ IT (IT Admin)` | ควบคุมความปลอดภัย สิทธิ์ผู้ใช้งาน และระบบโครงสร้างพื้นฐาน | ดูแลการกำหนด Role & Permission Matrix, ดูแลระบบยืนยันตัวตน, จัดการ Audit Trail | ห้ามเข้าถึงรายละเอียดเหตุผลการเข้าพบที่เป็นเรื่องส่วนตัวของนักศึกษาโดยตรง | 02-Stakeholder, EP-04, NFR-ADV-01 |

### 2.3 Capabilities

| CAP | Capability | FR/BR/NFR/DR | US/UC/AC | Coverage |
|---|---|---|---|---|
| `CAP-01` | ตรวจสอบตารางเวลาว่าง (Availability Management) | FR-01, NFR-03, DR-02 | US-01, UC-01, AC-01, AC-02 | Detailed |
| `CAP-02` | สร้างและส่งคำขอนัดหมาย (Appointment Request Submission) | FR-02, FR-05, DR-03, DR-04 | US-02, UC-02, AC-03, AC-04, AC-05 | Detailed |
| `CAP-03` | พิจารณาคำขอนัดหมาย (Appointment Processing & Workflow) | FR-03, FR-05, BR-02, BR-03, DR-03 | US-03, UC-03, AC-06, AC-07, AC-08 | Detailed |
| `CAP-04` | จัดการการยกเลิกนัดหมาย (Cancellation Control) | BR-01, NFR-04, DR-03 | US-05, UC-04, AC-11, AC-12 | Detailed |
| `CAP-05` | ระบบแจ้งเตือนผู้ใช้งาน (Notification Service) | FR-04, DR-05 | US-04, UC-05, AC-09, AC-10 | Detailed |
| `CAP-06` | บันทึกสรุปผลและรายงานสถิติ (Consultation Records & Reporting) | FR-06, DR-03 | US-06, UC-06, AC-13 | Partial (Reporting Needs Follow-up) |
| `CAP-07` | ความปลอดภัยและการควบคุมสิทธิ์ (Security & Access Control) | NFR-01, DR-01 | Role & Permission Matrix | Partial (Matrix Detail Open) |

### 2.4 Constraints and Assumptions

| ID | Type | Statement | Source | Status/next action |
|---|---|---|---|---|
| `CT-01` | Technical / Scope | ขอบเขตการพัฒนาจำกัดอยู่ภายใน 1 ภาคการศึกษา และเป็นโครงงานเพื่อการศึกษา | 02-Scope, W04-Constraint | Confirmed |
| `CT-02` | Policy / Privacy | ไม่อนุญาตให้เชื่อมต่อระบบปฏิทินภายนอก (Google Calendar) เพื่อป้องกันความเสี่ยงด้าน Data Privacy | N-03, ISSUE-ADV-01 | Confirmed (Use internal calendar) |
| `CT-03` | Budget / Scope | ไม่อนุญาตให้ใช้บริการ SMS หรือ LINE API ที่มีค่าใช้จ่าย ให้ใช้ Email สถาบัน และ Web Notification เท่านั้น | N-02, ISSUE-ADV-02 | Confirmed |
| `AS-01` | Assumption | ผู้ใช้งานทุกคนสามารถเข้าถึงอินเทอร์เน็ต และมีบัญชีผู้ใช้งานของสถาบันที่ยืนยันตัวตนได้ | 01-Problem Brief (A-01), AS-01 | Confirmed |
| `AS-02` | Assumption | อาจารย์ที่ปรึกษามีการเข้ามาอัปเดตช่วงเวลาว่าง (Office Hours) ในระบบอย่างสม่ำเสมอ | 01-Problem Brief (A-02) | Confirmed |
| `AS-03` | Assumption | การนัดหมายแบบกลุ่ม ให้ตัวแทน 1 คนเป็นผู้ส่งคำขอและระบุชื่อสมาชิกที่เข้าร่วมในฟอร์ม | 01-Problem Brief (A-03), E-03 | Confirmed |

### 2.5 External Interfaces

| ID | System | Data/direction | Core/Extension | TBD/failure concern |
|---|---|---|---|---|
| `EXT-01` | Mock / Institution Identity Service (SSO) | ข้อมูลการยืนยันตัวตน, User ID, Role (Inbound) | Core | หากระบบล่ม ผู้ใช้จะไม่สามารถล็อกอินเข้าสู่ระบบได้ |
| `EXT-02` | Institution Mail Service (SMTP) | ข้อมูลการแจ้งเตือน, Email Address, หัวข้อและเนื้อหาข้อความ (Outbound) | Core | หากระบบส่งเมลล่ม ผู้ใช้ต้องยังสามารถดูแจ้งเตือนบน Web Notification ได้ |

---

## 3. Functional Requirements

| FR | Requirement | Source | Priority/admission | BR/NFR/DR | US/UC/AC | Status |
|---|---|---|---|---|---|---|
| `FR-01` | ระบบต้องแสดงช่วงเวลาว่าง (Office Hours) และสถานะพร้อมให้เข้าพบของอาจารย์ที่ปรึกษา เพื่อให้นักศึกษาสามารถเลือกวันและเวลาได้ | E-01, E-02, RC-01 | Must / Core | NFR-03, DR-02 | US-01, UC-01, AC-01, AC-02 | Ready |
| `FR-02` | ระบบต้องให้นักศึกษาส่งคำขอนัดหมาย โดยระบุวัตถุประสงค์ รายชื่อผู้เข้าพบ (เดี่ยว/กลุ่ม) และแนบไฟล์เอกสารประกอบได้ | E-03, RC-02 | Must / Core | NFR-02, DR-03, DR-04 | US-02, UC-02, AC-03, AC-04 | Partial (Required fields TBD) |
| `FR-03` | ระบบต้องให้อาจารย์ที่ปรึกษาสามารถอนุมัติ ปฏิเสธ หรือเสนอวันและเวลานัดหมายใหม่ (Reschedule) พร้อมระบุเหตุผลได้ | E-04, RC-03 | Must / Core | BR-02, BR-03, DR-03 | US-03, UC-03, AC-06, AC-07, AC-08 | Ready |
| `FR-04` | ระบบต้องส่งข้อความแจ้งเตือนเมื่อมีการสร้างคำขอใหม่หรือมีการเปลี่ยนแปลงสถานะคำขอนัดหมาย ผ่าน Email สถาบัน และ Web Notification | E-05, E-06, N-02, RC-04 | Should / Core | DR-05 | US-04, UC-05, AC-09, AC-10 | Ready |
| `FR-05` | ระบบต้องรองรับการเลือกรูปแบบการเข้าพบทั้งแบบ On-site (ระบุห้อง/สถานที่) และ Online (ให้อาจารย์แนบลิงก์การประชุม) | E-03, E-04, N-04, RC-06 | Should / Supporting | DR-03 | US-02, US-03, UC-02, UC-03, AC-05, AC-06 | Ready |
| `FR-06` | ระบบต้องรองรับการบันทึกสรุปผลการเข้าพบของอาจารย์ และจัดทำรายงานสถิติการนัดหมายภาพรวมของภาควิชา | E-08, RC-08 | Could / Extension | DR-03 | US-06, UC-06, AC-13 | Partial (Reporting Spec TBD) |

### Detailed Requirement Records

#### FR-01: การแสดงตารางเวลาว่างของอาจารย์ที่ปรึกษา
| Field | Value |
|---|---|
| Requirement ID | `FR-01` |
| Statement | ระบบต้องแสดงช่วงเวลาว่าง (Office Hours) และสถานะพร้อมให้เข้าพบของอาจารย์ที่ปรึกษา เพื่อให้นักศึกษาสามารถเลือกวันและเวลาสำหรับการนัดหมายได้ |
| Rationale/Goal | `G-01` / เพื่อให้นักศึกษาทราบเวลาว่างที่แน่นอน ลดการเสียเวลาเดินทางไปหาแล้วไม่พบอาจารย์ และป้องกันการจองเวลาซ้ำซ้อน |
| Source | E-01, E-02, RC-01 |
| Priority/Admission | Must / Core |
| Trigger | นักศึกษาเลือกอาจารย์ที่ปรึกษาที่ต้องการเข้าพบและเปิดหน้าตารางเวลา |
| Preconditions/guards | อาจารย์ที่ปรึกษาได้สร้างช่วงเวลาว่าง (TimeSlot) ไว้ในระบบ |
| Expected result | ปฏิทินแสดงช่วงเวลาที่ว่างและไม่ว่างอย่างชัดเจน และปรับปรุงสถานะทันทีเมื่อมีรายการจอง |
| BR/NFR/DR links | NFR-03, DR-02 |
| US/UC/AC links | US-01, UC-01, AC-01, AC-02 |
| Verification | Demo & Test: ทดสอบเข้าหน้าปฏิทินด้วยบัญชีนักศึกษา และตรวจสอบความถูกต้องของช่วงเวลาว่าง |
| Status/TBD | Ready |

#### FR-02: การส่งคำขอนัดหมายพร้อมเอกสาร
| Field | Value |
|---|---|
| Requirement ID | `FR-02` |
| Statement | ระบบต้องให้นักศึกษาส่งคำขอนัดหมาย โดยระบุวัตถุประสงค์ (เช่น ปรึกษาโครงงาน, ลงทะเบียน), ระบุรายชื่อผู้เข้าพบ และแนบไฟล์เอกสารประกอบได้ |
| Rationale/Goal | `G-01` / ให้อาจารย์มีข้อมูลเพียงพอสำหรับการพิจารณาและเตรียมตัวล่วงหน้าก่อนการเข้าพบ |
| Source | E-03, RC-02 |
| Priority/Admission | Must / Core |
| Trigger | นักศึกษาเลือกช่วงเวลาว่างและกดยืนยันส่งข้อมูลในฟอร์มคำขอนัดหมาย |
| Preconditions/guards | ช่วงเวลาที่เลือกต้องมีสถานะ "ว่าง" และผู้ใช้กรอก Required Fields ครบถ้วน |
| Expected result | บันทึกคำขอใหม่ในสถานะ "Pending" จัดเก็บไฟล์แนบ และสร้าง Event แจ้งเตือนไปยังอาจารย์ |
| BR/NFR/DR links | NFR-02, DR-03, DR-04 |
| US/UC/AC links | US-02, UC-02, AC-03, AC-04 |
| Verification | Test: ทดสอบกรอกฟอร์มทั้งแบบข้อมูลครบ ข้อมูลไม่ครบ และทดสอบอัปโหลดไฟล์ขนาดต่างๆ |
| Status/TBD | Partial (รอสรุปรายการ Required fields เพิ่มเติมตาม OQ-W05-01) |

#### FR-03: การพิจารณาคำขอนัดหมายโดยอาจารย์
| Field | Value |
|---|---|
| Requirement ID | `FR-03` |
| Statement | ระบบต้องให้อาจารย์ที่ปรึกษาสามารถอนุมัติ ปฏิเสธ หรือเสนอวันและเวลานัดหมายใหม่ (Reschedule) พร้อมระบุเหตุผลได้ |
| Rationale/Goal | `G-02` / ให้อาจารย์สามารถจัดระเบียบคิว บริหารจัดการเวลา และปรับเปลี่ยนเวลากรณีติดภารกิจด่วนได้ |
| Source | E-04, RC-03 |
| Priority/Admission | Must / Core |
| Trigger | อาจารย์ที่ปรึกษากดเลือกคำสั่ง อนุมัติ, ปฏิเสธ หรือเสนอเลื่อนเวลา ในหน้ารายการคำขอ |
| Preconditions/guards | คำขอนัดหมายต้องมีสถานะเป็น "Pending" (หากปฏิเสธหรือขอเลื่อน ต้องระบุเหตุผลตาม BR-02) |
| Expected result | สถานะคำขอเปลี่ยนเป็น "Confirmed", "Rejected" หรือ "Rescheduled" และส่งแจ้งเตือนให้นักศึกษา |
| BR/NFR/DR links | BR-02, BR-03, DR-03 |
| US/UC/AC links | US-03, UC-03, AC-06, AC-07, AC-08 |
| Verification | Test: ทดสอบการทำงานของทั้ง 3 คำสั่งและตรวจสอบการบันทึกเหตุผลและการเปลี่ยนสถานะของ TimeSlot |
| Status/TBD | Ready |

#### FR-04: การแจ้งเตือนสถานะการนัดหมาย
| Field | Value |
|---|---|
| Requirement ID | `FR-04` |
| Statement | ระบบต้องส่งข้อความแจ้งเตือนเมื่อมีการสร้างคำขอใหม่หรือมีการเปลี่ยนแปลงสถานะคำขอนัดหมาย ผ่าน Email สถาบัน และ Web Notification ภายในระบบ |
| Rationale/Goal | `G-03` / เพื่อให้ผู้ใช้งานทราบความคืบหน้าของนัดหมายได้อย่างรวดเร็วและแม่นยำ |
| Source | E-05, E-06, N-02, RC-04 |
| Priority/Admission | Should / Core |
| Trigger | มีการสร้างคำขอใหม่ หรือคำขอเปลี่ยนสถานะ (Confirmed, Rejected, Rescheduled, Cancelled) |
| Preconditions/guards | ผู้ใช้มีอีเมลสถาบันที่ถูกต้องบันทึกอยู่ในระบบ |
| Expected result | ส่งอีเมลแจ้งเตือน และสร้างรายการแจ้งเตือนบนแถบ Web Notification ภายในเวลา 1 นาที |
| BR/NFR/DR links | DR-05 |
| US/UC/AC links | US-04, UC-05, AC-09, AC-10 |
| Verification | Test: สร้างเหตุการณ์เปลี่ยนสถานะและตรวจสอบกล่องข้อความจำลองและกระดิ่งแจ้งเตือนบนเว็บ |
| Status/TBD | Ready |

#### FR-05: การรองรับรูปแบบเข้าพบ On-site และ Online
| Field | Value |
|---|---|
| Requirement ID | `FR-05` |
| Statement | ระบบต้องรองรับการเลือกรูปแบบการเข้าพบทั้งแบบ On-site (ระบุห้อง/สถานที่) และ Online โดยให้อาจารย์เป็นผู้แนบลิงก์การประชุม |
| Rationale/Goal | เพิ่มความยืดหยุ่นในการให้คำปรึกษากรณีมีข้อจำกัดด้านการเดินทางหรือเหตุสุดวิสัย |
| Source | E-03, E-04, N-04, RC-06 |
| Priority/Admission | Should / Supporting |
| Trigger | นักศึกษาเลือกตัวเลือกรูปแบบเข้าพบในฟอร์ม หรืออาจารย์ระบุลิงก์ขณะอนุมัติ |
| Preconditions/guards | หากเป็น Online อาจารย์ต้องแนบ URL ลิงก์ห้องประชุมที่ถูกต้องก่อนกดยืนยันอนุมัติ |
| Expected result | หน้ารายละเอียดการนัดหมายแสดงสถานที่ห้องพัก หรือลิงก์การประชุมที่กดเข้าห้องได้ |
| BR/NFR/DR links | DR-03 |
| US/UC/AC links | US-02, US-03, UC-02, UC-03, AC-05, AC-06 |
| Verification | Test & Inspection: ตรวจสอบการแสดงผลลิงก์ในหน้าจอนักศึกษาหลังคำขอได้รับการอนุมัติ |
| Status/TBD | Ready |

#### FR-06: การบันทึกสรุปผลและรายงานสถิติ
| Field | Value |
|---|---|
| Requirement ID | `FR-06` |
| Statement | ระบบต้องรองรับให้อาจารย์บันทึกสรุปผลหลังเสร็จสิ้นการเข้าพบ และจัดทำรายงานสถิติการนัดหมายภาพรวมของภาควิชา |
| Rationale/Goal | ช่วยให้มีประวัติติดตามความคืบหน้าของนักศึกษา และช่วยภาควิชาบริหารจัดการภาพรวม |
| Source | E-08, RC-08 |
| Priority/Admission | Could / Extension |
| Trigger | นัดหมายสิ้นสุดลง และอาจารย์กดบันทึกสรุปผล หรือเจ้าหน้าที่เปิดดูหน้ารายงาน |
| Preconditions/guards | คำขอนัดหมายต้องมีสถานะเป็น Confirmed และเลยกำหนดเวลานัดหมายแล้ว |
| Expected result | สถานะเปลี่ยนเป็น "Completed" บันทึกข้อความสรุปผล และอัปเดตสถิติภาพรวม |
| BR/NFR/DR links | DR-03 |
| US/UC/AC links | US-06, UC-06, AC-13 |
| Verification | Review & Demo: ตรวจสอบหน้าบันทึกสรุปผลและหน้าแสดงผลสถิติ |
| Status/TBD | Partial (รอรายละเอียดรูปแบบรายงานสถิติตาม OQ-W05-05) |

---

## 4. Business Rules

| BR | Rule | Authority/source | Affected FR/UC | Status |
|---|---|---|---|---|
| `BR-01` | **กฎการยกเลิก/เลื่อนนัดล่วงหน้า 24 ชั่วโมง:** นักศึกษาต้องแจ้งยกเลิกหรือขอเลื่อนนัดหมายล่วงหน้าอย่างน้อย 24 ชั่วโมงก่อนถึงเวลานัดหมาย หากเหลือน้อยกว่า 24 ชั่วโมง ระบบจะปิดกั้นการกดยกเลิกผ่านหน้าเว็บ และให้ติดต่ออาจารย์โดยตรง (ยกเว้นอาจารย์เป็นผู้กดยกเลิกเนื่องจากภารกิจด่วน) | N-01, C-01, BR-ADV-01 | FR-03, UC-04, AC-11, AC-12 | Confirmed for case |
| `BR-02` | **กฎการระบุเหตุผลประกอบ:** ทุกครั้งที่อาจารย์ที่ปรึกษากดปฏิเสธคำขอ (Reject) หรือเสนอขอเลื่อนเวลา (Reschedule) ระบบต้องบังคับให้กรอกข้อความระบุเหตุผลเสมอ | 02-Stakeholder, UC-03, AC-07, AC-08 | FR-03, UC-03 | Confirmed for case |
| `BR-03` | **กฎการล็อกและปลดล็อกช่วงเวลา (Slot Locking):** เมื่อคำขอได้รับการอนุมัติ (Confirmed) ระบบต้องล็อกช่วงเวลาดังกล่าวทันทีไม่ให้ผู้อื่นจองได้ และหากคำขอถูกปฏิเสธหรือยกเลิก ระบบต้องปลดล็อกช่วงเวลานั้นให้กลับมาว่างทันที | UC-03, UC-04, AC-06, AC-07, AC-11 | FR-01, FR-03, UC-03, UC-04 | Confirmed for case |

---

## 5. Non-functional Requirements

| NFR | Quality statement | Context/stimulus | Response/measure | Source | Verification | Status/TBD |
|---|---|---|---|---|---|---|
| `NFR-01` | ระบบต้องควบคุมการเข้าถึงข้อมูลตามบทบาท (Role-Based Access Control) เพื่อความปลอดภัยและความเป็นส่วนตัว | ผู้ใช้งานเรียกดูข้อมูลคำขอหรือประวัติการเข้าพบ | นักศึกษาเข้าถึงได้เฉพาะคำขอของตนเอง, อาจารย์ดูได้เฉพาะคำขอที่ส่งถึงตน, ข้อมูลเหตุผลส่วนตัวไม่รั่วไหล (100% RBAC Compliance) | E-08, NFR-ADV-01 | Test & Security Audit | Partial (รอ Role Matrix สมบูรณ์ตาม OQ-W05-04) |
| `NFR-02` | ระบบต้องออกแบบขั้นตอนการใช้งานให้สะดวก รวดเร็ว และเข้าใจง่าย | นักศึกษาทำการค้นหาเวลาว่างและสร้างคำขอนัดหมาย | นักศึกษาสามารถทำรายการเสร็จสิ้นได้ภายในไม่เกิน 4 หน้าจอ/ขั้นตอน | 01-Problem Brief, NFR-02 | Usability Test | Ready |
| `NFR-03` | ระบบต้องแสดงผลตารางเวลาและอัปเดตสถานะการนัดหมายอย่างรวดเร็ว | ผู้ใช้งานโหลดหน้าปฏิทินตารางเวลาว่างของอาจารย์ | หน้าจอต้องโหลดและแสดงผลเสร็จสมบูรณ์ภายในเวลาไม่เกิน 3 วินาที ในสภาวะเครือข่ายอินเทอร์เน็ตปกติ | 01-Problem Brief, NFR-03, AC-01 | Performance Test | Ready |
| `NFR-04` | ระบบต้องรักษาความถูกต้องและสอดคล้องของกฎการนัดหมาย (Data & Process Integrity) | นักศึกษาพยายามกดยกเลิกนัดหมายเมื่อเวลากระชั้นชิด | ระบบต้องตรวจสอบเวลาและปิดกั้นการยกเลิกนัดหมายที่เหลือน้อยกว่า 24 ชั่วโมงได้ถูกต้อง 100% | N-01, NFR-04, BR-ADV-01 | Automated Test | Ready |

---

## 6. Data Requirements

| DR | Concept | Requirement/minimum data | Relationships | Classification | Source | Status |
|---|---|---|---|---|---|---|
| `DR-01` | User Account | รหัสผู้ใช้, ชื่อ-นามสกุล, อีเมลสถาบัน, บทบาท (Student, Advisor, Staff, Admin) | 1 User มีได้ 1 AdvisorProfile หรือความสัมพันธ์กับ Appointment | Internal Identity | 02-Context, EXT-01 | Ready |
| `DR-02` | TimeSlot (ตารางเวลาว่าง) | รหัสช่วงเวลา, รหัสอาจารย์, วันที่, เวลาเริ่มต้น, เวลาสิ้นสุด, สถานะ (ว่าง, จองแล้ว, ปิดใช้งาน) | เป็นของ 1 AdvisorProfile, อ้างอิงโดย 0..1 AppointmentRequest | Operational Data | FR-01, E-02 | Ready |
| `DR-03` | AppointmentRequest (คำขอนัดหมาย) | รหัสคำขอ, รหัสผู้ขอ (นักศึกษา), รหัสอาจารย์, รหัสช่วงเวลา, หัวข้อ/วัตถุประสงค์, รูปแบบ (On-site/Online), ลิงก์ห้องประชุม/สถานที่, รายชื่อผู้เข้าร่วม, สถานะคำขอ (Pending, Confirmed, Rejected, Rescheduled, Cancelled, Completed), เหตุผลประกอบ, บันทึกสรุปผล | เชื่อมโยงกับ 1 User (Student), 1 User (Advisor), 1 TimeSlot, มีได้ 0..N Attachment | Confidential / PII | FR-02, FR-03, FR-05, FR-06 | Ready |
| `DR-04` | Attachment (ไฟล์แนบ) | รหัสไฟล์, รหัสคำขอ, ชื่อไฟล์เดิม, เส้นทางจัดเก็บ (File Path), ขนาดไฟล์, ประเภทไฟล์ (รองรับ `.pdf`, `.docx` ขนาด $\le$ 10MB) | ผูกกับ 1 AppointmentRequest | User Content | FR-02, AC-04 | Ready |
| `DR-05` | Notification (การแจ้งเตือน) | รหัสการแจ้งเตือน, รหัสผู้รับ, ข้อความแจ้งเตือน, ลิงก์ปลายทาง, สถานะการเปิดอ่าน, วันเวลาที่สร้าง | เชื่อมโยงกับ 1 User | Internal Log | FR-04, AC-09 | Ready |

---

## 7. Behavioral Model References

| Model | IDs/version | Requirement anchors | Coverage/gap | SRS use |
|---|---|---|---|---|
| User Stories | `US-01` ถึง `US-06` (Week 06) | FR-01 ถึง FR-06, BR-ADV-01 | ครอบคลุมผู้ใช้หลักครบถ้วน (Student, Advisor, Staff) | อ้างอิงในหัวข้อ 3 และตาราง Traceability |
| Use Cases | `UC-01` ถึง `UC-06` (Week 06) | FR-01 ถึง FR-06, BR-01 | มี Specification ละเอียดของ UC-02, UC-03, UC-04 | ใช้กำหนดขอบเขตกระบวนการทำงานและ Exception Flow |
| Acceptance Criteria | `AC-01` ถึง `AC-13` (Week 06) | NFR-03, NFR-04, FR-01..FR-06, BR-01..BR-03 | ครอบคลุมทุกเงื่อนไขเชิงพฤติกรรมในรูปแบบ Given-When-Then | ใช้เป็นเกณฑ์ในการทดสอบและตรวจรับ Requirement |

### 7.1 Lifecycle Rules (Appointment State Machine)

| From | Trigger | To | Guard/result | Source |
|---|---|---|---|---|
| `[None]` | นักศึกษากรอกข้อมูลและกดยืนยันส่งคำขอ | `Pending` | TimeSlot ต้องว่าง และข้อมูล Required ครบถ้วน (ส่ง Alert ให้อาจารย์) | UC-02, AC-03 |
| `Pending` | อาจารย์กดปุ่ม "อนุมัติ" (Approve) | `Confirmed` | TimeSlot ถูกล็อกไม่ให้ผู้อื่นจอง (ส่ง Alert ให้นักศึกษา) | UC-03, AC-06, BR-03 |
| `Pending` | อาจารย์กดปุ่ม "ปฏิเสธ" (Reject) | `Rejected` | ต้องระบุเหตุผล; TimeSlot ปลดล็อกกลับมาว่าง | UC-03, AC-07, BR-02 |
| `Pending` | อาจารย์กดปุ่ม "เสนอเลื่อนเวลา" (Reschedule) | `Rescheduled` | ต้องระบุเหตุผลและเลือกช่วงเวลาว่างใหม่ | UC-03, AC-08, BR-02 |
| `Confirmed` | นักศึกษากด "ขอยกเลิกนัดหมาย" | `Cancelled` | เวลาปัจจุบันต้องห่างจากเวลานัด $\ge$ 24 ชั่วโมง; TimeSlot ปลดล็อก | UC-04, AC-11, BR-01 |
| `Confirmed` | อาจารย์กดยกเลิกนัดหมายด่วน | `Cancelled` | อาจารย์ต้องระบุเหตุผลภารกิจด่วน; TimeSlot ปลดล็อก | UC-04, Alternate 1b |
| `Confirmed` | สิ้นสุดเวลานัด และอาจารย์บันทึกผลการพบ | `Completed` | เลยกำหนดเวลานัดหมายแล้ว | UC-06, AC-13 |

---

## 8. External Interface Requirements

| Interface | Requirement/data | Direction | Owner | Failure/privacy concern | Status |
|---|---|---|---|---|---|
| `EXT-01: Identity Service` | ตรวจสอบการเข้าสู่ระบบ, ดึง User ID, Role, ข้อมูลพื้นฐานนักศึกษา/อาจารย์ | Inbound | IT Admin / Dev Team | หากระบบล่ม ผู้ใช้จะไม่สามารถยืนยันตัวตนได้; ต้องจำกัดการดึงเฉพาะข้อมูลที่จำเป็น (Data Minimization) | Core / Partial (TBD Protocol) |
| `EXT-02: Mail Service` | รับคำสั่งส่งอีเมลแจ้งเตือน (Email, Subject, Body) ไปยังอีเมลสถาบัน | Outbound | IT Admin / Dev Team | เซิร์ฟเวอร์ส่งเมลอาจหน่วงหรือล่ม; ระบบต้องไม่ล่มตาม และต้องมี Web Notification สำรอง | Core / Ready |

---

## 9. Traceability and Coverage

| Source | W05 requirement | W06 model | SRS section | Verification | Coverage |
|---|---|---|---|---|---|
| E-01, E-02 | `FR-ADV-01` | US-01, UC-01, AC-01, AC-02 | 3 (FR-01) | Demo, Test | Covered |
| E-03 | `FR-ADV-02` | US-02, UC-02, AC-03, AC-04 | 3 (FR-02) | Test, Inspection | Partial (Fields TBD) |
| E-04 | `FR-ADV-03` | US-03, UC-03, AC-06..AC-08 | 3 (FR-03) | Test | Covered |
| E-05, E-06, N-02 | `FR-ADV-04` | US-04, UC-05, AC-09, AC-10 | 3 (FR-04) | Test | Covered |
| E-03, E-04, N-04 | `FR-ADV-05` | US-02, US-03, AC-05, AC-06 | 3 (FR-05) | Inspection | Covered |
| E-08 | `FR-ADV-06` | US-06, UC-06, AC-13 | 3 (FR-06) | Demo, Review | Partial (Report TBD) |
| C-01, N-01 | `BR-ADV-01` | US-05, UC-04, AC-11, AC-12 | 4 (BR-01) | Automated Test | Covered |
| E-08 | `NFR-ADV-01` | Quality Scenario | 5 (NFR-01) | Security Audit | Partial (Matrix TBD) |
| 01-Problem Brief | `NFR-02` | - | 5 (NFR-02) | Usability Test | Covered |
| 01-Problem Brief | `NFR-03` | AC-01 | 5 (NFR-03) | Performance Test | Covered |
| N-01 | `NFR-04` | AC-12 | 5 (NFR-04) | Automated Test | Covered |

---

## 10. Open Issues

| OI | Question/TBD | Affected IDs | Owner | Next action | Expected evidence | Needed by |
|---|---|---|---|---|---|---|
| `OI-01` | ข้อมูล Required Fields ขั้นต่ำในฟอร์มขอนัดหมาย และขีดจำกัดประเภทไฟล์แนบเพิ่มเติม (OQ-W05-01) | FR-02, DR-04, UC-02 | อาจารย์ที่ปรึกษา / เจ้าหน้าที่ | สัมภาษณ์ตัวแทนอาจารย์ | ตารางรายการฟิลด์บังคับที่ผ่านการยืนยัน | Sprint 1 Design |
| `OI-02` | แนวทางข้อยกเว้นสำหรับกฎ 24 ชม. กรณีเกิดเหตุสุดวิสัยร้ายแรง เช่น ป่วยกะทันหัน (OQ-W05-02) | BR-01, UC-04 | งานกิจการนักศึกษา / อาจารย์ | ขอคำปรึกษาคณะ/ภาควิชา | ประกาศแนวปฏิบัติกรณียกเว้น | Sprint 2 Dev |
| `OI-03` | ความถี่ในการส่งอีเมลสรุปคำขอนัดหมายประจำวันให้อาจารย์ (OQ-W05-03) | FR-04, EXT-02 | อาจารย์ที่ปรึกษา / IT Admin | สอบถามความต้องการอาจารย์ | มติข้อตกลงรอบเวลาส่งเมล | Sprint 1 Dev |
| `OI-04` | ตาราง Role & Permission Matrix ฉบับสมบูรณ์ (OQ-W05-04) | NFR-01, ACT-01..04 | IT Admin / เจ้าหน้าที่ | ประสานงาน IT Admin | ตารางสิทธิ์ Read/Write/Approve | Sprint 1 Design |
| `OI-05` | รูปแบบรายงานสถิติการเข้าพบที่ภาควิชาต้องการนำไปใช้งานจริง (OQ-W05-05) | FR-06, ACT-03 | หัวหน้าภาควิชา / เจ้าหน้าที่ | เก็บตัวอย่างฟอร์มรายงานเดิม | Mockup และฟิลด์ของรายงาน | Sprint 2 Dev |

---

## 11. Verification Plan

| VF | Method | Target IDs | Procedure/evidence | Owner | Status |
|---|---|---|---|---|---|
| `VF-01` | Inspection & Test | FR-01, NFR-03, AC-01 | ทดสอบการโหลดหน้าปฏิทินเวลาว่างของอาจารย์ จับเวลาโหลดข้อมูล และตรวจความถูกต้องของสถานะ TimeSlot | Dev Team / Tester | Planned |
| `VF-02` | Test | FR-02, AC-03, AC-04 | ทดสอบกรอกฟอร์มขอนัดหมาย อัปโหลดไฟล์ `.pdf`, `.docx` ขนาดไม่เกิน 10MB และทดสอบอัปโหลดไฟล์เกินขนาด | Tester | Planned |
| `VF-03` | Test | FR-03, BR-02, BR-03, AC-06..08 | ทดสอบฟังก์ชัน อนุมัติ ปฏิเสธ และขอเลื่อนเวลา ตรวจสอบว่าระบบบังคับกรอกเหตุผล และตรวจการล็อก TimeSlot | Tester | Planned |
| `VF-04` | Automated Test | BR-01, NFR-04, AC-11, AC-12 | เขียน Test Script จำลองการยกเลิกนัดหมายที่ $> 24$ ชั่วโมง (ต้องสำเร็จ) และ $< 24$ ชั่วโมง (ต้องถูกบล็อก) | Dev Team | Planned |
| `VF-05` | Test | FR-04, EXT-02, AC-09, AC-10 | ทดสอบเปลี่ยนสถานะคำขอ แล้วจับเวลาการส่ง Email จำลอง และตรวจการแสดงผลบนกระดิ่ง Web Notification | Tester | Planned |
| `VF-06` | Security Audit | NFR-01, ACT-01..04 | ทดสอบสิทธิ์การเข้าถึง URL และ API ข้ามผู้ใช้ (เช่น นักศึกษาพยายามเปิดดูคำขอของผู้อื่น) | Security / IT Admin | Planned |

---

## 12. Review Gate

- [x] W05 FR/BR/NFR/DR ทุกข้อมี disposition
- [x] W06 US/UC/AC ย้อนกลับ W05 ได้
- [x] Partial/Extension/TBD มองเห็นและถูกระบุสถานะชัดเจน
- [x] Open Issue ทุกข้อมี owner/action/evidence ครบถ้วน
- [x] Status เป็น Baseline Candidate

---

## Appendix A — Requirement Disposition

| Backlog ID | Included/Deferred/Extension/Issue | SRS section | Reason |
|---|---|---|---|
| `FR-ADV-01` | Included (Core) | 3 (FR-01) | เป็นหัวใจหลักในการแก้ปัญหาการเดินไปหาแล้วไม่พบอาจารย์ |
| `FR-ADV-02` | Included (Core) | 3 (FR-02) | ฟังก์ชันหลักในการสร้างคำขอนัดหมาย |
| `FR-ADV-03` | Included (Core) | 3 (FR-03) | ฟังก์ชันหลักของอาจารย์ในการบริหารจัดการคิว |
| `FR-ADV-04` | Included (Core) | 3 (FR-04) | แจ้งเตือนผ่านอีเมลและเว็บเพื่อลดความผิดพลาด |
| `FR-ADV-05` | Included (Supporting) | 3 (FR-05) | เพิ่มความยืดหยุ่นในการเลือก On-site/Online |
| `FR-ADV-06` | Included (Extension) | 3 (FR-06) | ระบบรายงานสถิติเป็นฟังก์ชันเสริมสำหรับภาควิชา |
| `BR-ADV-01` | Included (Core) | 4 (BR-01) | กฎการยกเลิกล่วงหน้า 24 ชม. เพื่อความเป็นธรรม |
| `NFR-ADV-01` | Included (Core) | 5 (NFR-01) | การรักษาความลับของข้อมูลการปรึกษา |
| `ISSUE-ADV-01` | Deferred / Hold | 1.3 (Scope), 10 | เสี่ยงต่อ Data Privacy และขัดนโยบาย IT สถาบัน (Google Calendar Sync) |
| `ISSUE-ADV-02` | Out of Scope / Hold | 1.3 (Scope) | ค่าใช้จ่ายและความซับซ้อน API ภายนอกเกินขอบเขตโครงงาน (LINE Notify) |
| `ISSUE-ADV-03` | Deferred / Hold | 1.3 (Scope), 10 | ยังไม่มีนโยบายอย่างเป็นทางการจากภาควิชา (No-show Penalty) |
| `ISSUE-ADV-04` | Deferred / Hold | 1.3 (Scope) | อาจารย์ต้องการตรวจสอบข้อมูลด้วยตนเองทุกครั้ง (Auto-approval) |

---

## Appendix B — Review and Revision

| Item | Before | After | Reason/source | Reviewer |
|---|---|---|---|---|
| Notification Channel | ต้องการใช้ LINE Notify / LINE OA | ปรับเป็น Email สถาบัน + Web Notification | ผลการเจรจาต่อรอง N-02 / C-02 เพื่อคุม Scope และค่าใช้จ่าย | IT Admin / Dev Team |
| Calendar Sync | ต้องการ Sync ข้อมูลกับ Google Calendar | ใช้ระบบปฏิทินภายในระบบจำลองเท่านั้น | ผลการเจรจาต่อรอง N-03 / C-03 ติดเรื่องความปลอดภัยและนโยบาย IT | IT Admin |
| Meeting Link | เสนอให้เชื่อมต่อ Auto-generate Link Zoom/Teams | ให้อาจารย์เป็นผู้แนบลิงก์ Manual ในฟอร์ม | ผลการเจรจาต่อรอง N-04 / C-04 ลดความซับซ้อนการผูก API องค์กร | Dev Team |
| Cancellation Rule | นักศึกษาต้องการยกเลิกได้ตลอดเวลา | บังคับยกเลิกล่วงหน้า $\ge$ 24 ชั่วโมง | ผลการเจรจาต่อรอง N-01 / C-01 เพื่อป้องกันอาจารย์เสียเวลาทำงาน | อาจารย์ที่ปรึกษา |

---

## Appendix C — AI Use Disclosure

| Activity | AI assistance | Human verification/change | Evidence |
|---|---|---|---|
| สรุปสังเคราะห์เอกสาร Week 01–06 สู่โครงสร้าง SRS | ช่วยจัดหมวดหมู่ข้อมูล, ร่างข้อความ SRS และทำตาราง Traceability Matrix | ตรวจทานความถูกต้องของ ID, ตรวจสอบการคงความหมายของ Business Rules และตรวจสอบขอบเขต In/Out Scope | เอกสารส่งมอบ Week 01 ถึง Week 06 ใน Repository |
| การจัดทำ Lifecycle Rules และ Verification Plan | ช่วยเรียบเรียง State Transition และร่างตารางการทดสอบ | ปรับแก้เงื่อนไข Guard และกำหนดวิธีการทดสอบให้สอดคล้องกับขอบเขตการจำลองของวิชา ENGSE206 | 06-requirement-models.md และ 07-srs-v1_2.md |