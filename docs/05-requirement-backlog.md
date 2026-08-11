# 05 — Requirement Backlog and Prioritization

> **Week 5 deliverable**  
> Requirement ต้องระบุได้ ตรวจสอบได้ และเชื่อมโยงกับ stakeholder/value ที่ชัดเจน

## 1. Prioritization Method

- **วิธีที่ใช้:** MoSCoW Method (Must have, Should have, Could have, Won't have for current release) ร่วมกับ Value vs Risk & Dependency Analysis
- **หลักเกณฑ์:**
  1. **Business Value & Core Workflow:** ให้ความสำคัญสูงสุดกับ Requirement ที่เป็นแกนหลักของการนัดหมาย (ค้นหาเวลาว่าง -> ส่งคำขอ -> พิจารณาอนุมัติ)
  2. **Evidence & Stakeholder Consensus:** Requirement ที่ผ่านการเจรจาข้อยกเว้น (Negotiation Record) และมีระดับความเชื่อมั่น (Confidence) ระดับ High จะถูกจัดอยู่ในกลุ่ม Must/Should
  3. **Technical & Scope Constraints:** ฟังก์ชันที่มีความซับซ้อน เสี่ยงต่อ Data Privacy ขัดต่อนโยบาย IT หรือเกินขอบเขตงบประมาณ/เวลา จะถูกลดความสำคัญหรือจัดไว้ในกลุ่ม Won't
  4. **Dependency Order:** Requirement ที่เป็นเงื่อนไขตั้งต้น (เช่น ตารางเวลาว่าง และ Access Control) ต้องได้รับการพัฒนาในอันดับต้น

---

## 2. Functional Requirements

| ID | Requirement Statement | Source / Stakeholder | Priority | Acceptance Measure | Status |
|---|---|---|---|---|---|
| **FR-01** | ระบบต้องแสดงช่วงเวลาว่าง (Office Hours) ของอาจารย์ที่ปรึกษา เพื่อให้นักศึกษาสามารถเลือกวันและเวลาสำหรับการนัดหมายได้ | E-01, E-02 / นักศึกษา, อาจารย์ | Must | นักศึกษาและอาจารย์เห็นช่วงเวลาว่างรายชั่วโมงตรงกันบนตารางเวลาภายในระบบ | Ready for Dev |
| **FR-02** | ระบบต้องให้นักศึกษาส่งคำขอนัดหมาย โดยระบุวัตถุประสงค์ รายชื่อผู้เข้าพบ (รายบุคคล/กลุ่ม) และแนบเอกสารประกอบได้ | E-03 / นักศึกษา | Must | นักศึกษาสามารถกรอกฟอร์ม เลือกช่วงเวลาว่าง แนบไฟล์ และกดส่งคำขอสำเร็จ | Ready for Dev |
| **FR-03** | ระบบต้องให้อาจารย์สามารถอนุมัติ ปฏิเสธ หรือเสนอวันและเวลานัดหมายใหม่ (Reschedule) ได้ | E-04 / อาจารย์ที่ปรึกษา | Must | อาจารย์เปลี่ยนสถานะคำขอได้ถูกต้อง และระบบบันทึกสถานะตามที่เลือก | Ready for Dev |
| **FR-04** | ระบบต้องแจ้งเตือนผู้เกี่ยวข้องผ่าน Email สถาบัน และ Web Notification เมื่อมีคำขอนัดใหม่หรือสถานะคำขอเปลี่ยนแปลง | E-05, E-06, C-02 / นักศึกษา, อาจารย์ | Should | เกิด Notification บนหน้าเว็บ และ Email ส่งถึงกล่องข้อความเมื่อมีการเปลี่ยนสถานะคำขอ | Draft |
| **FR-05** | ระบบต้องบันทึกประวัติการนัดหมาย สรุปผลการเข้าพบ และจัดทำรายงานสรุปสถิติสำหรับภาควิชา | E-08 / เจ้าหน้าที่ภาควิชา, อาจารย์ | Could | เจ้าหน้าที่และอาจารย์สามารถเรียกดู/ส่งออกรายงานสถิติย้อนหลังได้ | Draft |

---

## 3. Non-functional Requirements

| ID | Quality Attribute | Requirement Statement | Measure / Criterion | Priority | Status |
|---|---|---|---|---|---|
| **NFR-01** | Security & Access Control | ระบบต้องกำหนดสิทธิ์การเข้าถึงข้อมูลตามบทบาท (RBAC) โดยนักศึกษาเห็นเฉพาะคำขอตนเอง อาจารย์เห็นคำขอนักศึกษาในสังกัด และเจ้าหน้าที่เห็นระดับภาควิชา | ผ่านการทดสอบ Role & Permission Matrix 100% ไม่พบข้อมูลรั่วไหลข้ามบทบาท | Must | Ready for Dev |
| **NFR-02** | Data Privacy | ระบบต้องจัดเก็บเฉพาะข้อมูลที่จำเป็นต่อการนัดหมาย (Data Minimization) และใช้งานปฏิทินภายในระบบเท่านั้น | ไม่มีข้อมูลส่วนตัวที่ไม่จำเป็นถูกจัดเก็บ และไม่มีการส่งออกข้อมูลไปยัง External API | Must | Ready for Dev |
| **NFR-03** | Usability & Real-time | ระบบต้องแสดงผลอัปเดตสถานะการจองและตารางเวลาให้เป็นปัจจุบัน (Real-time update) บนหน้าเว็บ UI | การอัปเดตสถานะแสดงผลบนหน้าจอผู้ใช้ภายในเวลาไม่เกิน 3 วินาที | Should | Draft |
| **NFR-04** | Compatibility | ระบบต้องรองรับการใช้งานผ่าน Web Browser มาตรฐานทั้งบนคอมพิวเตอร์และสมาร์ตโฟน | หน้าเว็บแสดงผล Responsive และทำงานได้สมบูรณ์บน Chrome, Safari, Edge | Should | Draft |

---

## 4. Business Rules / Constraints

| ID | Rule / Constraint | Rationale | Related FR/NFR |
|---|---|---|---|
| **BR-01** | **Advance Notice Cancellation:** การยกเลิกหรือขอเลื่อนนัดหมายโดยนักศึกษา ต้องทำล่วงหน้าอย่างน้อย 24 ชั่วโมงก่อนเวลานัดหมาย (มติ N-01 / C-01) | ป้องกันการเสียเวลาของอาจารย์ และเปิดโอกาสให้นักศึกษาคนอื่นลงนัดหมายแทนได้ | FR-02, FR-03 |
| **BR-02** | **Institutional Communication Only:** ช่องทางการส่งแจ้งเตือนจำกัดเฉพาะ Email สถาบัน และ Web Notification ในระบบเท่านั้น (มติ N-02 / C-02) | ควบคุมค่าใช้จ่าย ป้องกันปัญหา API ภายนอก และอยู่ในขอบเขตโครงการ | FR-04 |
| **BR-03** | **Consultation Mode Authority:** ระบบรองรับทั้งแบบ On-site และ Online โดยอาจารย์มีสิทธิ์ขาดในการพิจารณาอนุมัติรูปแบบ และเป็นผู้ระบุลิงก์ประชุมกรณี Online (มติ N-04 / C-04) | เพื่อความยืดหยุ่นในการสื่อสาร และให้อาจารย์จัดสรรตามความเหมาะสมของเนื้อหา | FR-02, FR-03 |
| **BR-04** | **Internal Calendar Isolation:** ปฏิทินและตารางเวลาจะใช้งานระบบจำลองภายในเท่านั้น ห้าม Sync กับ External Calendar เช่น Google Calendar (มติ N-03 / C-03) | ป้องกันประเด็น Data Privacy และเป็นไปตามข้อจำกัดนโยบาย IT สถาบัน | FR-01, NFR-02 |

---

## 5. Prioritized Backlog Summary

| Priority | Count | Requirement IDs |
|---|---:|---|
| **Must** | 5 | FR-01, FR-02, FR-03, NFR-01, NFR-02 |
| **Should** | 4 | FR-04, NFR-03, NFR-04, BR-01 |
| **Could** | 1 | FR-05 |
| **Won't (current release)** | 3 | Google Calendar External Sync (N-03), LINE Notify API (N-02), Auto-generate Meeting Link API (N-04) |

---

## 6. Assumptions / Dependencies

| ID | Assumption or Dependency | Impact if false | Owner / Follow-up |
|---|---|---|---|
| **A-01** | ผู้ใช้ทุกคนสามารถยืนยันตัวตนผ่านระบบบัญชีผู้ใช้ของสถาบัน (SSO) ได้ | ต้องพัฒนาระบบลงทะเบียนและยืนยันตัวตนใหม่ ซึ่งกระทบระยะเวลาโครงการ | IT Admin / Dev Team |
| **A-02** | อาจารย์ที่ปรึกษาเข้ามาอัปเดตช่วงเวลาว่าง (Office Hours) บนระบบอย่างสม่ำเสมอ | ตารางเวลาว่างไม่เป็นปัจจุบัน นักศึกษาจองเวลาที่อาจารย์ไม่สะดวกจริง | อาจารย์ที่ปรึกษา (Advisor) |
| **A-03** | ฝ่าย IT สถาบันไม่อนุญาตการเชื่อมต่อ External OAuth และ Third-party API เสียค่าใช้จ่าย | หากเปลี่ยนนโยบาย อาจต้องปรับสถาปัตยกรรมระบบเพื่อรองรับ Google Calendar / LINE API | IT Admin |
| **A-04** | เงื่อนไขข้อยกเว้นการยกเลิกนัดหมายกะทันหันกรณีป่วย/เหตุสุดวิสัย (Force Majeure) จะได้รับการสรุปนโยบายจากภาควิชา | นักศึกษาอาจเสียสิทธิ์ หรือระบบไม่สามารถผ่อนผันเงื่อนไข 24 ชม. ได้ | เจ้าหน้าที่ภาควิชา / สถาบัน |