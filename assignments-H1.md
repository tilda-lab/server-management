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

### d) Hei Ansible.

2026-11-03 21:47 / MacBook Pro (Apple M3 Pro) / macOS Tahoe version 26.6.1

Ansible on avoimen lähdekoodin automaatiotyökalu, jolla voidaan hallita ja konfiguroida palvelimia sekä suorittaa komentoja etänä. Yhteyden muodostamiseen käytetään SSH-protokollaa. Ansible käyttää YAML-muotoisia playbook-tiedostoja, joihin määritellään suoritettavat tehtävät. Lisäksi kohdekoneet listataan inventory-tiedostoon.

Harjoituksessa asensin Ansiblen Debianiin ja kokeilin sen toimintaa SSH-yhteyden kautta paikalliseen koneeseen (localhost).

<img width="1662" height="694" alt="ansible-harjoitus" src="https://github.com/user-attachments/assets/1c875a7f-19c5-4724-bb5e-352b5c2583b8" />

#

<img width="1728" height="460" alt="python-warning" src="https://github.com/user-attachments/assets/08ccad6a-28fe-43ee-807a-a1af817bbe73" />

Pythoniin liittyvän varoituksen poistaminen opettajan ohjeilla (Karvinen, 2026).

```yaml
[all:vars]
ansible_python_interpreter=/usr/bin/python3
```

<img width="1810" height="692" alt="python-warning-korjattu" src="https://github.com/user-attachments/assets/50e51849-8a7d-4b28-bebe-215f52ba5b7c" />


#

### Lähteet

Tero Karvinen. SSH public key - Login without password. Luettavissa: https://terokarvinen.com/ssh-public-key-login-without-password/ Luettu: 3.11.2026

Tero Karvinen. Hello Ansible. Luettavissa: https://terokarvinen.com/hello-ansible/ Luettu: 3.11.2026

SSH Academy. How to Use ssh-keygen to Generate a New SSH Key? Luettavissa: 
https://www.ssh.com/academy/ssh/keygen Luettu: 3.11.2026

Red Hat. What is YAML? Luettavissa: https://www.redhat.com/en/topics/automation/what-is-yaml Luettu: 3.11.2026


