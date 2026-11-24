#

### a) Räpylä. Daemonin asennus.

2026-11-24 start 22:52 / MacBook Pro (Apple M3 Pro) / macOS Tahoe version 26.6.1

Prosessi aloitettu päivittämisellä `sudo apt update` ja tämän jälkeen lähdin asentamaan rsyslogia. Debianissa rsyslog on yksi syslog-protokollaa hyödyntävistä lokituspalveluista eli se vastaanottaa ja tallentaa käyttöjärjestelmän sekä sovellusten tuottamia tapahtumaviestejä. Niiden avulla voi seurata järjestelmän toimintaa ja selvittää ongelmatilanteita.

`22:56`

Yritin asennusta komennolla `sudo apt install syslogd` ja tämä ei toiminut. Antoi virheilmoituksen sekä ehdotuksen ladattavasta paketista ja kokeilin seuraavksi `sudo apt install inetutils-syslogd` Tällä asennus onnistui.

<img width="2018" height="1080" alt="2026-11-24 at 22 56 51" src="https://github.com/user-attachments/assets/e9baf356-ac71-41d3-b616-d7e05b7a2322" />


#

<img width="1980" height="490" alt="2026-11-24 at 22 57 39" src="https://github.com/user-attachments/assets/1b8e1286-5ec1-42d6-8e80-d90cd068755a" />


#

### b) Automaatti. Daemonin automatisointi Ansiblella.



#

### Lähteet:

Wikipedia. List of Unix daemons. Luettavissa: https://en.wikipedia.org/wiki/List_of_Unix_daemons Luettu 24.11.2026.

Debian. Man-pages. Syslogd. Luettavissa: https://manpages.debian.org/testing/inetutils-syslogd/syslogd.8.en.html Luettu 24.11.2026

Free Code Camp. The Syslog Handbook – How to Collect and Redirect Logs to a Remote Server. Luettavissa: https://www.freecodecamp.org/news/what-is-syslog-handbook/ Luettu 24.11.2026.

Rsyslog. https://www.rsyslog.com Luettu 24.11.2026
