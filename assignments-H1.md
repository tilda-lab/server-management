#

### x) Lue artikkelit ja tiivistä muutamalla lauseella

Karvinen 2026: SSH public key - Login without password https://terokarvinen.com/ssh-public-key-login-without-password/
- SSH Public Key todennus on salasanaton menetelmän kirjauta SSH-palvelimelle.
- Se perustuu yksityiseen ja julkiseen avaimeen. Yksityinen avain säilytetään omalla tietokoneella ja julkinen avain kopioidaan palvelimelle.
- Karvisen artikkeli käsittelee SSH yhteyden asennusta sekä avainparien luomista

  
Karvinen 2026: Hello Ansible
https://terokarvinen.com/hello-ansible/
-  Karvisen artikkeli käsittelee avoimeen lähdekoodiin perustuvan automaatiotyökalu Ansiblen asennusta ja peruskonfigurointia.
-  Ansiblella voidaan hallita ja konfiguroida useita palvelimia yhtäaikaa.
-  Ansible hyödyntää SSH yhteyttä ja erillistä ohjelmaa ei tarvitse ladata ohjattaville koneille tai palvelimille. SSH-daemoni ja Python riittävät.
-  Asetukset määritellään YAML-muotoisissa tiedostoissa, joita kutsutaan playbookeiksi.

#

### a) Debian 13

Debianin asennus raportoitu aiemmessa tehtävässä. https://github.com/tilda-lab/server-management/blob/main/assignments-H0.md

#

### b) Sshecrets. SSH-palvelimen asennus ja testaus

2026-11-03 19:43 / MacBook Pro (Apple M3 Pro) / macOS Tahoe version 26.6.1

Asensin Debian-virtuaalikoneelle OpenSSh Server ohjelmiston komennolla `sudo apt install openssh-server` ja käynnistin palvelun `sudo systemctl start ssh`

Tarkistin SSH yhteyden toimivuuden `systemctl status ssh` Tilaksi ilmoitettiin active. 

Lopuksi testasin SSH-yhteyden muodostamisen komennolla `ssh localhost`

<img width="1682" height="674" alt="debian" src="https://github.com/user-attachments/assets/7f398fd8-b0e5-41dd-82ca-14d1a6c4d461" />



