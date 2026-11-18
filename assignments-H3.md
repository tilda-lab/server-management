x)





a) Apassi. Apache 2 asennus.

2026-11-18 start 6:48 / MacBook Pro (Apple M3 Pro) / macOS Tahoe version 26.6.1

#

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





##### Lähteet:

Ansible Community Documentation 
https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_handlers.html
