# BUG-13: POST /api/books-д JSON `null` илгээхэд сервер бүхэлдээ унадаг

Орчин:  Уншлагын жагсаалт v2.0, Brave 157.1.99.57 (Chromium; headless, DevTools Protocol-оор удирдсан), Ubuntu 26.04.1 LTS, 2026-11-19
Урьдчилсан нөхцөл: `node app.js`-ийг шинээр асаасан (анхны 3 ном), http://localhost:3000 нээсэн (цонхны өргөн 1280px)

## Дахин гаргах алхам

1. `node app.js`-ийг шинээр асаа (терминалд «Уншлагын жагсаалт: http://localhost:3000»).
2. `curl -i -X POST localhost:3000/api/books -H 'Content-Type: application/json' -d 'null'`
3. `curl -i localhost:3000/` (эсвэл хөтчөөр хуудсыг сэргээ).

Хүлээгдэж байсан: Буруу биед 400 алдаа буцааж, сервер үргэлжлэн ажиллана (эрүүл ухаан + «буруу JSON биетэй POST хүсэлтэд 400»).

Бодит үр дүн:     2-р алхам → `curl: (52) Empty reply from server`; node процесс терминалд `TypeError: Cannot read properties of null (reading 'title')` хэвлээд exit code 1-ээр гарна. 3-р алхам → `curl: (7) Failed to connect to localhost port 3000`; хөтөч хуудсыг нээж чадахгүй. `node app.js`-ийг гараар дахин асаах хүртэл үйлчилгээ зогсох бөгөөд дахин асаахад санах ойн бүх нэмсэн ном алдагдана.

Ноцтой байдал: Critical — нэвтрэлтгүй ганц хүсэлт бүх хэрэглэгчийн үйлчилгээг зогсоож, бүх өгөгдлийг устгадаг (DoS).

Хавсралт:      [`evidence/bug-13-curl.txt`](../evidence/bug-13-curl.txt) · [`evidence/bug-13-server-log.txt`](../evidence/bug-13-server-log.txt)

Олдсон аялал:  Saboteur
