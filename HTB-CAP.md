HTB-CAP

<img width="950" height="574" alt="Screenshot From 2025-10-06 13-12-54" src="https://github.com/user-attachments/assets/74f0f34c-9944-4924-a575-44afa3db60d5" />

Port 21,22,80 нээлттэй байсан

<img width="1915" height="816" alt="Screenshot From 2025-10-06 13-28-06" src="https://github.com/user-attachments/assets/9f59ecf9-b672-4dca-b109-2cabd485e017" />

<img width="1639" height="768" alt="image" src="https://github.com/user-attachments/assets/e1d8671a-bc2f-42c0-b895-b7c806010d6b" />

<img width="1245" height="153" alt="image" src="https://github.com/user-attachments/assets/432ce77a-4c1d-4e3e-acf0-300ad49f9e93" />

Татсан .pcap файлыг Wireshark-д нээж шинжилсэн. Тэндээс nathan хэрэглэгчийн нэвтрэх (login) нууц үг олдсон:

<img width="658" height="183" alt="image" src="https://github.com/user-attachments/assets/1665ddd2-0fba-4b89-a21a-b06857f6e200" />

ssh-ээр хандаж user.txt авсан

<img width="657" height="443" alt="Screenshot From 2025-10-07 00-16-00" src="https://github.com/user-attachments/assets/487e208f-86c9-4649-b9a1-38321ead9df7" />

<img width="957" height="949" alt="Screenshot From 2025-10-07 00-17-38" src="https://github.com/user-attachments/assets/fbbdcab8-fdf9-465d-a004-44f0e56e6fa6" />

Эндээс python3.8 нь cap_setuid чадварыг (capability) агуулж байгааг харсан — энэ нь хэрэглэгчийн ID-г (uid) өөрчилж root эрх авахад ашиглагдаж болно.

<img width="957" height="949" alt="Screenshot From 2025-10-07 00-18-15" src="https://github.com/user-attachments/assets/1c188f25-2737-4244-b667-acce624eb27b" />



<img width="683" height="322" alt="Screenshot From 2025-10-07 00-23-52" src="https://github.com/user-attachments/assets/162b9e20-218a-48b9-9bb2-80e7e404a75e" />

<img width="648" height="55" alt="Screenshot From 2025-10-07 00-25-10" src="https://github.com/user-attachments/assets/a9dbbaa9-88fa-48c7-ac3b-acf9ec92081e" />

Энэ комманд os.setuid(0) дуудах замаар процессийн uid-ийг 0 (root) болгоод интерактив bash shell эхлүүлдэг. Ингэснээр би root shell авч root флагийг олж авсан.

<img width="645" height="108" alt="Screenshot From 2025-10-07 00-25-34" src="https://github.com/user-attachments/assets/78a521e3-47e3-4042-9506-bd762538be8c" />
