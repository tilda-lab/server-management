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

2026-11-11 07:46 / MacBook Pro (Apple M3 Pro) / macOS Tahoe version 26.6.1

Loin uuden käyttäjän ansible ja automatisoin kirjautumisen kohdepalvelimelle ssh-avaimella. Tämä mahdollisti komentojen suorittamisen sudo-oikeuksilla ilman jatkuvia salasanan tarkistuksia.

Sudo-oikeudet määritettiin NOPASSWD asetuksilla, 


Lopuksi toiminta testattiin ansible-ping komennolla. `ansible localhost -i host.ini -m ansible.builtin.ping` Testien perusteella SSH-yhteys ja sudo-oikeuksien käyttö toimivat ilman salasanan kysymistö.

#

b) Antero. 

#

c) Package. Pakettien asennus Ansiblella.

#

d) File. Tiedostojen käyttöoikeudet ja hallinnointi.


#

e) Jotain muuta. 


#

### Lähteet: 

Passwordless Sudo with Ansible: https://terokarvinen.com/passwordless-sudo-with-ansible/
Sudo without password: https://terokarvinen.com/passwordless-sudo/


