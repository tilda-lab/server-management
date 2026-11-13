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

Loin uuden käyttäjän ansible ja automatisoin kirjautumisen kohdepalvelimelle ssh-avaimella. Tämä mahdollisti komentojen suorittamisen sudo-oikeuksilla ilman jatkuvia salasanan tarkistuksia.

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
edit. 2026-11-13 start 8:30 / MacBook Pro (Apple M3 Pro) / macOS Tahoe version 26.6.1
Uusinta H2-osion tehtävistä.

a) Sudoless.

Loin uuden käyttäjän nimellä antero ja automatisoin kirjautumisen ssh-avaimella.

bash
sudo adducer antero
sudo grouped sudoless
sudo adducer antero sudoless


#
[8:56]
 <img width="1393" height="612" alt="2026-11-13 at 8 56 39" src="https://github.com/user-attachments/assets/297ce8f3-1699-4575-9f6e-2431c7a1384d" /> 
#
[8:59]
<img width="1094" height="122" alt="2026-11-13 at 8 59 29" src="https://github.com/user-attachments/assets/94da2eac-ed99-4658-88f5-1e66c367d735" />


