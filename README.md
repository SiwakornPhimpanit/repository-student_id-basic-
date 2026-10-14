# คู่มือข้อ 1 Docker

แทน YOUR_NAME และ STUDENT_ID ด้วยข้อมูลจริงในไฟล์และชื่อโฟลเดอร์
ชุดนี้เริ่ม Menu v1 เพื่อทำจุดตรวจ ยังไม่ใช่งานพร้อมส่ง
เปิด Docker Desktop และใช้ PowerShell ในโฟลเดอร์ที่แตก ZIP

## ขั้นที่ 1

```powershell
docker build -t ksu-menu:1.0 .
docker run -d --name menu-test -p 8080:80 ksu-menu:1.0
docker ps
```

เปิด http://localhost:8080 เก็บ screenshots/00-menu.png ให้เห็นเว็บและ docker ps
ให้ผู้คุมสอบตรวจก่อนลบ menu-test

## ขั้นที่ 2

```powershell
docker pull kamthornsa/ksu-promo:1.0
docker image inspect kamthornsa/ksu-promo:1.0 --format '{{json .Config.ExposedPorts}}'
docker image inspect kamthornsa/ksu-promo:1.0 --format '{{json .Config.Cmd}}'
docker image inspect kamthornsa/ksu-promo:1.0 --format '{{json .Config.Entrypoint}}'
docker image history --no-trunc kamthornsa/ksu-promo:1.0
docker image inspect kamthornsa/ksu-promo:1.0
```

เติมผลจริงใน Part A โดย history อาจไม่บอกชื่อและ tag ของ base image โดยตรง
อย่าใช้ CMD เพียงอย่างเดียวเป็นหลักฐานระบุ base image

## ขั้นที่ 3 หลังผู้คุมสอบตรวจ

```powershell
docker rm -f menu-test
docker compose up -d
docker compose ps
```

เปิด http://localhost:8080 และ http://localhost:8081 เติมรหัสลับลง Part B

## ขั้นที่ 4

แก้ Menu v1 เป็น Menu v2 เพิ่มรายการด้านล่างใน ul และนำ comment รอบลิงก์ออก

```html
<li><span>มัทฉะลาเต้เย็น</span><strong>65 บาท</strong></li>
<a href="http://localhost:8081">ดูโปรโมชั่น</a>
```

วาง li ใน ul และวาง a หลัง ul จากนั้นรันเพียงคำสั่งเดียว:

```powershell
docker compose up -d --build --no-deps menu
```

รีเฟรชและทดสอบคลิกลิงก์ เก็บ 01-menu.png และ 02-promo.png ให้เห็นแถบ URL พร้อม port

## ทดลอง latest ก่อนตอบ Part C ข้อ 2

```powershell
docker pull kamthornsa/ksu-promo:latest
docker image inspect kamthornsa/ksu-promo:latest --format '{{json .Config.ExposedPorts}}'
```

หากผลยืนยัน port 3000 รันคำสั่งนี้ (หากต่างออกไป เปลี่ยนฝั่งขวาตามผล):

```powershell
docker run -d --name promo-latest-test -p 8082:3000 kamthornsa/ksu-promo:latest
```

เปิด http://localhost:8082 เทียบกับ tag 1.0 เติมผลจริง แล้วลบ container ทดลอง:

```powershell
docker rm -f promo-latest-test
```

## ส่ง GitHub

สร้าง repository Public ชื่อ final-รหัสจริง ปรับ URL ด้านล่าง
ตรวจชื่อ รหัส คำตอบครบ และภาพ PNG จริงทั้ง 3 ภาพก่อน commit

```powershell
git init
git branch -M main
git status
git add index.html Dockerfile .dockerignore docker-compose.yml ANSWER.md screenshots
git commit -m "Docker practical exam"
git remote add origin https://github.com/YOUR_USERNAME/final-STUDENT_ID.git
git push -u origin main
```

ตรวจภาพใน ANSWER.md บน GitHub และสถานะ Public แล้วส่งลิงก์ repo
