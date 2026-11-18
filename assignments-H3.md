### x) Lue ja tiivistä.

Karvinen 2026: Apache installed with Ansible - quick notes. https://terokarvinen.com/apache-ansible/

- Lyhyt ja tiivis muistiinpano Apachen asentamisesta
- Sisältää hyödyllisiä esimerkkejä Ansiblella automatisoinnista sekä YAML-syntaksia
- Tekstin alussakin korostetaan sen olevan muistiinpano. Se ei siis itsessään toimi asennuksen ohjeena vaan muistin tukena sellaiselle käyttäjälle joka tietää prosessin ennalta.


Ansible Community Documentation: Handlers: running operations on change. https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_handlers.html

- Handlers on Ansiblen toiminto joka käynnistyy ainoastaan pyydettäessä tai tiettyjen ehtojen täyttyessä

'ansible-doc service'

- komento tulostaa service-moduulin dokumentaation
- MODULE on johdantokappale joka sisältää perustiedot
- enabled allitsee käynnistymistä
- name sisältää nimitiedot
- state määrittää tilan, eli käytettyjä arvoja ovat mm. start, stop, restrat
- dokumentaatiosta löytyy lisäksi käyttöesimerkit


### y)



### a) Apassi. Apache 2 asennus.

2026-11-18 start 6:48 / MacBook Pro (Apple M3 Pro) / macOS Tahoe version 26.6.1

Aloitin Apache 2 asennuksen tarkistamalla päivitykset `sudo apt update` ja tämän jälkeen suoritin asennuksen komennolla `sudo apt install apache2`

<img width="1038" height="524" alt="2026-11-18 at 6 51 07" src="https://github.com/user-attachments/assets/7d88d03f-5627-4e2c-b2c0-665b27c5d99a" />

Testasin asennuksen onnistumisen `sudo systemctl status apache2` ja lisäksi varmistin toimivuuden curl-komennolla. `curl http://localhost` hakee URL-osoitteen HTML-sisällön ja tulostaa sen terminaaliin. 

<img width="1062" height="364" alt="2026-11-18 at 6 52 34" src="https://github.com/user-attachments/assets/d9ac1b49-2099-40bb-896e-11722c33499a" />

<img width="1080" height="423" alt="2026-11-18 at 6 59 16" src="https://github.com/user-attachments/assets/9607c181-243f-451e-baa5-d66da2edf68b" />

Näiden testien lisäksi kokeilin avata asennussivua virtuaalikoneen ulkopuolella. Hain ip-osoitteen `hostname -I` komennolla ja sain tulokseksi yksityisen ip-osoitteen. Tarkistin virtuaalikoneen verkkoasetukset ja verkkosovittimena oli NAT eli Network Address Translation, suomeksi osoitteenmuutos. Virtuaalikone käytti siis tietokoneeni verkkoyhteyttä ja verkkoliikenne oli yksisuuntaista virtuaalikoneelta ulos. Vaihtamalla asetuksen siltayhteydeksi eli Bridged Adapter -asetukseen virtuaalikone näkyy verkossa omana laitteena. 

<img width="947" height="468" alt="2026-11-18 at 7 01 16" src="https://github.com/user-attachments/assets/adcfebaf-639f-4f0c-ae47-edf6d6fb56ba" />

#

`07:04`

Asetusten muuttamisen jälkeen verkkosivu toimi odotetusti ja asennus suoritettu onnistuneesti.

<img width="1226" height="669" alt="2026-11-18 at 7 04 31" src="https://github.com/user-attachments/assets/b316dcfc-92ee-4849-91e7-79982b6e1cce" />

#

### b) Moottorix. Nginx asennus.

2026-11-18 start 7:53 / MacBook Pro (Apple M3 Pro) / macOS Tahoe version 26.6.1

Varmistin alkuun päivitykset ja tämän jälkeen asensin Nginx -paketin komennolla `sudo apt install nginx` 

<img width="959" height="353" alt="2026-11-18 at 7 58 13" src="https://github.com/user-attachments/assets/b54ec933-0956-4f3c-9497-e4761fb4128d" />

Tarkistin Apachen tilan ja sammutin ohjelman komennolla `sudo systemctl stop apache2` ja testasin Nginxin suorittamalla `sudo systemctl status nginx` Asennus oli oli onnistunut, mutta ohjelma ei ollut käynnistynyt. 

<img width="1153" height="605" alt="2026-11-18 at 8 11 39" src="https://github.com/user-attachments/assets/430725a1-b989-4ec0-8cca-5624e00e48b8" />

Suoritin komennon `sudo systemctl start nginx` ja tarkistin ohjelman tilan. Sain ilmoituksen "Active (running)"

<img width="1168" height="405" alt="2026-11-18 at 8 19 23" src="https://github.com/user-attachments/assets/ac19da83-f74b-4442-a6a9-9701dfd0b109" />

Nginxin testaukseen soveltuvat samat komennot mitä käytin Apachen kohdalla.

```bash
sudo systemctl status # kertoo ohjelman tilan
curl -I http://localhost # hakee ja tulostaa terminaaliin verkkosivun otsaketiedot
```

# 

`08:54` 

Nginx asennettu ja toiminnassa.

<img width="907" height="205" alt="2026-11-18 at 8 54 37" src="https://github.com/user-attachments/assets/fd1a101d-b533-483e-adfd-0b22ab99ae27" />


#

### c) Automoottorix. Nginxin asennuksen automatisointi Ansiblella.

2026-11-18 start 09:03 / MacBook Pro (Apple M3 Pro) / macOS Tahoe version 26.6.1

Tein Nginxin automatisoinnille uuden hakemiston ja loin tarvittavat tiedostot.

<img width="882" height="299" alt="2026-11-18 at 9 33 46" src="https://github.com/user-attachments/assets/b3ef79c2-d39e-43cb-aa69-33b82a205209" />

<img width="880" height="261" alt="2026-11-18 at 9 39 15" src="https://github.com/user-attachments/assets/eb601ebb-313a-4402-90c7-96c18ac35171" />

```yaml
name: nginx # asennettava paketti
state: present # varmistaa ohjelman asennuksen
update_cache: true # päivittää paketin
service # hallitsee palvelua
state: started # käynnistää palvelun
enabled: true # automaattinen käynnistys
```
<img width="733" height="196" alt="2026-11-18 at 9 41 07" src="https://github.com/user-attachments/assets/1af91344-04db-4c53-b226-f29872141e26" />

#

```yaml
ansible-playbook -I inventory.ini site.yml -K
```

Playbookin testaus ja suorittaminen. Antoi varoituksen Pythonin versiosta ja lisäsin inventory.ini -tiedostoon `[all:vars]
ansible_python_interpreter=/usr/bin/python3 `

<img width="1166" height="376" alt="2026-11-18 at 9 46 08" src="https://github.com/user-attachments/assets/9c588abf-9583-4b6e-80cb-03dbcf55c284" />

<img width="1171" height="462" alt="2026-11-18 at 9 48 59" src="https://github.com/user-attachments/assets/de9a4b94-9fc2-42a4-9efa-1e75fc719b31" />


#

`09:48` 

Lopuksi tein vielä testin, sammutin Nginxin ja tämän jälkeen ajoin `ansible-playbook -I inventory.ini site.yml -K` Lokista voi havaita automaattisen käynnistyksen. Ohjelma siis toimii toivotusti.

<img width="1161" height="404" alt="2026-11-18 at 10 13 33" src="https://github.com/user-attachments/assets/2d80b7dd-4a39-40ff-93ab-914ed8d261b4" />

<img width="1160" height="323" alt="2026-11-18 at 10 13 50" src="https://github.com/user-attachments/assets/c6cda083-b78c-4de2-89ee-a97b973cd0c8" />

#

### Lähteet:

Tero Karvinen. Apache installed with Ansible - quick notes. Luettavissa: https://terokarvinen.com/apache-ansible/ Luettu 18.11.2026

Ansible Community Documentation. Luettavissa:
https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_handlers.html Luettu 18.11.2026

Nginx. Beginner's guide. Luettavissa: https://nginx.org/en/docs/beginners_guide.html Luettu: 18.11.2026

