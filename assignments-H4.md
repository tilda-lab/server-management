#
x) Karvinen 2023: Configuration Management of Distributed Systems over Unreliable and Hostile Networks (pdf, ̣mirrors: local, archive.org), vain nämä kohdat:
	▪	4.12.1 Size and Complexity of Some DSLs (112. Ominaisuuksien määrä.)
	▪	4.12.2 Use of DSL Functions in Case Configuration (112-115. Mitä oikeasti käytetään.)
	▪	4.12.3.1 Dependencies Between Main Functions (115-117. Tärkeimmät rakennuspalikat.)

  - Tekstissä käsitellään modernia konfigurointia ja ohjelmien riippuvuuksia sekä eri  kielien eroavaisuuksia
  - Idempotentti eli saman toiminnon voi suorittaa useita kertoja ja lopputulos pysyy aina samana
    

a) Räpylä. Daemonin asennus.

2026-11-24 start 22:52 / MacBook Pro (Apple M3 Pro) / macOS Tahoe version 26.6.1

Prosessi aloitettu päivittämisellä `sudo apt update` ja tämän jälkeen lähdin asentamaan rsyslogia. Debianissa rsyslog on yksi syslog-protokollaa hyödyntävistä lokituspalveluista eli se vastaanottaa ja tallentaa käyttöjärjestelmän sekä sovellusten tuottamia tapahtumaviestejä. Niiden avulla voi seurata järjestelmän toimintaa ja selvittää ongelmatilanteita.

`22:56`

Yritin asennusta komennolla `sudo apt install syslogd` ja tämä ei toiminut. Antoi virheilmoituksen sekä ehdotuksen ladattavasta paketista ja kokeilin seuraavksi `sudo apt install inetutils-syslogd` Tällä asennus onnistui.

<img width="2018" height="1080" alt="2026-11-24 at 22 56 51" src="https://github.com/user-attachments/assets/e9baf356-ac71-41d3-b616-d7e05b7a2322" />


#

<img width="1980" height="490" alt="2026-11-24 at 22 57 39" src="https://github.com/user-attachments/assets/1b8e1286-5ec1-42d6-8e80-d90cd068755a" />


#

b) Automaatti. Daemonin automatisointi Ansiblella.

2026-11-24 start 23:15 / MacBook Pro (Apple M3 Pro) / macOS Tahoe version 26.6.1

Pieniä teknisiä haasteita ja tehtävät jäivät jumiin. Täydennän ja palaan raportointiin.

<img width="1338" height="354" alt="2026-11-24 at 23 15 58" src="https://github.com/user-attachments/assets/af9fff1e-c031-46bc-ba2a-076d79b626ed" />

<img width="1984" height="614" alt="2026-11-24 at 23 16 14" src="https://github.com/user-attachments/assets/86ad7260-3128-4e23-b15f-acb370152ee2" />

<img width="2014" height="872" alt="2026-11-24 at 23 32 08" src="https://github.com/user-attachments/assets/2cd78993-fefb-4096-9565-ed38f5d0f016" />

#

Lähteet:

Wikipedia. List of Unix daemons. Luettavissa: https://en.wikipedia.org/wiki/List_of_Unix_daemons Luettu 24.11.2026.

Debian. Man-pages. Syslogd. Luettavissa: https://manpages.debian.org/testing/inetutils-syslogd/syslogd.8.en.html Luettu 24.11.2026

Free Code Camp. The Syslog Handbook – How to Collect and Redirect Logs to a Remote Server. Luettavissa: https://www.freecodecamp.org/news/what-is-syslog-handbook/ Luettu 24.11.2026.

Rsyslog. https://www.rsyslog.com Luettu 24.11.2026

#

edit. 2026-11-28 start 10:55 / MacBook Pro (Apple M3 Pro) / macOS Tahoe version 26.6.1

a) Ensimmäisenä tarkistin asentamani syslog-daemonin tilan komennolla `systemctl status rsyslog` ja tämä palautti ilmoituksen "Unit rsyslog.service could not be found" Kokeilin seuraavaksi `systemctl status syslog`, joka osoitti palvelun olevan aktiivinen (active). Tämän perusteella totesin asentaneeni rsyslogin sijaan toisen syslog-toteutuksen. Kyseessä on Inetutils-ohjelmistokokoelmaan kuuluva syslog-daemon.

<img width="1159" height="325" alt="2026-11-28 at 11 07 35" src="https://github.com/user-attachments/assets/858f3602-8f63-4ec4-97f3-15372af2a138" />

#

Tarkistin vielä asennetun ohjelmistopaketin tiedot paketinhallintatyökalulla. Käytin komentoa `dpkg -l | grep inetutils`, joka listaa annettuun hakusanaan liittyvät paketit.

<img width="1229" height="63" alt="2026-11-28 at 11 17 08" src="https://github.com/user-attachments/assets/ca73ae73-c66e-4c5e-ba47-231266373a2c" />
