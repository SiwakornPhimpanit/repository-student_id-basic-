# ANSWER — YOUR_NAME STUDENT_ID

## Part A — ข้อมูลจาก image kamthornsa/ksu-promo:1.0

| คำถาม | คำตอบ | คำสั่งที่ใช้ |
| --- | --- | --- |
| Port | [กรอกจากผลจริง] | `docker image inspect kamthornsa/ksu-promo:1.0 --format '{{json .Config.ExposedPorts}}'` |
| CMD | [กรอกจากผลจริง รวม Entrypoint ถ้ามี] | `docker image inspect kamthornsa/ksu-promo:1.0 --format '{{json .Config.Cmd}}'` และ `docker image inspect kamthornsa/ksu-promo:1.0 --format '{{json .Config.Entrypoint}}'` |
| Base image | [กรอกจากหลักฐานจริง] | `docker image history --no-trunc kamthornsa/ksu-promo:1.0` และ `docker image inspect kamthornsa/ksu-promo:1.0` |

ผลคำสั่งและหลักฐานที่ใช้ระบุ base image:

```text
[วางผลจริง ห้ามเดา base image จากชื่อ image]
```

## Part B — รหัสลับบนหน้าโปรโมชั่น

[กรอกรหัสลับที่เห็นจริงบน localhost:8081 ของ tag 1.0]

## Part C — คำถาม

ปรับคำตอบเป็นภาษาของตนเองและเติมผลทดลองก่อนส่ง

1. เมนูมีซอร์ส index.html ของเรา จึงแก้แล้ว build image ใหม่ได้ ส่วนโปรโมชั่นมีเฉพาะ image ไม่มีซอร์สสำหรับแก้และ build ตามวิธีเดียวกัน การแก้ไฟล์ภายใน container หากทำได้จะไม่แก้ image ต้นฉบับและไม่คงอยู่เมื่อสร้าง container ใหม่
2. ไม่ระบุ tag จะใช้ latest ซึ่งเป็น tag แยกจาก 1.0 และไม่ได้รับประกันว่าเหมือนกัน ผลทดลองจริง: [เติมเนื้อหาของ latest และความต่างจาก 1.0]
3. ฝั่งซ้าย 8081 คือ port บนเครื่องเรา ฝั่งขวา 3000 คือ port ภายใน container ที่แอปรับคำขอ บริการนี้ใช้ 3000 ตามโจทย์ โดยต้องตรวจยืนยันจาก image และการเปิดเว็บ จึงไม่ได้ใช้ 80
4. เมื่อมี image เดิมแล้ว docker compose up -d อย่างเดียวไม่ build ไฟล์ที่เปลี่ยน เพราะ COPY เก็บไฟล์ไว้ตอน build ใช้ docker compose up -d --build --no-deps menu เพื่อ build และอัปเดต menu โดย promo ยังทำงานอยู่
5. ใช้ http://localhost:8081 เพราะเบราว์เซอร์ทำงานบนเครื่องเรา ส่วน promo เป็นชื่อ DNS ภายในเครือข่าย Compose สำหรับ container ในเครือข่ายเดียวกัน เบราว์เซอร์บนเครื่องเราใช้ชื่อนี้ไม่ได้ตามปกติ

## ภาพหน้าจอ

![Menu v1 และ docker ps](screenshots/00-menu.png)
![Menu](screenshots/01-menu.png)
![Promo](screenshots/02-promo.png)
