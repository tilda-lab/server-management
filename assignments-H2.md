#

### X) Lue ja tiivistä

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

##### Lähteet: 

Passwordless Sudo with Ansible: https://terokarvinen.com/passwordless-sudo-with-ansible/
Sudo without password: https://terokarvinen.com/passwordless-sudo/

#
edit. 2026-11-13 start 8:30 / MacBook Pro (Apple M3 Pro) / macOS Tahoe version 26.6.1 / uusinta H2-osion tehtävistä.

a) Sudoless.

Loin uuden käyttäjän nimellä antero ja automatisoin kirjautumisen ssh-avaimella.

#
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


`ansible-playbook site.yml`





