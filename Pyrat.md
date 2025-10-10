<img width="1253" height="667" alt="image" src="https://github.com/user-attachments/assets/54eae20d-e1aa-4e54-aa03-bdb4dfff12fe" />

онгорхой байгаа 8000 порт

<img width="457" height="125" alt="image" src="https://github.com/user-attachments/assets/08470e20-3b83-4eb6-9e44-18b3676feb04" />

ман ямар ч /dir бичсэн зөвхөн ийшээ redirect хийсэн.

<img width="425" height="320" alt="image" src="https://github.com/user-attachments/assets/68f656ec-cb56-4cac-a313-e5e594fe6aec" />

үүн дээр хэлсэн шиг хамгийн энгийн connection буюу telnet ашиглаж үзсэн.

энэхүү холболтоос болон description хархад нэг төрлийн python jail байна.
үүн дээр python reverse shell туршиж үзсэн.

<img width="1354" height="503" alt="image" src="https://github.com/user-attachments/assets/b83ae56d-bab9-4c1f-8af5-c2ac58b05899" />



<img width="544" height="511" alt="image" src="https://github.com/user-attachments/assets/25d833af-20d5-46d2-ab78-5df32b2296fd" />

<img width="671" height="295" alt="image" src="https://github.com/user-attachments/assets/d28b6af2-d469-413d-98d6-a6477a2f0db4" />

<img width="671" height="123" alt="image" src="https://github.com/user-attachments/assets/e73b5d5e-193c-4314-a239-d8561e7eecaf" />

<img width="631" height="417" alt="image" src="https://github.com/user-attachments/assets/650fad8b-3964-47f1-8dda-3ca59c37d2c8" />

<img width="654" height="436" alt="image" src="https://github.com/user-attachments/assets/da3baab2-6b9b-4017-a4d2-9fcd3daca856" />

<img width="573" height="411" alt="image" src="https://github.com/user-attachments/assets/3b04ba96-0de1-4c7c-9dee-b7a1ac757992" />

дүгнэлт
Python SimpleHTTP (порт 8000) ашиглан pyrat төрлийн интерактив Python "jail"/консоль нээлттэй ажиллаж байсан. Тус сервис нь удирдлагын (admin) команд эсвэл shell гэсэн команд хүлээн авч, хэрэв админ эрхтэй холболт бол root шэлл олгож чадаж байна уу гэдгээ шалгадаг. Тухайн системд /opt/dev/.git/config файлд think хэрэглэгчийн Git credential (username=think, password=_TH1NKINGPirate$_) нээлттэй байсан тул тэдгээрийг ашиглан админын консол руу нэвтэрч, дараа нь нууц үг давтан туршилтаар (bruteforce/try) abc123 -ийг олж admin-аар бүрэн root шэлл авсан. Эцэст нь root эрхээр root.txt файлыг уншиж чадсан.
сэргийлэх
Тус машины 8000 порт дээр ажиллаж буй сервисийг зогсоох (хэрвээ production биш, шалгах бол)
sudo systemctl stop <service> эсвэл хэрвээ script бол процессыг /bin/kill-ээр зогсооно.
Хэрэглэгдэж буй админ/репо credential-уудыг даруй солих — think болон admin-ын нууц үгийг систем дээр болон GitHub/QA систем дээр шууд сольж, тухайн credential-ыг даруй устгана.
Энэ credential-ыг агуулсан файлыг устгах: /opt/dev/.git/config-ийг устгах, commit түүхээс салгах (гаргууд арга: git filter-repo эсвэл git filter-branch), эсвэл репог public биш сервер рүү шилжүүлэх.
Дараалал болон нэвтрэлтүүдийг шалгах (audit): /var/log/auth.log, web service logs, bash history-г шалгана. Хэн, хэзээ нэвтэрсэн, ямар IP-ууд холбогдсон гэдгийг тэмдэглэх.
Плаги/бид тогтоосон backdoor/unknown accounts-ыг шалгах — /etc/passwd, /etc/sudoers-ийг шалгаад сэжигтэй хэрэглэгчийг устгах.
Хэрэв боломжтой бол машин дээрээс бүрэн rebuild/restore хийх — compromised server-г rebuild хийх нь хамгийн баталгаатай шийдэл.
