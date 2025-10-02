Hackthebox-codeparttwo machine

2024-28397 (js2py Sandbox Escape) сул тал дээр үндэслэсэн

<img width="942" height="769" alt="Screenshot 2025-09-25 231805" src="https://github.com/user-attachments/assets/081797ee-afa8-4558-b1c2-8d6bffb35131" />

Порт 22 — SSH нээлттэй

Порт 8000 — Gunicorn 20.0.4 нээлттэй /Gunicorn нь Nginx-ээр дамжих Python вэб апп-ыг ажиллуулдаг WSGI сервер юм./

<img width="994" height="668" alt="Screenshot 2025-09-25 234013" src="https://github.com/user-attachments/assets/c239eeee-5b28-4c71-8797-b9fd90ba712d" />

directory brute-force-г ffuf-аар гүйцэтгэсэн:

Ингээд /download директорид ZIP архив байгааг илрүүлсэн.

<img width="974" height="298" alt="Screenshot 2025-09-25 234311" src="https://github.com/user-attachments/assets/0d62153f-f924-4936-ad21-3d4c5c342fba" />


<img width="510" height="503" alt="Screenshot 2025-09-25 234701" src="https://github.com/user-attachments/assets/16870081-92a8-43e6-be94-64966f584779" />

app.py дээр /runcode маршрут байгааг олж, js2py ашиглан JavaScript-г гүйцэтгэдэгийг тогтоосон.

requirements.txt дахь заавал суух номын сангийн мөрөнд:

js2py==0.74

Эмзэг байдлын шинжилгээ

js2py-ийн уг хувилбар нь CVE-2024-28397 — sandbox-ыг тойрч гарч Python объект руу нэвтрэх боломж олгодог гэдгийг олж мэдсэн. GitHub дээр нийтэлсэн PoC (Marven11-ийн PoC)

<img width="535" height="343" alt="Screenshot 2025-09-25 235130" src="https://github.com/user-attachments/assets/100ab3bd-8da5-4453-b2ca-44b2e5f345b8" />



<img width="660" height="251" alt="Screenshot 2025-09-26 001156" src="https://github.com/user-attachments/assets/ff66936d-faee-48d3-8c13-1367551cec60" />


Эмзэг талын тухай товч:

js2py.disable_pyimport()-ийн бүрэн бус sandboxing-ийг ашиглан

Python-ийн дотоод объект загварт нэвтрэн аюултай класс (жишээ нь subprocess.Popen) руу хандаж болно

Үр дүнд нь дурын команд гүйцэтгэх боломжтой болдог

Публич PoC-ийг ашиглан буцах холболт (reverse shell) үүсгэх payload бичжээ:


<img width="1002" height="451" alt="Screenshot 2025-09-26 102709" src="https://github.com/user-attachments/assets/2c5f491b-e6e9-4845-b45e-1f32c98efd17" />

payload-г site дээр нь run хийсэн.

<img width="639" height="194" alt="Screenshot 2025-09-26 102741" src="https://github.com/user-attachments/assets/aafef71e-fa7f-4fea-aa24-b6ab11517e89" />

Payload амжилттай ажиллаж, анхны shell-ийг авсан.

<img width="630" height="357" alt="Screenshot 2025-09-26 104326" src="https://github.com/user-attachments/assets/5ca17156-5dbd-4dc6-9689-fb3510c34587" />

Системд нэвтэрсний дараа shell-ээс хэрэглэгчдийг шалгасан:

marco нэртэй хэрэглэгчийг олсон.

Flask апп-үүд ихэвчлэн instance фолдерт нууц мэдээлэл (жишээ нь hash) хадгалдаг. Тэндээс marco-гийн MD5 нууц үгийн hash-ыг илрүүлж, хаш-ийг задалж SSH нэвтрэх боломжтой нууц үг авсан.

<img width="711" height="338" alt="Screenshot 2025-09-26 104532" src="https://github.com/user-attachments/assets/7529edcb-d520-4ff1-9cfb-e8d3b07c8ac8" />

Тэндээс marco-гийн MD5 нууц үгийн hash-ыг илрүүлж, хаш-ийг задалж SSH нэвтрэх боломжтой нууц үг авсан.

<img width="821" height="278" alt="Screenshot 2025-09-26 104602" src="https://github.com/user-attachments/assets/7fff5629-0a59-421a-b651-108dd188e08d" />

гэсэнээр хэрэглэгчээр нэвтэрч, user flag-ыг авсан.

<img width="616" height="682" alt="Screenshot 2025-09-26 104736" src="https://github.com/user-attachments/assets/ec1268a0-4cfb-4390-875a-e71846f6163f" />

sudo -l
Энэ командын үр дүнд npbackup-cli бинарийг root эрхээр гүйцэтгэх эрхтэй болохыг олсон.

npbackup-cli бол Veritas NetBackup-ын бүрэлдэхүүн бөгөөд npbackup.conf тохиргооны файлыг ашигладаг. Тус файлд команд шахаж оруулснаар root эрхтэй код ажиллуулах боломж гарсан.

<img width="385" height="330" alt="Screenshot 2025-09-26 105155" src="https://github.com/user-attachments/assets/5a8cddd0-1900-43db-9a17-c611b2664cb8" />

Энэ командын үр дүнд npbackup-cli бинарийг root эрхээр гүйцэтгэх эрхтэй болохыг олсон.

npbackup-cli бол Veritas NetBackup-ын бүрэлдэхүүн бөгөөд npbackup.conf тохиргооны файлыг ашигладаг. Тус файлд муухай команд шахаж оруулснаар root эрхтэй код ажиллуулах боломж гарсан.


<img width="332" height="113" alt="Screenshot 2025-09-26 105935" src="https://github.com/user-attachments/assets/ecd2e09a-f46e-406b-a4f6-78549ecbdd80" />

Ингээд npbackup-cli-г ажиллуулж, setuid-тай bash үүсгэсэн.
Энэ нь /bin/bash-д setuid битийг тавьж, root эрхээр ажиллах боломж олгоно.


<img width="952" height="179" alt="Screenshot 2025-09-26 111757" src="https://github.com/user-attachments/assets/77b783a4-4d41-4fab-b976-53e092f2d7c4" />

/bin/bash -p

<img width="277" height="129" alt="Screenshot 2025-09-26 112352" src="https://github.com/user-attachments/assets/1f1418ad-67ca-4230-b67c-f2465c5e1eb4" />
