<img width="934" height="508" alt="Screenshot From 2025-10-02 15-10-34" src="https://github.com/user-attachments/assets/daa53788-71eb-4723-8d9f-19aa1bcbb181" />

22 порт (SSH) нээлттэй

80 порт (HTTP) нээлттэй

<img width="480" height="270" alt="Screenshot From 2025-10-02 15-10-19" src="https://github.com/user-attachments/assets/cd882799-7e1f-4f75-8e30-d9a95856d4f6" />

Хялбар нэвтрэлтийг хангах үүднээс hosts файлд домэйныг нэмж оруулсан:

<img width="1914" height="864" alt="Screenshot From 2025-10-02 15-14-10" src="https://github.com/user-attachments/assets/625431d9-43c5-441f-9a48-bc5a304b26ca" />

http://soulmate.htb хуудас руу нэвтэрсэндээ таних тэмдэгттэй болзоо (dating) сайт гарч ирсэн.

Бүртгэл (register), нэвтрэх (login)

Хэрэглэгчийн профайл үүсгэх

Хайлт, бусад гишүүдтэй харилцах

<img width="951" height="314" alt="Screenshot From 2025-10-02 15-17-18" src="https://github.com/user-attachments/assets/85cfbdc0-bc73-4dcd-a9b1-a00d63818233" />

dirsearch ашиглан далд фолдер/файлуудыг хайсан:

<img width="816" height="170" alt="Screenshot From 2025-10-02 15-19-51" src="https://github.com/user-attachments/assets/b41c4da2-9e87-4c89-b623-d312a9351765" />

Эдгээрээс login болон register хуудсууд нээлттэй нь довтлох боломжит цэгүүд байж магадгүйг харуулж байна. Нууцлан хадгалагдсан нөөц файлууд шууд нээлттэй олдоогүй.






<img width="540" height="168" alt="Screenshot From 2025-10-02 15-21-16" src="https://github.com/user-attachments/assets/87cb07b0-c32a-45f1-8846-ff0f18bca3a0" />

http://ftp.soulmate.htb руу орсон үед /WebInterface/login.html

CrushFTP 11.W.657 хувилбартай холбоотой мэдэгдсэн сул талыг хайхад:

CVE-2025–31161 — Authentication Bypass
Энэ сул тал нь зөвшөөрөлгүй хэрэглэгч нэмэх боломж олгохтой холбоотой байсан.

Нийтэлсэн exploit-ийг GitHub-аас хуулж ашигласан:

<img width="940" height="484" alt="Screenshot From 2025-10-02 15-24-36" src="https://github.com/user-attachments/assets/4f5a857d-c28d-47e9-864d-825466101c26" />

<img width="822" height="252" alt="Screenshot From 2025-10-02 15-25-52" src="https://github.com/user-attachments/assets/b3223112-6aad-4aec-9471-6ea1e711f3ef" />

Ийм маягаар test:admin123 хэрэглэгчийг үүсгэн веб интерфэйс рүү нэвтэрсэн.

<img width="1914" height="932" alt="Screenshot From 2025-10-02 15-27-17" src="https://github.com/user-attachments/assets/e56d2749-fc34-4a1f-b11d-2d15e78d9f6c" />

Веб интерфэйс рүү test:admin123-аар нэвтэрч, Admin → User Option хэсэгрүү орсон.

ben хэрэглэгчийн нууц үгийг өөрчлөх ажиллагаа хийсэн:

enerate random password товчны дараа үүссэн санамсаргүй нууц үгийг устгаад өөрийн хүссэн нууц (123456) оруулж Use this password дарсан.

Систем нь: Verification: User ben password successfully changed to 123456 гэж баталсан.

Save-ыг дарсан.

<img width="1979" height="368" alt="Screenshot From 2025-10-02 15-29-05" src="https://github.com/user-attachments/assets/5f6ba054-10a2-4509-8d3b-02fbc4244de1" />

Дараа нь системээс logout хийн ben:123456 дээр нэвтэрсэн.


<img width="873" height="258" alt="Screenshot From 2025-10-02 15-30-23" src="https://github.com/user-attachments/assets/7cc9e54e-d33b-4b7c-9813-7abd25c193d9" />

Эксплойт — Reverse shell авах

ben хэрэглэгчээр нэвтэрсний дараа файлуудыг судалж, боломжит директориуд:

/IT/ – IT баримт файлууд

/ben/ – хэрэглэгчийн фолдер

/webProd/ – вэб продакшн фолдер (файлын upload хийх боломжтой хэсэг)

/webProd/ руу ороод Upload сонголтыг ашиглан PentestMonkey-ын PHP reverse shell-ийг байршуулсан:

<img width="768" height="124" alt="Screenshot From 2025-10-02 15-37-30" src="https://github.com/user-attachments/assets/f36abcd2-20de-48c8-9765-021ea1a72741" />

Өөр терминал дээр listener эхлүүлсэн:

FTP вэб интерфэйсээр shell.php-г upload хийж, дараа нь хандахад:

<img width="450" height="196" alt="Screenshot From 2025-10-02 15-45-28" src="https://github.com/user-attachments/assets/9bb2dcb9-bfe0-4e75-a5b2-71dcac3f5d21" />

Reverse shell-ийг хүлээн авсан

<img width="936" height="318" alt="Screenshot From 2025-10-02 15-46-13" src="https://github.com/user-attachments/assets/2aad9e63-a211-4f6d-86b4-0ba395c43a24" />

Дараа нь linPEAS-ыг ашиглан автомат privilege escalation-ын шалгалт явуулсан.

Үүний тулд өөр компьютероос энгийн HTTP сервер асаагаад linpeas.sh-г татаж ажиллуулсан:

<img width="938" height="701" alt="Screenshot From 2025-10-02 15-54-36" src="https://github.com/user-attachments/assets/80dccb76-fc66-4cd3-aa16-c27d8b8e027b" />

cat /usr/local/lib/erlang_login/start.escript

<img width="952" height="409" alt="Screenshot From 2025-10-02 15-57-37" src="https://github.com/user-attachments/assets/bd2cd502-126d-430f-870a-87a3c937a7ec" />

<img width="952" height="409" alt="Screenshot From 2025-10-02 15-59-33" src="https://github.com/user-attachments/assets/b5819de2-8cc1-4dbb-9116-13f784f88218" />

Шинэ нээлт — Erlang SSH үйлчилгээ

linPEAS-ийн үр дүнгээс Erlang дээр суурилсан SSH үйлчилгээ нь 2222 порт дээр ажиллаж байгааг олж харсан.

ben-ийн авсан нууц үгээр localhost:2222 руу холбож үзэхэд:

<img width="580" height="126" alt="Screenshot From 2025-10-02 16-00-18" src="https://github.com/user-attachments/assets/95253aff-d79a-4247-86fb-55e2bad0fda9" />

Erlang shell-д os:cmd/1 функцээр систем команд ажиллуулж болдог ба энэ нь root эрхээр ажиллаж байв.

<img width="588" height="98" alt="Screenshot From 2025-10-02 16-03-18" src="https://github.com/user-attachments/assets/9d2a2911-dda3-4a16-b65c-ead28d58e2fa" />

Erlang shell-ээс cat /root/root.txt командыг ажиллуулан root тугийг авсан:

<img width="646" height="79" alt="Screenshot From 2025-10-02 16-03-32" src="https://github.com/user-attachments/assets/cd1392fc-68b0-4b0c-8925-d87f99e00521" />




















