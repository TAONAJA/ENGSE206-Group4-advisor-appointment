# 10 — Design Strategy and Rationale

> **Week 10 deliverable**  
> **โครงการ:** ระบบนัดหมายเข้าพบอาจารย์ที่ปรึกษา (Advisor Appointment System)  
> **ทีม:** ENGSE206 Group 4 | **เวอร์ชัน:** 1.0 (Draft for Week 10) | **วันที่:** 23/10/2026  
> **เอกสารอ้างอิงหลัก:** [07-srs-v1.md](../docs/07-srs-v1.md), [05-requirement-backlog.md](../docs/05-requirement-backlog.md), [06-requirement-models.md](../docs/06-requirement-models.md), [decision-log.md](../project-management/decision-log.md)

---

## 1. Design Goals

การแปลง Functional Requirements (FR) และ Non-Functional Requirements (NFR) จากเอกสาร [07-srs-v1.md](../docs/07-srs-v1.md) ให้เป็นเป้าหมายและแนวทางการออกแบบเชิงระบบ (Design Goals):

| Goal | Related Requirement | Design Implication |
|---|---|---|
| **DG-01: การค้นหาเวลาว่างและการส่งคำขอนัดหมายที่สะดวกรวดเร็ว (Frictionless Availability Search & Appointment Booking)** | FR-01, FR-02, NFR-01 (RC-01, RC-02) | ออกแบบอินเทอร์เฟซค้นหาช่วงเวลาว่าง (Office Hours) ของอาจารย์ที่แสดงสถานะเรียลไทม์ และแบบฟอร์มส่งคำขอนัดหมายในหน้าเดียวแบบลดขั้นตอน (≤ 3 ขั้นตอน) พร้อมตัวเลือกวัตถุประสงค์ รูปแบบการเข้าพบ (On-site / Online) สมาชิกผู้เข้าร่วม และระบบอัปโหลดไฟล์เอกสารประกอบ (รองรับ `.pdf`, `.docx` ขนาดไม่เกิน 10MB) |
| **DG-02: ความโปร่งใสและการติดตามสถานะคำขออย่างต่อเนื่อง (End-to-End Status Tracking & Notification)** | FR-03, FR-04, NFR-02 (RC-03, RC-04, RC-06) | ออกแบบสถานะวงจรชีวิตของคำขอนัดหมายให้ชัดเจน (`Pending` → `Approved` / `Rejected` / `Rescheduled` → `Completed` / `Cancelled`), จัดทำ Dashboard สำหรับติดตามคำขอ และพัฒนาระบบ Event-driven Notification เพื่อส่งการแจ้งเตือนผ่าน Email สถาบัน และ Web Notification ทันทีเมื่ออาจารย์เปลี่ยนสถานะคำขอ |
| **DG-03: การบริหารจัดการตารางเวลาและการพิจารณาคำขอของอาจารย์อย่างมีประสิทธิภาพ (Effective Schedule Management & Review Workflow)** | FR-01, FR-03, BR-01 (RC-01, RC-03) | ออกแบบ Advisor Management Console สำหรับอาจารย์ที่ปรึกษา ให้สามารถตั้งค่าและปรับเปลี่ยน Office Hours, พิจารณาอนุมัติ ปฏิเสธ (บังคับระบุเหตุผล) หรือขอเลื่อนนัดหมาย (Reschedule) พร้อมการควบคุม State Transition ไม่ให้อนุญาตการยกเลิกนัดหมายล่วงหน้าน้อยกว่า 24 ชั่วโมง (BR-01) |
| **DG-04: การควบคุมความปลอดภัยและการคุ้มครองข้อมูลการเข้าพบ (Security, RBAC & Data Privacy)** | NFR-03, BR-04 (RC-07) | บังคับใช้ Role-Based Access Control (RBAC) เพื่อแยกสิทธิ์อย่างเด็ดขาดระหว่าง นักศึกษา (Student), อาจารย์ที่ปรึกษา (Advisor) และผู้ดูแลระบบ (Admin) คุ้มครองข้อมูลบันทึกการให้คำปรึกษา และออกแบบระบบบันทึกประวัติการเปลี่ยนสถานะ (Audit Trail) แบบ Append-only ป้องกันการแก้ไขย้อนหลัง |
| **DG-05: ประสิทธิภาพการตอบสนองและการเชื่อมต่อระบบอย่างมีเสถียรภาพ (High Performance & Integration Reliability)** | NFR-02, EXT-01, EXT-02, EXT-03 | ออกแบบระบบให้ตอบสนองคำขอทั่วไปภายใน ≤ 2–3 วินาที (และส่งแจ้งเตือนสำเร็จภายใน ≤ 1 นาที), เชื่อมต่อระบบยืนยันตัวตนสถาบัน (EXT-01) และแยกการจัดเก็บไฟล์แนบประกอบคำขอไปยัง Dedicated File Storage (EXT-03) พร้อมประมวลผลการแจ้งเตือนแบบ Asynchronous Background Task (EXT-02) |

---

## 2. Design Principles

หลักการออกแบบที่ทีมยึดถือในการตัดสินใจด้าน Architecture, Data และ UX/UI:

1. **Simplicity & Low Friction (ความเรียบง่ายและลดภาระผู้ใช้งาน):**  
   นักศึกษาต้องสามารถตรวจสอบตารางเวลาว่างของอาจารย์และส่งคำขอนัดหมายได้รวดเร็วภายในไม่เกิน 3 ขั้นตอน ใช้ตัวเลือกแบบ Dropdown/Radio สำหรับระบุหัวข้อ วัตถุประสงค์ และรูปแบบการเข้าพบ เพื่อลดข้อผิดพลาดจากการพิมพ์
2. **Transparency & Real-time Feedback Loop (ความโปร่งใสและการแจ้งเตือนที่ทันท่วงที):**  
   คำขอนัดหมายทุกรายการต้องมีหมายเลขอ้างอิง (Appointment ID) ผู้ใช้สามารถติดตามสถานะและเหตุผลประกอบการพิจารณาของอาจารย์ได้ตลอดเวลา โดยระบบจะส่งการแจ้งเตือนผ่าน Email สถาบัน และ Web Notification ทันทีเมื่อเกิดการเปลี่ยนแปลงสถานะ
3. **Role-Based Separation of Concerns & Data Privacy (การแบ่งแยกสิทธิ์และคุ้มครองความเป็นส่วนตัว):**  
   จัดสรรการเข้าถึงฟังก์ชันและข้อมูลตามบทบาท (`Student`, `Advisor`, `Admin`) อย่างเคร่งครัด โดยข้อมูลประวัติการขอคำปรึกษาและเอกสารแนบจะถูกจำกัดสิทธิ์ให้เห็นเฉพาะนักศึกษาผู้ขอและอาจารย์ที่ปรึกษาที่เกี่ยวข้องเท่านั้น
4. **Schedule Integrity & Immutability of Records (ความถูกต้องของตารางนัดหมายและการคงรูปของประวัติ):**  
   ตารางนัดหมายต้องป้องกันการจองซ้อนทับ (Double Booking) และบันทึกประวัติการเปลี่ยนสถานะ (Status History / Audit Log) ต้องเป็นแบบ Append-only (ห้ามแก้ไขหรือลบ) เพื่อความโปร่งใสและตรวจสอบย้อนหลังได้
5. **Progressive Disclosure & Proactive Validation (การทยอยแสดงผลและการดักจับข้อผิดพลาดเชิงรุก):**  
   แสดงข้อมูลที่จำเป็นตามลำดับขั้นตอน และทำการตรวจจับข้อผิดพลาดตั้งแต่ฝั่ง Client (เช่น ตรวจสอบชนิดและขนาดไฟล์แนบ ตรวจสอบการเลือกช่วงเวลาว่าง) ก่อนส่งข้อมูลไปยังเซิร์ฟเวอร์
6. **Cross-Platform Accessibility & Responsive Design (การเข้าถึงได้ง่ายผ่านทุกอุปกรณ์):**  
   ออกแบบอินเทอร์เฟซให้รองรับการใช้งานบนอุปกรณ์หลากหลาย (Responsive Web) ทั้งสมาร์ตโฟน แท็บเล็ต และคอมพิวเตอร์ เพื่อให้นักศึกษาและอาจารย์สามารถใช้งานได้สะดวกทุกที่ทุกเวลา

---

## 3. Candidate Strategies / Alternatives

การเปรียบเทียบทางเลือกในการออกแบบ สถาปัตยกรรม และเทคโนโลยี พร้อมเหตุผลและ Trade-offs ที่เกิดขึ้น:

| Decision Area | Option A | Option B | Selected Option | Rationale | Trade-off |
|---|---|---|---|---|---|
| **Client Platform Architecture (รูปแบบแพลตฟอร์มฝั่งผู้ใช้งาน)** | **Native Mobile App** (iOS / Android) | **Responsive Web App** (Mobile-first Web Application) | **Option B: Responsive Web App** | นักศึกษาและอาจารย์ต้องการเข้าถึงระบบได้ทันทีจากทุกอุปกรณ์โดยไม่ต้องติดตั้งแอปพลิเคชันเพิ่มเติม รองรับการใช้งานผ่านเว็บเบราว์เซอร์ของมหาวิทยาลัย สอดคล้องกับ NFR-01 และลดความซับซ้อนในการบำรุงรักษา | ไม่สามารถใช้งานฟังก์ชันระดับระบบปฏิบัติการของสมาร์ตโฟนได้เต็มรูปแบบ เช่น Native Push Notifications แต่แก้ปัญหาด้วย Email และ Web Notification ได้ |
| **User Authentication & Identity Strategy (การยืนยันตัวตนและจัดการสิทธิ์)** | **Local User Account System** (สร้างระบบสมัครสมาชิกและรหัสผ่านใหม่) | **University Identity Service / Single Sign-On** (เชื่อมต่อระบบยืนยันตัวตนกลางของสถาบัน - EXT-01) | **Option B: University Identity Service (SSO)** | ใช้ประโยชน์จากฐานข้อมูลบัญชีนักศึกษาและอาจารย์ที่มีอยู่แล้ว ป้องกันบุคคลภายนอกแอบอ้าง ยืนยันตัวตนน่าเชื่อถือ และสามารถดึงข้อมูลสถานะ/บทบาทเพื่อนำมาผูกกับสิทธิ์ RBAC ได้ทันที (NFR-03) | มี External Dependency กับระบบ Identity ของสถาบัน หากระบบสถาบันขัดข้องจะเข้าสู่ระบบไม่ได้ จึงต้องมี Error Handling และ Session Timeout ที่รัดกุม |
| **Attachment & Document Storage Strategy (การจัดเก็บไฟล์เอกสารประกอบคำขอ)** | **Database BLOB / Base64** (จัดเก็บไฟล์ลงในตารางฐานข้อมูลหลักโดยตรง) | **Dedicated File / Object Storage** (แยกจัดเก็บไฟล์บน Storage แล้วเก็บ URL/Path ในฐานข้อมูลหลัก - EXT-03) | **Option B: Dedicated File Storage + Relational DB Metadata** | เอกสารประกอบการขอคำปรึกษา (`.pdf`, `.docx`) มีขนาดใหญ่หากเก็บในฐานข้อมูลหลักจะทำให้ Database Bloat และประสิทธิภาพการ Search/Query ลดลง การแยกเก็บไฟล์และอ้างอิง URL ช่วยรักษา Performance ของระบบ (NFR-02) | เพิ่มจุดจัดเก็บข้อมูลเป็น 2 ส่วน (DB + Storage) ต้องมีกลไกตรวจสอบ Transaction เพื่อป้องกันไฟล์กำพร้า (Orphaned Files) หากการบันทึกคำขอล้มเหลว |
| **Notification Delivery Mechanism (กลไกการส่งสัญญาณแจ้งเตือน)** | **Client Polling** (ให้หน้าเว็บส่ง Request สอบถามสถานะใหม่เป็นระยะๆ) | **Event-Driven Notification Service** (ส่งการแจ้งเตือนอัตโนมัติเมื่อเกิด Event การเปลี่ยนสถานะ - EXT-02) | **Option B: Event-Driven Notification Service** | การตอบรับ/ปฏิเสธนัดหมายเกิดขึ้นเป็นรายเหตุการณ์ (Event-based) การใช้ Event-driven Service ทำให้ส่ง Email สถาบัน และ Web Notification หาผู้ใช้ได้ทันทีเมื่อสถานะเปลี่ยน (FR-04) และประหยัด Bandwidth ของเซิร์ฟเวอร์ | มีความซับซ้อนในการพัฒนาระบบ Asynchronous Event / Queue มากกว่าการเขียน Client Polling แบบพื้นฐาน |
| **Workflow Rules & Audit Logging Strategy (การจัดการกฎการนัดหมายและประวัติ)** | **In-place Status Update** (อัปเดตสถานะทับในตารางคำขอนัดหมายโดยตรง) | **Finite State Machine (FSM) + Append-Only Audit Log** (ควบคุมสถานะด้วย FSM และบันทึกประวัติลงตาราง Log แยก) | **Option B: Finite State Machine + Append-Only Audit Log** | ช่วยบังคับใช้กฎทางธุรกิจ เช่น ห้ามยกเลิกล่วงหน้าน้อยกว่า 24 ชม. (BR-01) และบังคับระบุเหตุผลเมื่อปฏิเสธ/ขอเลื่อน ตาราง Log แบบ Append-only ช่วยให้ตรวจสอบประวัติย้อนหลังได้โดยไม่ถูกแก้ไข (BR-04, NFR-03) | เพิ่มปริมาณการเขียนข้อมูลลงหลายตารางใน 1 Transaction และต้องจัดการดึงข้อมูล History มาแสดงผลให้มีประสิทธิภาพ |

---

## 4. Quality Attribute Tactics

การนำแท็กติกเชิงสถาปัตยกรรม (Architecture Tactics) มาใช้เพื่อตอบสนองต่อ Non-Functional Requirements (NFR) ของระบบ:

| Quality Attribute | Tactic | Related NFR | Evidence in Design |
|---|---|---|---|
| **Usability (ความสะดวกในการใช้งาน)** | **Minimize Steps & Cognitive Load:** รวมขั้นตอนการส่งคำขอนัดหมายไว้ในฟอร์มหน้าเดียว เลือกอาจารย์/ช่วงเวลาว่าง/วัตถุประสงค์ผ่าน Dropdown และแสดงระบบ Preview ชื่อและขนาดไฟล์แนบก่อนส่ง | NFR-01 (ส่งคำขอสำเร็จภายใน ≤ 3 ขั้นตอน) | Wireframe หน้าขอจองนัดหมาย (Booking UI), Client-side Validation Logic, Sequence Diagram การส่งคำขอ |
| **Performance (ประสิทธิภาพการตอบสนอง)** | **Resource Separation & Indexing Scheme:** แยกการเก็บไฟล์แนบไว้ที่ Dedicated File Storage (EXT-03), ทำ Indexing บนฟิลด์ที่ใช้ค้นหาบ่อย (`AdvisorId`, `StudentId`, `Status`, `AppointmentDate`) ในฐานข้อมูล และส่ง Notification แบบ Background Task | NFR-02 (ระบบตอบสนองผลลัพธ์ภายใน ≤ 2–3 วินาที และส่งแจ้งเตือนภายใน ≤ 1 นาที) | Database Indexing Scheme, Asynchronous Notification Service Architecture |
| **Security & Access Control (ความปลอดภัยและการควบคุมสิทธิ์)** | **Role-Based Access Control (RBAC) & Data Isolation:** ตรวจสอบสิทธิ์ผ่าน Authorization Middleware โดยแยกสิทธิ์ของ Student, Advisor และ Admin อย่างเด็ดขาด ป้องกันการเข้าถึงข้อมูลคำขอนัดหมายข้ามบุคคล | NFR-03 (ควบคุมสิทธิ์การเข้าถึงตามบทบาท) | RBAC Permission Matrix, Data Model (`User.role`), API Route Guard Architecture |
| **Auditability & Data Integrity (ความสามารถในการตรวจสอบและความคงรูปของข้อมูล)** | **Immutable / Append-Only Audit Trail:** ตาราง `AppointmentHistory` และ `AuditLog` รองรับเฉพาะคำสั่ง `INSERT` ไม่อนุญาตคำสั่ง `UPDATE` หรือ `DELETE` บันทึกทุกการเปลี่ยนสถานะ ผู้ดำเนินการ และเวลาอย่างแม่นยำ | NFR-03, BR-04 | Data Model (`AppointmentHistory`), Database Trigger / Application Log Service Logic |
| **Modifiability & Extensibility (ความยืดหยุ่นและการบำรุงรักษา)** | **Separation of Concerns & Interface Segregation:** ออกแบบระบบแบบ Layered Architecture (Presentation, Service, Data Access) และเชื่อมต่อระบบภายนอก (SSO, Notification, Storage) ผ่าน Service Interface | NFR-03, EXT-01..03 | Conceptual Architecture Diagram (Week 11), Module Dependency Diagram |

---

## 5. Architecture / UX Constraints

ข้อจำกัดด้านสถาปัตยกรรม ประสบการณ์ผู้ใช้งาน และขอบเขตของระบบที่ต้องนำมาเป็นกรอบในการออกแบบ:

1. **Business Data & Booking Constraints (ข้อจำกัดด้านข้อมูลและการจอง - BR-01):**  
   - การส่งคำขอนัดหมายต้องระบุข้อมูลสำคัญครบถ้วน (อาจารย์ผู้รับการขอเข้าพบ, วันเวลา, วัตถุประสงค์, รูปแบบ On-site/Online) และการยกเลิก/เลื่อนนัดหมายผ่านระบบต้องทำล่วงหน้าไม่น้อยกว่า 24 ชั่วโมง
2. **Role & Permission Constraints (ข้อจำกัดด้านสิทธิ์การเข้าถึง - NFR-03):**  
   - ระบบต้องจำกัดการเข้าถึงข้อมูลตามบทบาท (RBAC) โดยนักศึกษาดูได้เฉพาะคำขอของตนเอง อาจารย์ดูและจัดการได้เฉพาะคำขอที่ส่งถึงตนเอง และผู้ดูแลระบบเท่านั้นที่จัดการข้อมูลพื้นฐานของระบบได้
3. **Workflow State Guard Constraints (ข้อจำกัดการเปลี่ยนผ่านสถานะ - FR-03):**  
   - การเปลี่ยนสถานะเป็น `Rejected` หรือ `Rescheduled` บังคับให้อาจารย์ต้องกรอกข้อความระบุเหตุผลหรือข้อเสนอแนะในระบบก่อนเสมอ เพื่อความโปร่งใสและแจ้งให้นักศึกษาทราบ
4. **Audit Immutability Constraints (ข้อจำกัดด้านการคงรูปของประวัติย้อนหลัง - BR-04):**  
   - บันทึกประวัติการเปลี่ยนสถานะคำขอและ Audit Log ต้องสร้างขึ้นโดยอัตโนมัติจากระบบ และห้ามไม่ให้ผู้ใช้งานทุกกลุ่ม (รวมถึง Admin) แก้ไข หรือลบข้อมูลประวัติต่างๆ ได้
5. **Interaction & Platform Constraints (ข้อจำกัดด้านการใช้งานและแพลตฟอร์ม - NFR-01):**  
   - การส่งคำขอนัดหมายต้องเสร็จสิ้นภายในไม่เกิน 3 ขั้นตอน รองรับการแสดงผลแบบ Responsive Web Browser ทั้งบนสมาร์ตโฟนและคอมพิวเตอร์ผ่านเครือข่ายของสถาบัน
6. **System Scope Boundary Constraints (ข้อจำกัดขอบเขตของระบบ):**  
   - อ้างอิงตาม [00-project-profile.md](../docs/00-project-profile.md) และ [07-srs-v1.md](../docs/07-srs-v1.md) ระบบจะไม่ครอบคลุม:
     - การเชื่อมต่อปฏิทินภายนอกแบบ Two-way Sync กับ Google Calendar (Hold ตามนโยบาย Data Privacy)
     - การแจ้งเตือนผ่าน LINE Notify หรือ Mobile Push Notification
     - ระบบยื่นใบลาป่วย/ลากิจอย่างเป็นทางการ และการนัดหมายข้ามคณะ/สถาบัน
7. **External System Integration Constraints (ข้อจำกัดการเชื่อมต่อระบบภายนอก):**  
   - ระบบต้องพร้อมเชื่อมต่อกับระบบภายนอก 3 ส่วนหลัก:
     - **EXT-01 (University Identity Service / SSO):** สำหรับตรวจสอบและยืนยันตัวตนผู้ใช้
     - **EXT-02 (Institutional Email / Web Notification Service):** สำหรับส่งสัญญาณแจ้งเตือนเปลี่ยนสถานะคำขอ
     - **EXT-03 (Document / Object Storage Service):** สำหรับอัปโหลดและจัดเก็บไฟล์เอกสารประกอบการขอเข้าพบ

---

## 6. Design Decisions to Record

การตัดสินใจสำคัญเชิงสถาปัตยกรรมและการออกแบบที่บันทึกไว้ใน [project-management/decision-log.md](../project-management/decision-log.md):

| Decision ID | Date | Decision Summary | Selected Option | Rationale | Impacted Artefacts | Owner |
|---|---|---|---|---|---|---|
| **D-01** | 18/08/2026 | ปรับลดขอบเขตการเชื่อมต่อ Google Calendar สองทาง (Two-Way Sync) | Option B: ใช้ระบบตารางเวลาภายในระบบ (Internal Calendar) | ติดข้อจำกัดด้านนโยบาย Data Privacy และข้อจำกัดทางเทคนิค OAuth ของสถาบัน จึงปรับเป็น Provisional/Hold | [05-requirement-backlog.md](../docs/05-requirement-backlog.md), [08-validation-traceability.md](../docs/08-validation-traceability.md) | จิราพัชร อินจันทร์ |
| **D-02** | 23/09/2026 | เลือกสถาปัตยกรรม Client ฝั่งผู้ใช้เป็น Responsive Web Application | Option B: Responsive Web Application | ลดอุปสรรคในการใช้งาน ผู้ใช้สามารถเข้าใช้งานผ่านเบราว์เซอร์ได้ทันทีโดยไม่ต้องติดตั้งแอปพลิเคชัน สอดคล้องกับ NFR-01 | [10-design-strategy.md](10-design-strategy.md), [11-conceptual-architecture.md](11-conceptual-architecture.md) | จักรพงศ์ หมื่นไชยศรี |
| **D-03** | 23/09/2026 | เชื่อมต่อระบบยืนยันตัวตนกลางของสถาบัน (SSO) | Option B: University Identity Service (EXT-01) | ใช้ประโยชน์จากฐานข้อมูลบัญชีนักศึกษา/อาจารย์เดิม ป้องกันการปลอมแปลงตัวตน และนำ Role มาใช้กับระบบ RBAC สอดคล้องกับ NFR-03 | [10-design-strategy.md](10-design-strategy.md), [11-conceptual-architecture.md](11-conceptual-architecture.md) | ญาณวุฒิ ชวนอาจ |
| **D-04** | 23/09/2026 | แยกจัดเก็บไฟล์เอกสารประกอบบน Dedicated File/Object Storage | Option B: Dedicated File Storage (EXT-03) + DB URL | ป้องกันปัญหาฐานข้อมูลโตเร็วผิดปกติ (Database Bloat) และรักษาความเร็วในการ Query ข้อมูล สอดคล้องกับ NFR-02 | [10-design-strategy.md](10-design-strategy.md), [13-detailed-design.md](13-detailed-design.md) | จิราพัชร อินจันทร์ |
| **D-05** | 23/09/2026 | ใช้ Finite State Machine และตาราง Audit Log แบบ Append-Only | Option B: FSM + Append-Only Log | ควบคุมการเปลี่ยนสถานะคำขอให้เป็นไปตามกฎธุรกิจ (BR-01, BR-04) และเก็บบันทึกประวัติที่ไม่สามารถแก้ไขหรือลบได้ | [10-design-strategy.md](10-design-strategy.md), [13-detailed-design.md](13-detailed-design.md) | จักรพงศ์ หมื่นไชยศรี |
| **D-06** | 23/09/2026 | ใช้ Event-Driven Notification Service ผ่าน Email สถาบัน และ Web Notification | Option B: Event-Driven Notification (EXT-02) | ส่งการแจ้งเตือนทันทีเมื่อสถานะเปลี่ยน (FR-04) ประหยัด Bandwidth และสอดคล้องกับขอบเขตสถาบันโดยไม่ต้องพึ่งพา LINE API | [10-design-strategy.md](10-design-strategy.md), [11-conceptual-architecture.md](11-conceptual-architecture.md) | ญาณวุฒิ ชวนอาจ |

> ดูรายละเอียดบันทึกการตัดสินใจฉบับเต็มได้ที่ [project-management/decision-log.md](../project-management/decision-log.md)