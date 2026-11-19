# BUG-11: «Хуучин хувилбар» линк 500 Internal Server Error буцаадаг

Орчин:  Уншлагын жагсаалт v2.0, Brave 157.1.99.57 (Chromium; headless, DevTools Protocol-оор удирдсан), Ubuntu 26.04.1 LTS, 2026-11-19
Урьдчилсан нөхцөл: `node app.js`-ийг шинээр асаасан (анхны 3 ном), http://localhost:3000 нээсэн (цонхны өргөн 1280px)

## Дахин гаргах алхам

1. http://localhost:3000 хуудсыг нээ.
2. Хуудасны доод талын «Хуучин хувилбар» линк дээр дар.
3. (API) `curl -i localhost:3000/old`

Хүлээгдэж байсан: «Бүх хуудас, линк ажиллана.»

Бодит үр дүн:     `/old` хуудсанд зөвхөн «Internal Server Error» текст гарна; `curl -i` → `HTTP/1.1 500 Internal Server Error`. Сервер унахгүй (дараагийн хүсэлт 200).

Ноцтой байдал: Major — хуудасны линк бүрэн ажиллахгүй, серверийн дотоод алдаа хэрэглэгчид шууд харагдана.

Хавсралт:      [`screenshots/bug-11.png`](../screenshots/bug-11.png) · [`evidence/bug-11-curl.txt`](../evidence/bug-11-curl.txt)

Олдсон аялал:  Charter-ийн «линкүүд» хэсэг (Supermodel аяллын төгсгөлд)

![BUG-11](../screenshots/bug-11.png)
