# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## ภาพรวมโปรเจกต์

โปรเจกต์นี้ยังไม่มีซอร์สโค้ด มีเพียงโครงสร้างเอกสาร (`docs/`) สำหรับบริหารจัดการโปรเจกต์แบบ end-to-end ตั้งแต่ requirement ไปจนถึง retrospective ยังไม่มี build/lint/test command เพราะยังไม่มีโค้ดให้รัน — เมื่อมีการเพิ่มโค้ดจริงในอนาคต ให้อัปเดตไฟล์นี้ด้วยคำสั่ง build/lint/test ที่เกี่ยวข้อง

## โครงสร้างเอกสารและลำดับการไหลของงาน (docs pipeline)

เอกสารทั้งหมดอยู่ใต้ `docs/` และแต่ละโฟลเดอร์มี `index.md` อธิบายจุดประสงค์ของตัวเอง ลำดับการไหลของงานคือ:

```
01-requirements (01-spec → 02-plan → 03-task)
        ↓
02-design (01-prototypes → 02-technical)
        ↓
03-testing (01-test-plan → 02-test-result)
        ↓
04-retrospectives
```

พร้อมกับ `05-log` ที่บันทึกความเคลื่อนไหว/การตัดสินใจสำคัญแบบ chronological คู่ขนานไปกับทุกขั้นตอน และ `00-archived` สำหรับเอกสารที่เลิกใช้แล้ว

รายละเอียดแต่ละโฟลเดอร์:

- **01-requirements/01-spec** — ต้นทาง (source of truth) ของ feature requirements, user stories, business rules, scope
- **01-requirements/02-plan** — roadmap, phase/milestone, priority ที่แตกมาจาก spec
- **01-requirements/03-task** — task breakdown ที่ลงมือทำได้จริง พร้อมสถานะ/ผู้รับผิดชอบ
- **02-design/01-prototypes** — wireframe/mockup, user flow, design system เบื้องต้น อ้างอิงจาก spec
- **02-design/02-technical** — system architecture, database schema, API design, ตัวเลือกเทคโนโลยี
- **03-testing/01-test-plan** — test case/scenario อ้างอิงจาก spec และ technical design
- **03-testing/02-test-result** — ผล pass/fail และบั๊กที่พบจริง
- **04-retrospectives** — สรุปบทเรียนหลังจบ phase/sprint โดยอ้างอิงจาก test result และ log
- **05-log** — changelog, decision log, เหตุการณ์สำคัญ
- **00-archived** — เอกสารเวอร์ชันเก่า/ที่ถูกยกเลิก

## กฎสำคัญเมื่อแก้ไขเอกสาร

- **ห้ามลบเอกสารออกจากโปรเจกต์โดยตรง** — ให้ย้ายไปเก็บไว้ใน `docs/00-archived/` เพื่อรักษาประวัติการตัดสินใจ (ระบุไว้ใน `docs/00-archived/index.md`)
- เอกสารแต่ละหมวดอ้างอิงถึงกันด้วย wikilink สไตล์ Obsidian (`[[../path/index|label]]`) ตามลำดับการไหลของงานข้างต้น — เมื่อเพิ่มเอกสารใหม่ในหมวดใด ให้เชื่อมโยงไปยังหมวดต้นทางและหมวดปลายทางตามรูปแบบเดิม
- เนื้อหาเอกสารเขียนเป็นภาษาไทย ให้เขียนเอกสารใหม่ในภาษาเดียวกันเพื่อความสอดคล้อง

## เงื่อนไขและข้อกำหนดในการทำงาน

- **ห้ามข้ามลำดับ pipeline** — อย่าเริ่มเขียนเอกสารในหมวดปลายทาง (เช่น `02-design`, `03-testing`) ก่อนที่หมวดต้นทางที่เกี่ยวข้อง (เช่น `01-requirements/01-spec`) จะมีเนื้อหารองรับ หากจำเป็นต้องข้าม ให้ระบุเหตุผลไว้ใน `05-log`
- **บันทึกการตัดสินใจสำคัญทุกครั้ง** — เมื่อมีการเปลี่ยนแผน เปลี่ยน scope หรือตัดสินใจเชิงเทคนิคที่กระทบหลายหมวด ให้เพิ่มรายการใน `docs/05-log/index.md` พร้อมวันที่และเหตุผล
- **ปรับสถานะงานให้ตรงความจริงเสมอ** — เอกสารใน `01-requirements/03-task` ต้องสะท้อนสถานะปัจจุบัน (ยังไม่เริ่ม/กำลังทำ/เสร็จแล้ว) ทุกครั้งที่มีความคืบหน้า
- **ก่อนทำการเปลี่ยนแปลงเชิงโครงสร้าง** (ย้าย/ลบ/รีออร์แกไนซ์โฟลเดอร์ในระดับ `docs/`) ให้แจ้งและขอคำยืนยันจากผู้ใช้ก่อนเสมอ เนื่องจากกระทบ wikilink ที่เชื่อมโยงกันทั้งโปรเจกต์
- ยังไม่มี build/lint/test เพราะไม่มีโค้ด — เมื่อเริ่มมีโค้ดจริง ให้เพิ่มเงื่อนไขเรื่อง commands ในไฟล์นี้ทันที ไม่ปล่อยให้ CLAUDE.md ล้าหลังโค้ด

> เงื่อนไขข้างต้นเป็นค่าเริ่มต้นที่สรุปจากกฎที่มีอยู่แล้วในเอกสาร หากมีข้อกำหนดเฉพาะเจาะจงเพิ่มเติม (เช่น ผู้อนุมัติเอกสาร, deadline ของแต่ละ phase, เครื่องมือที่ต้องใช้) แจ้งได้เพื่อเพิ่มเข้าไปในส่วนนี้

## Agent และ Skill ที่มีในโปรเจกต์

- **Agent `backlog-analyst`** (`.claude/agents/backlog-analyst.md`) และ **Skill `requirement-to-backlog`** (`.claude/skills/requirement-to-backlog/SKILL.md`) — ใช้วิเคราะห์เอกสารใน `docs/01-requirements/01-spec` แล้วแปลงเป็น Product Backlog (epic, user story, acceptance criteria, priority แบบ MoSCoW) บันทึกผลลงที่ `docs/01-requirements/03-task/product-backlog.md` ทั้งสองใช้วิธีการเดียวกัน ต่างกันที่ agent เหมาะกับ spec จำนวนมากที่ต้องแยกบริบทการทำงาน
