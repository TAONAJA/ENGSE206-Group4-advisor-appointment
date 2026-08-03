# 04 — Evidence Log and Issue List

> **Week 4 deliverable**  
> เก็บข้อเท็จจริงและสิ่งที่ตีความแยกกันอย่างชัดเจน

## 1. Evidence Tags

`CF` case fact · `SN` simulated need · `CT` constraint/rule · `OP` opinion · `AS` assumption · `PS` proposed solution · `OQ` open question

---

## 2. Evidence Log

| E-ID | Source/role/session | Tag | Statement / observed event | Context | Confidence + reason | Related/conflicting E-ID | Follow-up/owner |
|---|---|---|---|---|---|---|---|
| **E-01** | S-00 Case Description | CF | ตารางเวลาอาจารย์ไม่ชัดเจน ทำให้นักศึกษาต้องเสี่ยงเดินไปหาที่ห้องพักแล้วไม่พบอาจารย์ | Current process | High (Case) | E-02 | ใช้เป็นข้อมูลตั้งต้น |
| **E-02** | S-01 นักศึกษา | SN | ผู้แจ้งต้องการดูช่วงเวลาว่าง (Office Hours) ของอาจารย์แบบ Real-time ก่อนทำการนัดหมาย | Appointment | Medium (Simulation) | E-01, E-03 | ยืนยันการเชื่อมต่อตารางเวลาอาจารย์ |
| **E-03** | S-01 นักศึกษา | SN | ผู้แจ้งต้องการระบุหัวข้อ วัตถุประสงค์ และแนบไฟล์เอกสารประกอบการขอเข้าพบ | Booking Form | Medium (Simulation) | E-02, E-04 | กำหนดขนาดและประเภทไฟล์แนบ |
| **E-04** | S-02 อาจารย์ที่ปรึกษา | SN | อาจารย์ต้องการอนุมัติ ปฏิเสธ หรือเสนอเลื่อนเวลานัดหมายได้เมื่อติดภารกิจด่วน | Approval Workflow | Medium (Simulation) | E-03, E-05 | ยืนยันเงื่อนไขการเสนอเปลี่ยนเวลา |
| **E-05** | S-02 อาจารย์ที่ปรึกษา | SN | ต้องการให้ระบบส่งสัญญาณแจ้งเตือนเมื่อมีคำขอนัดหมายใหม่เข้ามา | Notification | Medium (Simulation) | E-04 | ยืนยันช่องทางแจ้งเตือน (Email/Line) |
| **E-06** | S-01 นักศึกษา | SN | ผู้แจ้งต้องการทราบสถานะการอนุมัติคำขอนัดหมายแบบทันที | Tracking | Medium (Simulation) | E-05 | ยืนยันรูปแบบข้อความแจ้งเตือน |
| **E-08** | S-04 ผู้ดูแลระบบ | CT | ระบบต้องจำกัดสิทธิ์การเข้าถึงข้อมูลประวัติการนัดหมายตามบทบาทเพื่อความเป็นส่วนตัว | Security & Privacy | High (Policy) | E-07 | ยืนยัน Role & Permission Matrix |


## 3. Issue 

| ID | Evidence-linked issue/conflict | Parties + authority | Positions | Interests/constraints | Status |
|---|---|---|---|---|---|
| **C-01** | เงื่อนไขเวลาในการยกเลิกหรือเลื่อนนัดหมาย (E-03, E-04) | นักศึกษา vs อาจารย์ที่ปรึกษา | นักศึกษาต้องการยกเลิกได้ตลอดเวลา แต่อาจารย์ต้องการให้แจ้งล่วงหน้าอย่างน้อย 24 ชม. | ความยืดหยุ่นของผู้ใช้ vs การจัดสรรเวลาและภารกิจของอาจารย์ | Decided |
| **C-02** | ช่องทางการส่งแจ้งเตือนสถานะคำขอ (E-05, E-06) | ผู้ดูแลระบบ IT vs นักศึกษา/อาจารย์ | นักศึกษาต้องการ LINE Notify/Push Notification แต่ IT ให้ใช้ Web + Email สถาบัน | ค่าใช้จ่าย/ขอบเขตเทคนิคระบบสถาบัน vs ความสะดวกในการรับข่าวสาร | Decided |
| **C-03** | การเชื่อมโยงตารางเวลากับปฏิทินภายนอก (E-01, E-02) | อาจารย์ที่ปรึกษา vs ผู้ดูแลระบบ IT | อาจารย์ต้องการ Sync ข้อมูลกับ Google Calendar อัตโนมัติ แต่ IT กังวลเรื่องความปลอดภัย | ความสะดวกของอาจารย์ vs นโยบายความเป็นส่วนตัวและสิทธิ์ API | Open |
| **C-04** | รูปแบบและสถานที่ในการจัดนัดหมาย (E-03, E-04) | นักศึกษา vs อาจารย์ที่ปรึกษา | นักศึกษาขอเข้าพบแบบออนไลน์ (Zoom/MS Teams) แต่อาจารย์ต้องการเน้นพบหน้า (On-site) | ความสะดวกการเดินทาง vs ประสิทธิภาพในการให้คำปรึกษา | Decided |

## 4. Negotiation Record

| Date | Participants | Topic | Agreed outcome | Follow-up |
|---|---|---|---|---|
| [date] | [names/roles] | [กรอก] | [กรอก] | [กรอก] |

## 4. New / Revised Insights

- [Insight 1]
- [Insight 2]

## 5. Links to Evidence Files

- [Workshop notes](../evidence/week-04/README.md)
- [Meeting minutes](../project-management/meeting-minutes/README.md)
