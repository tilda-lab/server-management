x)





a) Apassi. Apache 2 asennus.

2026-11-18 start 6:48 / MacBook Pro (Apple M3 Pro) / macOS Tahoe version 26.6.1

Aloitin Apache 2 asennuksen tarkistamalla päivitykset `sudo apt update` ja tämän jälkeen suoritin asennuksen komennolla `sudo apt install apache2`

<img width="1038" height="524" alt="2026-11-18 at 6 51 07" src="https://github.com/user-attachments/assets/7d88d03f-5627-4e2c-b2c0-665b27c5d99a" />

Testasin asennuksen onnistumisen `sudo systemctl status apache2` ja lisäksi varmistin toimivuuden curl-komennolla. `curl http://localhost` hakee URL-osoitteen HTML-sisällön ja tulostaa sen terminaaliin. 

<img width="1062" height="364" alt="2026-11-18 at 6 52 34" src="https://github.com/user-attachments/assets/d9ac1b49-2099-40bb-896e-11722c33499a" />

<img width="1080" height="423" alt="2026-11-18 at 6 59 16" src="https://github.com/user-attachments/assets/9607c181-243f-451e-baa5-d66da2edf68b" />

Näiden testien lisäksi kokeilin avata asennussivua virtuaalikoneen ulkopuolella. Hain ip-osoitteen `hostname -I` komennolla ja sain tulokseksi yksityisen ip-osoitteen. Tarkistin virtuaalikoneen verkkoasetukset ja verkkosovittimena oli NAT eli Network Address Translation, suomeksi osoitteenmuutos. Virtuaalikone käytti siis tietokoneeni verkkoyhteyttä ja verkkoliikenne oli yksisuuntaista virtuaalikoneelta ulos. Vaihtamalla asetuksen siltayhteydeksi eli Bridged Adapter -asetukseen virtuaalikone näkyy verkossa omana laitteena. 

<img width="947" height="468" alt="2026-11-18 at 7 01 16" src="https://github.com/user-attachments/assets/adcfebaf-639f-4f0c-ae47-edf6d6fb56ba" />

#

`07:04`Asetusten muuttamisen jälkeen verkkosivu toimi odotetusti ja asennus suoritettu onnistuneesti.

<img width="1226" height="669" alt="2026-11-18 at 7 04 31" src="https://github.com/user-attachments/assets/b316dcfc-92ee-4849-91e7-79982b6e1cce" />

#

b) Moottorix. Nginx asennus.

2026-11-18 start 7:53 / MacBook Pro (Apple M3 Pro) / macOS Tahoe version 26.6.1

Varmistin alkuun päivitykset ja tämän jälkeen asensin Nginx -paketin komennolla `sudo apt install nginx` 

<img width="959" height="353" alt="2026-11-18 at 7 58 13" src="https://github.com/user-attachments/assets/0b3c8867-1b30-4628-9705-21338d4b3a0c" />

Testasin komennolla `sudo systemctl status nginx` ja sain ilmoitukse.

<img width="1260" height="436" alt="2026-11-18 at 8 00 36" src="https://github.com/user-attachments/assets/626654ba-ed6f-4aa0-a7d1-7fa3f0e25668" />



<img width="1153" height="605" alt="2026-11-18 at 8 11 39" src="https://github.com/user-attachments/assets/c38dfb06-b9fe-4b69-9f2a-792761147388" />



#

##### Lähteet:

Tero Karvinen. Apache installed with Ansible - quick notes. Luettavissa: https://terokarvinen.com/apache-ansible/ Luettu 18.11.2026

Ansible Community Documentation. Luettavissa:
https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_handlers.html Luettu 18.11.2026

