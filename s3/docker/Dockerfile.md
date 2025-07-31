

FROM node:20-alpine

- اولین دستور فایل هستش مگر اینکه ARG قبلش استفاده کنیم.

---


LABEL maintainer="ferzz@example.com"
LABEL version="1.0"

- یه سری متادیتا هستش که اضافه میکنیم


LABEL org.opencontainers.image.title="nazareto"
LABEL org.opencontainers.image.version="2.3.1"
LABEL org.opencontainers.image.source="https://github.com/ferzz/nazareto"

برای دیدن لیبل ها

docker inspect myapp


---

RUN apk add --no-cache git
RUN npm install

- هر ران یک لایه جدید ایجاد میکنه.
- میشه چند دستور رو در یک ران ترکیب کرد.
RUN apk update && apk add --no-cache git curl


CMD ["node", "index.js"]

- فقط یک دستور مجاز است
- اگر در `docker run` دستور بدی، این نادیده گرفته می‌شه


ENTRYPOINT ["python"]

- مشابه `CMD` اما **غیربازنویسی‌شونده** (ثابت می‌مونه مگر با `--entrypoint`)

میشه cmd و entrypoint رو ترکیب کرد
ENTRYPOINT ["python", "app.py"]
CMD ["--port", "8000"]

---
ADD

شبیه `COPY` ولی با قابلیت‌های اضافه:
- استخراج اتوماتیک فایل‌های `.tar.gz`
- دانلود URL مستقیم (به شدت توصیه نمی‌شود برای URL)



COPY ./src /app/src

فقط فایل‌های در `.dockerignore` نادیده گرفته می‌شن
سریع‌تر از `ADD` و قابل پیش‌بینی‌تره


---

WORKDIR

تنظیم مسیر کاری (مثل `cd`) برای دستورات بعدی
WORKDIR /app

---

ENV
ENV NODE_ENV=production
ENV PORT=3000

---

ARG

تعریف آرگومان برای زمان build (نه زمان اجرا)
ARG VERSION=1.0

---

EXPOSE
اعلام پورت مورد استفاده در کانتینر
EXPOSE 3000
- فقط جنبه‌ی **مستندسازی** داره. پورت رو باز نمی‌کنه! باید در `docker run` از `-p` استفاده کنی.

---

VOLUME

تعریف مسیرهایی که بهتره به عنوان Volume استفاده بشن

VOLUME ["/data"]

---

USER
مشخص‌کردن کاربری که دستورات بعدی با اون اجرا می‌شن
USER node


---

HEALTHCHECK
بررسی سلامت کانتینر
HEALTHCHECK --interval=30s --timeout=10s \
  CMD curl -f http://localhost:3000/health || exit 1


---

ONBUILD
دستوراتی که در image پایه ذخیره می‌شن و در مرحله بعدی build یک image جدید اجرا می‌شن

`ONBUILD COPY . /app`

---

SHELL
تغییر shell پیش‌فرض برای اجرای `RUN`

SHELL ["/bin/bash", "-c"]
