
sudo apt install docker-compose-plugin
برای نصب 



version: "3.8"

services:
  web:
    build:
		context: .
		dockerfile: Dockerfile.dev
    ports:
      - "8080:80"
    environment:
      - DEBUG=true
    depends_on:
      db:
        condition: service_healthy
    volumes:
      - ./src:/app/src
    networks:
      - app_net
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:8080/health"]
      interval: 30s
      timeout: 10s
      retries: 3

  db:
    image: postgres:16
    environment:
      POSTGRES_PASSWORD: mypass
    volumes:
      - pgdata:/var/lib/postgresql/data
	networks:
      - app_net

volumes:
  pgdata:



networks:
  app_net:


انواع Network

| Driver    | توضیح خلاصه                                    | کِی استفاده میشه؟                     |
| --------- | ---------------------------------------------- | ------------------------------------- |
| `bridge`  | شبکه‌ی محلی مجازی بین کانتینرها روی یک ماشین   | پیش‌فرض Docker روی single-host        |
| `host`    | استفاده مستقیم از شبکه‌ی میزبان (no isolation) | نیاز به بیشترین performance           |
| `none`    | بدون هیچ شبکه‌ای                               | برای امنیت یا custom نیاز             |
| `overlay` | ایجاد شبکه بین چند ماشین (multi-host)          | فقط در **Docker Swarm** یا Kubernetes |
| `macvlan` | اتصال مستقیم به شبکه فیزیکی با MAC خاص         | وقتی نیاز داری IP مستقیم از LAN بگیری |