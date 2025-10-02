<img width="938" height="333" alt="Screenshot 2025-09-26 114609" src="https://github.com/user-attachments/assets/9807879f-e895-4bd4-b72f-60e970c7c56e" />

Үр дүн: зөвхөн 22/tcp (ssh) илэрсэн.

<img width="942" height="371" alt="Screenshot 2025-09-26 114618" src="https://github.com/user-attachments/assets/57618dcc-64b3-453a-bbc9-adbb2ba85b81" />

Ихэнхдээ IKE Main Mode handshakе ийг буцааж өгсөн:

SA=(Enc=3DES Hash=SHA1 Group=2:modp1024 Auth=PSK ...) 


→ peer нь pre-shared key (PSK) шаарддаг бөгөөд 3DES+SHA1 ашиглаж байна — орчин үеийн стандартын хувьд сул.

Vendor ID-ууд (XAUTH, Dead Peer Detection) мөн илэрсэн. Vendor ID ба XAUTH байгааг харсан тул Aggressive Mode-ыг туршиж, танигч (identity) ба PSK-ийн материал гоос мэдээлэл цуглуулахыг оролдсон.

<img width="946" height="425" alt="Screenshot 2025-09-26 120640" src="https://github.com/user-attachments/assets/6960d900-1387-4da6-a6ff-963b7836982d" />

Дараа нь оффлайн (dictionary) довтолгоо хийсэн:

psk-crack -d /usr/share/wordlists/rockyou.txt hash.txt

Гарсан үр дүн: PSK нь freakingrockstarontheroad гэж crack болсон.

<img width="621" height="352" alt="Screenshot 2025-09-26 124046" src="https://github.com/user-attachments/assets/99a99487-aec5-4a66-ae3e-67b27d630361" />

User флагийг авах

Системд орсны дараа даруй user флагийг авсан:

ike@expressway:~$ cat user.txt

<img width="358" height="107" alt="Screenshot 2025-09-26 124144" src="https://github.com/user-attachments/assets/9b6393a1-fc50-4028-9f40-21707e3885ff" />

sudo version-г шалгасан.

<img width="563" height="488" alt="Screenshot 2025-09-26 124318" src="https://github.com/user-attachments/assets/e5ff6c88-e328-4164-8d43-8f9edd3efa96" />


<img width="380" height="200" alt="Screenshot 2025-09-26 124432" src="https://github.com/user-attachments/assets/af0abdaa-040d-4b5b-b82c-f0eff6f48e57" />

