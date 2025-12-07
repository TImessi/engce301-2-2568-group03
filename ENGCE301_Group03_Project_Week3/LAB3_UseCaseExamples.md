# Use Case Scenarios – ENGCE301 Lab Submission Portal

เอกสารนี้รวบรวม Use Case Scenario ที่ขยายความจาก User Stories
ใช้เป็นแนวทางในการพัฒนาระบบส่วน HTML/CSS (Web Lab)

---

## UC-03: Submit Lab File
**Reference:** FR-3, FR-4, US-03
**Primary Actor:** Student
**Goal:** ส่งไฟล์งาน LAB ผ่านระบบให้สำเร็จ

### Preconditions
1. นักศึกษาเข้าสู่ระบบเรียบร้อยแล้ว
2. เลือก LAB ที่ต้องการส่ง และเข้ามาสู่หน้า "Lab Details" แล้ว
3. LAB นั้นยังไม่ถูกปิดการส่ง (Not Closed)

### Postconditions
1. ไฟล์งานถูกบันทึกลงในระบบ
2. ระบบบันทึกเวลาที่ส่ง (Timestamp)
3. สถานะการส่งของนักศึกษาเปลี่ยนเป็น "Submitted" หรือ "Late"

### Main Flow (Happy Path - ส่งตรงเวลา)
1. นักศึกษาคลิกปุ่ม **"Choose File"** ในส่วน Submission
2. ระบบเปิดหน้าต่างให้เลือกไฟล์จากเครื่อง
3. นักศึกษาเลือกไฟล์ที่ถูกต้อง (.zip หรือ .pdf) แล้วกดยืนยัน
4. ระบบแสดงชื่อไฟล์ที่เลือก
5. นักศึกษากดปุ่ม **"Submit Assignment"**
6. ระบบตรวจสอบขนาดและประเภทไฟล์ (Validation)
7. ระบบตรวจสอบเวลาปัจจุบันเทียบกับ Deadline (พบว่าไม่เกิน)
8. ระบบบันทึกไฟล์และเปลี่ยนสถานะเป็น **"Submitted"**
9. ระบบแสดงข้อความแจ้งเตือน **"Submission Successful"**

### Alternative Flows
- **AF-1: ส่งงานช้า (Late Submission Policy)**
  1. ในขั้นตอนที่ 7 ระบบพบว่าเวลาปัจจุบัน **เกิน Deadline**
  2. ระบบบันทึกไฟล์ แต่กำหนดสถานะเป็น **"Late"**
  3. ระบบแสดงข้อความ **"Submitted Late"** พร้อมป้ายเตือนสีแดง (Late Badge)

- **AF-2: ชนิดไฟล์ไม่ถูกต้อง (Invalid File Type)**
  1. ในขั้นตอนที่ 6 ระบบพบว่าไฟล์ไม่ใช่ .zip หรือ .pdf
  2. ระบบปฏิเสธการบันทึก และแสดงข้อความ Error **"Only PDF and ZIP files are allowed."**
  3. Use Case วนกลับไปที่ขั้นตอนที่ 1

---

## UC-04: View My Lab Status
**Reference:** FR-8, US-04
**Primary Actor:** Student
**Goal:** ตรวจสอบสถานะการส่งงานและคะแนนของทุก LAB

### Preconditions
1. นักศึกษาเข้าสู่ระบบแล้ว
2. อยู่ที่หน้า Home หรือเมนูหลัก

### Postconditions
1. นักศึกษาได้รับรู้สถานะปัจจุบันของงานทั้งหมด

### Main Flow
1. นักศึกษาคลิกเมนู **"My Labs"**
2. ระบบดึงข้อมูล LAB ทั้งหมดที่ลงทะเบียนไว้
3. ระบบแสดงตารางรายชื่อ LAB พร้อมคอลัมน์: Lab Name, Deadline, Status, Score
4. นักศึกษาดูรายการและสถานะ (เช่น Submitted, Missing, Graded)
5. หาก LAB ใดมีการตรวจแล้ว (Graded) ระบบแสดงคะแนนที่ได้รับ

### Alternative Flows
- **AF-1: ไม่มีข้อมูล (No Labs Found)**
  1. ระบบค้นหาไม่พบรายการ LAB ใดๆ
  2. ระบบแสดงข้อความ **"No labs assigned yet."**

---

## UC-06: Grade Submission (Instructor)
**Reference:** FR-7, US-08
**Primary Actor:** Instructor
**Goal:** ให้คะแนนและเขียน Feedback ให้นักศึกษา

### Preconditions
1. Instructor เข้าสู่ระบบและเลือกดูรายชื่อคนส่งงาน (Submission List) แล้ว

### Postconditions
1. คะแนนและ Feedback ถูกบันทึกลงระบบ
2. นักศึกษาเจ้าของงานสามารถเห็นคะแนนได้ทันที

### Main Flow
1. Instructor คลิกเลือกชื่อนักศึกษาที่ต้องการตรวจ
2. ระบบแสดงไฟล์งานที่นักศึกษาส่งมา
3. Instructor ตรวจงานและกรอกคะแนนลงในช่อง **"Score"**
4. Instructor พิมพ์ข้อเสนอแนะลงในช่อง **"Feedback Comments"**
5. Instructor กดปุ่ม **"Save Grade"**
6. ระบบบันทึกข้อมูลและแสดงสถานะว่า **"Graded"**

### Alternative Flows
- **AF-1: กรอกคะแนนผิดรูปแบบ (Invalid Score)**
  1. Instructor กรอกคะแนนเกินช่วงที่กำหนด (เช่น ให้ 150 เต็ม 100)
  2. ระบบแสดง Error **"Score must be between 0 and 100."**
  3. ระบบไม่บันทึกข้อมูล