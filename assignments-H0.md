#

### x) Lue artikkelit ja tiivistä muutamalla lauseella

https://github.com/AONCODES/linux-course/blob/main/h4.md

- Niemen raportin aiheena oli tunnilla käsitellyt asiat virtuaalipalvelimesta
- Tekstissä käytiin yksityiskohtaisesti läpi kuvakaappausten avulla UpCloudin tarjoaman virtuaalipalvelun vuokraus ja asennus
- Raporttiin on kirjattu työvaiheet selkeästi ja lisäksi Niemi esittelee käyttämänsä komennot yksityiskohtaisesti

https://partanennn.github.io/linux-servers/practices/fifth-week.html

- Partasen raportti käsitteli domainin hankintaa ja hän oli valinnut palveluntarjoaksi Namecheapin
- Raportissa on myös ohjeet domainin osoittamisesta virtuaalipalvelimelle

#

### a) Debianin asennus virtuaalikoneelle 

2026-10-25 / asennuksen aloitusaika 15:24 / MacBook Pro (Apple M3 Pro) / macOS Tahoe version 26.6.1

#

<img width="1950" height="1228" alt="debian-000" src="https://github.com/user-attachments/assets/a829e314-7681-4ede-889b-998abc9a31a0" />

Olen aikaisemmilla kursseilla asentanut Ubuntun serverin virtuaalikoneelle muutaman kerran, mutta asennusprosessi vaati hieman kertausta ennen uuden Linux-jakelun asentamista. Aloitin varmistamalla valitsemani asennuspaketin soveltuvuuden käyttämälleni laitteelle. Tämän jälkeen latasin asennustiedoston Debianin virallisilta verkkosivuilta. MacBookilleni sopiva asennusmedia oli Debian 13.7.0:n ARM64-arkkitehtuurille tarkoitettu verkkoasennuslevykuva (debian-13.7.0-arm64-netinst.iso)

#

<img width="1168" height="1586" alt="debian-002" src="https://github.com/user-attachments/assets/a4923281-3345-4444-938e-0e08a2c46979" />

Debian asennettu onnistuneesti virtuaalikoneelle.

#

### b) VPS-virtuaalipalvelimen vuokraaminen

2026-10-25 17:10

Vuokrasin virtuaalipalvelimen UpCloudilta. Palveluntarjoajan valintaan vaikuttivat tarjolla ollut ilmainen kokeilujakso sekä mahdollisuus sijoittaa palvelin suomessa sijaitsevaan datakeskukseen. Hinta on myös erittäin kohtuullinen 3e kuukaudessa kokeilujakson päätyttyä.

2026-10-25 17:42

Luotu ssh-avain onnistuneesti komennolla `ssh-keygen -t ed25519 -C "debian-upcloud`


#

### Lähteet

SSH Academy. How to Use ssh-keygen to Generate a New SSH Key? Luettavissa: https://www.ssh.com/academy/ssh/keygen Luettu: 25.10.2026

AONCODES. Kotitehtäväraportti. https://github.com/AONCODES/linux-course/blob/main/h4.md Luettu: 25.10.2026

Linuxize. Usermod command in Linux. Luettavissa: https://linuxize.com/post/usermod-command-in-linux/ Luettu: 25.10.2026

Linuxize. How to Set Up a Firewall with UFW on Debian 10. Luettavissa: https://linuxize.com/post/how-to-setup-a-firewall-with-ufw-on-debian-10/ Luettu: 25.10.2026

#












