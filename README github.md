# Stock Cycle Count — ฐานข้อมูล (Data Repository)

ที่เก็บข้อมูลต้นฉบับสำหรับแอป **Stock Cycle Count** (Big C Sainoi · store 11252)

แอปทำงานแบบ **ออฟไลน์** (ฝังข้อมูลในไฟล์ HTML) — repo นี้เป็น **ต้นฉบับกลาง** ไว้แก้ไข/อัปเดต แล้วค่อยสร้างไฟล์แอปใหม่

## โครงสร้างไฟล์

```
/data
  ├─ multI_SV.csv          ← ตารางแปลงลัง → ตัวเดี่ยว (pack → single mapping)
  ├─ product_master.csv    ← รายชื่อสินค้าทั้งหมด (product master)
  └─ packmap.js            ← ข้อมูล multI_SV ที่แปลงเป็น JS แล้ว (ฝังในแอป)
README.md
```

## ไฟล์แต่ละอัน

### 1. `data/multI_SV.csv`

ตารางแปลงหน่วยลัง (case/pack) เป็นตัวเดี่ยว (single unit)

|คอลัมน์                |ความหมาย                 |
|---------------------|-------------------------|
|Barcode              |บาร์โค้ดลัง (pack)          |
|Description          |ชื่อลัง                     |
|Barcode Component    |บาร์โค้ดตัวเดี่ยว (single)    |
|Description Component|ชื่อตัวเดี่ยว                 |
|Quantity             |จำนวนต่อลัง (เช่น 12, 24, 48)|

**การเพิ่มลังใหม่:** เพิ่มแถวใหม่ในไฟล์นี้ (ชื่อลัง + บาร์โค้ดตัวเดี่ยว + จำนวนต่อลัง) แล้วสร้าง `packmap.js` ใหม่ (ดูด้านล่าง)

### 2. `data/product_master.csv`

รายชื่อสินค้าทั้งหมด 30,712 รายการ

คอลัมน์: `DIVISION_NAME, DEPARTMENT_NAME, ART_SV_NAME, BARCODE, UOM, END_QTY, NORMAL_COST`

### 3. `data/packmap.js`

ไฟล์ JavaScript ที่แปลงจาก `multI_SV.csv` แล้ว — เอาไปฝังในแอป
รูปแบบ: `window.PACKMAP={byBc:{...}, byName:{...}}`

## วิธีอัปเดตข้อมูล

1. แก้ `multI_SV.csv` (เพิ่ม/แก้รายการลัง) หรือ `product_master.csv`
1. สร้าง `packmap.js` ใหม่จาก `multI_SV.csv`
1. เอา `packmap.js` ไปฝังในไฟล์แอป `Stock_Cycle_Count.html` (แทนที่บล็อก `<script>window.PACKMAP=...</script>`)

## การนำขึ้น GitHub

1. สร้าง repository ใหม่ (เช่น `stock-cycle-count-data`)
1. อัปโหลดโฟลเดอร์ `data/` และ `README.md`
1. ถ้าต้องการให้ดึงไฟล์ผ่าน URL ใช้รูปแบบ raw:
   `https://raw.githubusercontent.com/<user>/<repo>/main/data/multI_SV.csv`

> หมายเหตุ: แอปเวอร์ชันปัจจุบันฝังข้อมูลไว้ในตัวแล้ว ทำงานได้โดยไม่ต้องต่อเน็ต
> repo นี้มีไว้เพื่อเก็บต้นฉบับและควบคุมเวอร์ชันของข้อมูลเท่านั้น