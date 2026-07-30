---
title: My N8N Automation
emoji: 🔧
colorFrom: blue
colorTo: purple
sdk: docker
app_port: 7860
pinned: false
---

# n8n on Hugging Face Spaces

هذا الـ Space بيشغّل n8n (نسخة npm الرسمية) داخل حاوية Docker.

## ملاحظات مهمة

- **N8N_ENCRYPTION_KEY**: القيمة الموجودة في الـ Dockerfile دلوقتي قيمة حقيقية عشوائية (اتولدت مرة واحدة). **متغيرهاش بعد أول تشغيل** — لو غيرتها، هتفقد الوصول لأي بيانات اعتماد (credentials) اتخزنت قبل كده لأنها متشفرة بيها.
- **DB_TYPE=sqlite**: البيانات بتتخزن في `/home/node/.n8n/database.sqlite` جوه الحاوية. لو الـ Space اتعمله rebuild من غير persistent storage، البيانات ممكن تضيع. لو محتاج ثبات البيانات، فعّل **Persistent Storage** من إعدادات الـ Space، أو استخدم قاعدة بيانات خارجية (Postgres/Supabase) بدل SQLite.
- **WEBHOOK_URL / N8N_EDITOR_BASE_URL**: لازم يطابقوا الرابط الفعلي بتاع الـ Space (`https://<username>-<space-name>.hf.space`).

## لو حبيت تستخدم Postgres/Supabase بدل SQLite

استبدل السطرين دول:
```
ENV DB_TYPE=sqlite
ENV DB_SQLITE_DATABASE=/home/node/.n8n/database.sqlite
```
بـ:
```
ENV DB_TYPE=postgresdb
ENV DB_POSTGRESDB_HOST=<host>
ENV DB_POSTGRESDB_PORT=5432
ENV DB_POSTGRESDB_DATABASE=postgres
ENV DB_POSTGRESDB_USER=postgres
ENV DB_POSTGRESDB_PASSWORD=<password>
ENV DB_POSTGRESDB_SCHEMA=public
ENV DB_POSTGRESDB_SSL_ENABLED=true
ENV DB_POSTGRESDB_SSL_REJECT_UNAUTHORIZED=false
```
