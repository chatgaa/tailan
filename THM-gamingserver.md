<img width="1913" height="1007" alt="Screenshot From 2025-10-09 12-06-14" src="https://github.com/user-attachments/assets/26d49f07-074e-4b97-b907-357d70afac6e" />



<img width="976" height="530" alt="image" src="https://github.com/user-attachments/assets/1367cc63-4857-4423-bede-58b877fb1ac0" />

Нээлттэй Port:

<img width="1042" height="573" alt="image" src="https://github.com/user-attachments/assets/efca1fe1-abec-47f7-b490-1b64ddbeca1b" />



<img width="572" height="557" alt="image" src="https://github.com/user-attachments/assets/df906d82-406d-41b9-a9bd-b893f625e897" />


 pas

<img width="694" height="509" alt="image" src="https://github.com/user-attachments/assets/e0b59fef-9575-428c-abb6-52411bf13b24" />

john-the-ripper формат руу хөрвүүлэх

<img width="815" height="509" alt="image" src="https://github.com/user-attachments/assets/0d2ad497-23c4-40e9-938f-a429cf25b8e4" />

Нууц үгийг (passphrase) цөмлэх

<img width="817" height="848" alt="image" src="https://github.com/user-attachments/assets/9c5c56d2-8fb4-4991-a468-756a5be5c508" />

Цохилтыг дуусгаад баталгаажуулах:
john хэрэглэгчээр машиныг нэвтэрсний дараа user.txt файлыг хайж, уншсан:

Root эрх олж авах — LXD ашиглан

id командаар хэн ямар бүлэгт байгааг шалгахдаа lxd бүлэгт байгааг олсон. LXD бүлгийн гишүүн бол контейнерын тохиргоо дамжуулж, хостаас root эрх авахад ашиглагддаг учраас аюултай.

🧠 Яагаад LXD аюултай вэ?

lxd бүлэгт байгаа хүн төрийн контейнер үүсгэн, түүнд хостаас root файлов системийг mount хийнэ — ингэснээр контейнер доторх процессыг ашиглан хостийн файл систем дээр root эрхтэй ажиллах боломж гарна.

<img width="956" height="264" alt="Screenshot From 2025-10-09 12-58-52" src="https://github.com/user-attachments/assets/7c626a35-d60e-4464-98c0-2c2fe05ac11f" />

Өөрийн машин дээр lxd-alpine-builder скриптийг ашиглан Alpine Linux image үүсгэсэн:

<img width="770" height="576" alt="Screenshot From 2025-10-09 13-00-23" src="https://github.com/user-attachments/assets/d8261ce8-c367-40ee-a0e2-f3d076307f11" />



Image-ийг хохирогч руу илгээхийн тулд энгийн HTTP сервер ажиллуулсан:

<img width="767" height="157" alt="Screenshot From 2025-10-09 13-00-31" src="https://github.com/user-attachments/assets/3621edb6-103a-4b17-a359-a2519eab08f4" />

Дараах командын дарааллыг ашиглан:

image импортлох

privilege-тэй контейнер initialize хийх

хостын root-ийг контейнер руу mount хийх

контейнерийг ажиллуулж root shell авах

<img width="1213" height="548" alt="Screenshot From 2025-10-09 13-13-24" src="https://github.com/user-attachments/assets/582a7362-0f77-45f0-9f18-8778d931d1cd" />


