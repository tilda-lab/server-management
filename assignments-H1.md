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

<img width="1682" height="674" alt="debiansshpalvelin" src="https://github.com/user-attachments/assets/e0c33424-d0d5-4ecf-8c90-44761f73f0ab" />


#

### c) Pubkey. Kirjautumisen automatisointi.

2026-11-03 21:16 / MacBook Pro (Apple M3 Pro) / macOS Tahoe version 26.6.1

SSH-avainpari luodaan komennolla `ssh-keygen` käyttäen ed25519-algoritmia. Kopioin julkisen avaimen paikalliselle SSH-palvelimelle komennolla `ssh-copy-id tilda@localhost` Tämän jälkeen testasin kirjautumista komennolla `ssh tilda@localhost` Tämä toimi ongelmitta ja kirjautuminen ilman salasanaa onnistui.

<img width="1576" height="802" alt="debiansshpubkey" src="https://github.com/user-attachments/assets/2e8460b5-66cd-4927-beb8-c060ec3218c1" />

#

### Lähteet


