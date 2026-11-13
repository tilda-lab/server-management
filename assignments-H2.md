#

X) Lue ja tiivistä

Sudo without password: https://terokarvinen.com/passwordless-sudo/
- Uuden käyttäjän ja ryhmien luonti.
- Käyttöoikeuksien hallinnointi
- Muistutus hyvien salasana-käytäntöjen tärkeydestä

Passwordless Sudo with Ansible: https://terokarvinen.com/passwordless-sudo-with-ansible/
- Ansiblella komentojen suorittaminen kohdepalvelimella ilman sudon jatkuvaa salasanan kysymistä

#

a) Sudoless. 

2026-11-10 19:24 / MacBook Pro (Apple M3 Pro) / macOS Tahoe version 26.6.1

Loin uuden käyttäjän ansiblella ja automatisoin kirjautumisen kohdepalvelimelle ssh-avaimella. Tämä mahdollisti komentojen suorittamisen sudo-oikeuksilla ilman jatkuvia salasanan tarkistuksia.

Sudo-oikeudet määritettiin NOPASSWD asetuksilla, 

Lopuksi toiminta testattiin ansible-ping komennolla. `ansible localhost -i host.ini -m ansible.builtin.ping` Testien perusteella SSH-yhteys ja sudo-oikeuksien käyttö toimivat ilman salasanan kysymistö.

b) Antero. 

2026-11-11 20:48 / MacBook Pro (Apple M3 Pro) / macOS Tahoe version 26.6.1

Tehtävässä luotiin uusi käyttäjä antero ja sille lisättiin oma SSH-avain

c) Package. Pakettien asennus Ansiblella.

2026-11-11 07:48 / MacBook Pro (Apple M3 Pro) / macOS Tahoe version 26.6.1

Asennettu kaksi ohjelmistopakettia, curl ja tree.

d) File. Tiedostojen käyttöoikeudet ja hallinnointi.

Tiedostolle määritettiin omistajaksi ansible ja ryhmäksi ansibe. Käyttöoikuedet 0640 (-rw-r-----) Omistaja voi siis lukea ja muokata tiedosta, ryhmän jäsenillä lukuoikeus ja muilla ei ole tiedostoon mitään oikeuksia

e) Jotain muuta. 

Lähteet: 

Passwordless Sudo with Ansible: https://terokarvinen.com/passwordless-sudo-with-ansible/
Sudo without password: https://terokarvinen.com/passwordless-sudo/

#
edit. 2026-11-13 start 8:30 / MacBook Pro (Apple M3 Pro) / macOS Tahoe version 26.6.1 

a & b) Sudoless & Antero.

Loin uuden käyttäjän nimellä antero ja automatisoin kirjautumisen ssh-avaimella.

`08:56`

```bash
sudo adduser antero # lisää uuden käyttäjän
sudo groupadd sudoless # luo ryhmän
sudo adducer antero sudoless # lisää käyttäjänantero sudoles-ryhmään
```

 <img width="1393" height="612" alt="2026-11-13 at 8 56 39" src="https://github.com/user-attachments/assets/297ce8f3-1699-4575-9f6e-2431c7a1384d" /> 

#
Sudoers-asetuksien määrittely visudo-editorilla. Tiedostoon kirjasin sudoless-oikeudet kaikille käyttäjille = ALL ja lisäksi NOPASSWD määritteli ettei salasanaa kysytä.

`sudo visudo /etc/sudoers.d/sudoless`

`%sudoless ALL = (ALL) NOPASSWD: ALL`

#
`09:00`

```bash
ssh antero@localhost # muodostaa SSH-yhteyden
sudo -k # mitätöi aiemman tallennetun sudo-tunnistuksen
sudo echo "Hello World" # tulostaa tekstin komentoriville
```
<img width="1608" height="650" alt="2026-11-13 at 9 02 04" src="https://github.com/user-attachments/assets/e67f869b-4c90-4226-9744-8f116bcc8e7d" />

#
`09:23`

Testasin `ansible-playbook site.yml` ja sain useita virheilmoituksia. 

<img width="1574" height="998" alt="2026-11-13 at 9 26 10" src="https://github.com/user-attachments/assets/e98bd682-1c8c-4b07-bb57-b68c4cb02ecb" />

Ensimmäisenä korjasin puuttuvan salasanan. Komennosta `ansible-playbook site.yml` puuttui parametri -K eli ask-become-pass. Parametrin avulla Ansible kysyy sudo-salasanan.

`ansible-playbook site.yml -K`


<img width="1682" height="1206" alt="2026-11-13 at 9 30 30" src="https://github.com/user-attachments/assets/17e135c2-9db1-453b-8f52-b20900bfbc38" />

Toinen virheilmoitus liittyi tiedostopolun virheellisen syntaksiin.  " __ etc/sudoers.d/sudoless" Korjasin puuttuvan kauttaviivan.


`09:40` Ongelmat ratkaistu ja playbook toimi.

<img width="1692" height="1200" alt="2026-11-13 at 9 40 05" src="https://github.com/user-attachments/assets/1554d37f-8585-45a2-94f7-0fd42ca037ee" />


<img width="1656" height="290" alt="2026-11-13 at 9 59 44" src="https://github.com/user-attachments/assets/354c3e9f-a4ca-46ec-a8cd-a58b0cf5fb4e" />

#

c) Package. 

`09:59`

Määrittelin Ansiblella kahden paketin asennukset päivittämällä site.yml -tiedoston ja luomalla uuden roolin paketeille.



<img width="1656" height="290" alt="2026-11-13 at 9 59 44" src="https://github.com/user-attachments/assets/4f22b3f5-cd88-41a0-82cd-cab1907c3e3f" />

<img width="1678" height="554" alt="2026-11-13 at 10 01 57" src="https://github.com/user-attachments/assets/c7c669b5-64d7-49ef-9df3-b68fd5578527" />

<img width="1590" height="270" alt="2026-11-13 at 11 56 02" src="https://github.com/user-attachments/assets/244fa627-2cd2-4aad-8354-3fb3980ffc5f" />

#

`10:01` Paketit testattu toimiviksi.

```bash
curl -V
htop
```

<img width="1670" height="348" alt="2026-11-13 at 10 01 55" src="https://github.com/user-attachments/assets/a4b3e0e6-32c3-45ed-8e8c-46f533d2c7d5" />


<img width="1652" height="308" alt="2026-11-13 at 10 00 36" src="https://github.com/user-attachments/assets/9c4d3ed9-aee5-4e38-b638-5ab89c76def5" />

#

d) File. 

`12:21`

Loin uuden roolin files ja päivitin sen site.yml -tiedostoon. Testasin ja sain virheilmoituksen. 

<img width="1838" height="1376" alt="2026-11-13 at 12 21 28" src="https://github.com/user-attachments/assets/2875e930-da90-406a-a55b-21435c3a711d" />

```bash
käyttöoikeudet
0600 / -rw------ / omistaja (owner) saa lukea (r = read) ja muokata tiedostoja (w = write)
```


#

Lähteet: 

Passwordless Sudo with Ansible: https://terokarvinen.com/passwordless-sudo-with-ansible/
Sudo without password: https://terokarvinen.com/passwordless-sudo/


