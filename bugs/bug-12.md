# BUG-12: API буруу JSON биетэй POST-д 400 биш 200 {"result":"OK"} буцаадаг

Орчин:  Уншлагын жагсаалт v2.0, Brave 157.1.99.57 (Chromium; headless, DevTools Protocol-оор удирдсан), Ubuntu 26.04.1 LTS, 2026-11-19
Урьдчилсан нөхцөл: `node app.js`-ийг шинээр асаасан (анхны 3 ном), http://localhost:3000 нээсэн (цонхны өргөн 1280px)

## Дахин гаргах алхам

1. `node app.js`-ийг шинээр асаа.
2. `curl -i -X POST localhost:3000/api/books -H 'Content-Type: application/json' -d '{"title": "Эвдэрсэн",'`
3. `curl -i -X POST localhost:3000/api/books -d 'буруу оролт'`
4. `curl -i localhost:3000/api/books`

Хүлээгдэж байсан: «API: буруу JSON биетэй POST хүсэлтэд 400 алдаа буцаана.»

Бодит үр дүн:     2 ба 3-р алхам хоёулаа `HTTP/1.1 200 OK` `{"result":"OK"}`. 4-р алхамд 3 бичлэг хэвээр — сервер хүсэлтийг чимээгүй хаясан ч клиентэд «амжилттай» гэж хэлсэн.

Ноцтой байдал: Major — API-ийн клиент алдаагаа мэдэх боломжгүй; хэрэглэгчийн өгөгдөл алдааны мессежгүйгээр алдагдана.

Хавсралт:      [`evidence/bug-12-curl.txt`](../evidence/bug-12-curl.txt)

Олдсон аялал:  Saboteur
