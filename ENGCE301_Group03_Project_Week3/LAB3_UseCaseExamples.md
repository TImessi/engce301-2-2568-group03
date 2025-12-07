# Use Case Scenarios – ENGCE301 Lab Submission Portal

เอกสารนี้รวบรวม Use Case Scenario จำนวน 6 ข้อ (UC-01 ถึง UC-06)
ครอบคลุมการทำงานของ Student และ Instructor ตาม SRS

---

## UC-01: View Lab List
**Reference:** FR-1, US-01
**Primary Actor:** Student
**Goal:** ดูรายการ LAB ทั้งหมดที่มีในรายวิชา

### Preconditions
1. นักศึกษาเข้าสู่หน้าแรก (Landing Page) ของระบบได้

### Postconditions
1. นักศึกษาเห็นรายการ LAB เรียงตามลำดับ หรือตามวันหมดเขต

### Main Flow
1. นักศึกษาเปิดหน้าเว็บไซต์ (index.html)
2. ระบบดึงข้อมูลรายการ LAB ทั้งหมดจากฐานข้อมูล (หรือ Mock Data)
3. ระบบแสดงส่วน **"Upcoming Labs"**
4. แต่ละรายการแสดง: ชื่อ LAB, คำอธิบายย่อ, และ Deadline
5. นักศึกษารับรู้ว่ามีงานอะไรที่ต้องทำบ้าง

### Alternative Flows
- **AF-1: ไม่พบรายการ LAB**
  1. ระบบค้นหาแล้วไม่พบข้อมูล LAB
  2. ระบบแสดงข้อความ "No active labs at the moment."

---

## UC-02: View Lab Details
**Reference:** FR-2, US-02
**Primary Actor:** Student
**Goal:** ดูรายละเอียดโจทย์และไฟล์ประกอบของ LAB ที่เลือก

### Preconditions
1. นักศึกษาเห็นรายการ LAB จาก UC-01

### Postconditions
1. นักศึกษาเห็นรายละเอียดครบถ้วน (Objectives, Instruction, Files)

### Main Flow
1. นักศึกษาคลิกที่การ์ด LAB หรือปุ่ม **"View Details"**
2. ระบบเปิดหน้าต่างใหม่ หรือ Modal แสดงรายละเอียด
3. ระบบแสดงโจทย์, ไฟล์แนบ (PDF/Zip), และสถานะการส่งปัจจุบัน
4. นักศึกษาอ่านโจทย์เพื่อเตรียมตัวทำงาน

### Alternative Flows
- **AF-1: ข้อมูลผิดพลาด**
  1. ระบบไม่สามารถโหลดรายละเอียดได้
  2. ระบบแสดง Error "Cannot load lab details."

---

## UC-03: Submit Lab File
**Reference:** FR-3, FR-4, US-03
**Primary Actor:** Student
**Goal:** อัปโหลดไฟล์งานเพื่อส่งการบ้าน

### Preconditions
1. นักศึกษาอยู่ในหน้าดูรายละเอียด (UC-02)
2. LAB ยังไม่ถูกปิด (Status: Open)

### Postconditions
1. ไฟล์ถูกบันทึกและระบบจำเวลาส่ง (Timestamp)
2. สถานะงานเปลี่ยนเป็น Submitted หรือ Late

### Main Flow (ส่งปกติ)
1. นักศึกษาคลิกปุ่ม **"Choose File"**
2. เลือกไฟล์ .zip หรือ .pdf จากเครื่องคอมพิวเตอร์
3. นักศึกษากดปุ่ม **"Submit Assignment"**
4. ระบบตรวจสอบความถูกต้องของไฟล์ (File Validation)
5. ระบบบันทึกไฟล์และเวลาส่ง
6. ระบบแสดงข้อความ **"Submission Successful"**

### Alternative Flows
- **AF-1: ส่งงานช้า (Late Submission)**
  1. ระบบตรวจสอบพบว่าเวลาส่ง **เกิน Deadline**
  2. ระบบบันทึกงานแต่กำหนดสถานะเป็น **"Late"**
  3. แจ้งเตือนนักศึกษาว่าส่งงานล่าช้า

- **AF-2: ไฟล์ผิดประเภท**
  1. ระบบพบว่าไฟล์ไม่ใช่ .pdf หรือ .zip
  2. ระบบปฏิเสธการส่งและแจ้งเตือน "Invalid file format."

---

## UC-04: View My Lab Status
**Reference:** FR-8, US-04
**Primary Actor:** Student
**Goal:** ตรวจสอบสถานะและคะแนนของทุก LAB ในที่เดียว

### Preconditions
1. นักศึกษาเข้าเมนู "My Labs"

### Postconditions
1. นักศึกษาเห็นตารางสรุปงานทั้งหมด

### Main Flow
1. นักศึกษาคลิกเมนู **"My Labs"** (my-labs.html)
2. ระบบแสดงตารางรายการ LAB ทั้งหมด
3. ระบบแสดงสถานะแต่ละงาน: *Pending, Submitted, Late, หรือ Graded*
4. หากมีการให้คะแนนแล้ว ระบบจะแสดงคะแนนในช่อง Score

### Alternative Flows
- **AF-1: ยังไม่เคยส่งงานเลย**
  1. ระบบแสดงตารางว่าง หรือข้อความ "No submissions yet."

---

## UC-05: Create New Lab
**Reference:** FR-5, US-06
**Primary Actor:** Instructor
**Goal:** สร้างโจทย์ LAB ใหม่ให้นักศึกษาทำ

### Preconditions
1. ผู้ใช้ต้อง Login ด้วยสิทธิ์ Instructor

### Postconditions
1. มี LAB ใหม่ปรากฏในหน้ารายการของนักศึกษา

### Main Flow
1. Instructor คลิกปุ่ม **"Create Lab"**
2. ระบบแสดงแบบฟอร์มให้กรอกข้อมูล
3. Instructor กรอก: ชื่อ LAB, คำอธิบาย, Deadline, และแนบไฟล์โจทย์
4. Instructor กดปุ่ม **"Publish Lab"**
5. ระบบบันทึกข้อมูลและเปิดให้นักศึกษาเห็นทันที

### Alternative Flows
- **AF-1: ข้อมูลไม่ครบ**
  1. Instructor ลืมกรอกชื่อ LAB หรือ Deadline
  2. ระบบแจ้งเตือนให้กรอกข้อมูลให้ครบถ้วน

---

## UC-06: Grade Submission
**Reference:** FR-7, US-08
**Primary Actor:** Instructor
**Goal:** ตรวจงานและให้คะแนนนักศึกษา

### Preconditions
1. มีนักศึกษาส่งงานเข้ามาในระบบแล้ว
2. Instructor เข้าเมนูตรวจงาน

### Postconditions
1. นักศึกษาได้รับคะแนนและ Feedback
2. สถานะงานเปลี่ยนเป็น "Graded"

### Main Flow
1. Instructor เลือกรายชื่อนักศึกษาที่ส่งงาน
2. ระบบแสดงไฟล์งานและช่องกรอกคะแนน
3. Instructor ดาวน์โหลดไฟล์มาตรวจ
4. Instructor กรอกคะแนน (Score) และข้อเสนอแนะ (Feedback)
5. Instructor กด **"Save Grade"**
6. ระบบบันทึกผลการตรวจ

### Alternative Flows
- **AF-1: คะแนนเกินเกณฑ์**
  1. กรอกคะแนนเกินค่า Max Score (เช่น 105/100)
  2. ระบบแจ้งเตือนและไม่บันทึกผล