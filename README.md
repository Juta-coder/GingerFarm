# โหวตเมนู Ginger Farm Kitchen

แอปโหวตเมนู: แต่ละคนใส่ชื่อจริงแล้วเลือก 2 จาน ผลเก็บใน Google Sheet และดูผลได้เฉพาะ Admin (ต้องใส่รหัส)

## ไฟล์ในชุดนี้
| ไฟล์ | ใช้ทำอะไร |
|---|---|
| `index.html` | หน้าเว็บโหวต (ขึ้น GitHub) |
| `images/` | รูปเมนู 27 จาน (ขึ้น GitHub) |
| `Code.gs` | ระบบหลังบ้าน (วางใน Google Apps Script ไม่ต้องขึ้น GitHub) |

## ขั้นที่ 1: ตั้ง Google Sheet (5 นาที)
1. สร้าง Google Sheet ใหม่ ตั้งชื่อเช่น `GFK Menu Poll`
2. เมนู **Extensions > Apps Script** ลบโค้ดเดิม แล้ววางโค้ดทั้งหมดจาก `Code.gs` แล้วกด Save
3. ตั้งรหัส Admin: **Project Settings (ไอคอนเฟือง) > Script properties > Add script property**
   - Property: `ADMIN_PASSWORD`
   - Value: รหัสที่ต้องการ
4. **Deploy > New deployment** > เลือกประเภท **Web app**
   - Execute as: **Me**
   - Who has access: **Anyone**
5. กด Deploy แล้วกดอนุญาตสิทธิ์ (Authorize) จากนั้น **คัดลอก Web app URL** (ลงท้ายด้วย `/exec`)

## ขั้นที่ 2: ใส่ URL ลงหน้าเว็บ
เปิด `index.html` หาบรรทัดนี้:
```js
const API_URL = "PASTE_YOUR_APPS_SCRIPT_WEB_APP_URL_HERE";
```
แทนที่ข้อความในเครื่องหมายคำพูดด้วย Web app URL จากขั้นที่ 1

## ขั้นที่ 3: ขึ้น GitHub Pages
1. สร้าง repository ใหม่บน GitHub
2. **Add file > Upload files** แล้วลาก `index.html` และโฟลเดอร์ `images` ขึ้นไป กด Commit
3. **Settings > Pages** > Source: **Deploy from a branch** > Branch: `main` / `(root)` > Save
4. รอ 1-2 นาที จะได้ลิงก์ `https://<username>.github.io/<repo>/`

## การใช้งาน
- **ลิงก์โหวต (ส่งให้ทีม):** `https://<username>.github.io/<repo>/`
- **ลิงก์ Admin:** เติม `#admin` ท้ายลิงก์ เช่น `https://<username>.github.io/<repo>/#admin` แล้วใส่รหัส
- ดูข้อมูลดิบได้ที่ Google Sheet แท็บ `Votes`

## หมายเหตุ
- ถ้าแก้ `Code.gs` ภายหลัง ต้อง **Deploy > Manage deployments > Edit > Version: New version** URL จะยังเหมือนเดิม
- ใช้ชื่อเดิมโหวตซ้ำ = แก้โหวตเดิม (ไม่นับซ้ำ)
- GitHub Pages ฟรีต้องเป็น repo Public ใครมีลิงก์ก็เปิดหน้าโหวตได้ แต่ผลโหวตปลอดภัย เพราะรหัส Admin ตรวจที่ Google ไม่ได้อยู่ในหน้าเว็บ
- รูปเมนูเป็นของร้าน Ginger Farm Kitchen ใช้สำหรับโหวตภายในทีม
