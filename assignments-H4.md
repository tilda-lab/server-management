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

a) Räpylä. Daemonin asennus & b) Automaatti. Daemonin automatisointi

`11:07` Ensimmäisenä tarkistin asentamani syslog-daemonin tilan komennolla `systemctl status rsyslog` ja tämä palautti ilmoituksen "Unit rsyslog.service could not be found" Kokeilin seuraavaksi `systemctl status syslog`, joka osoitti palvelun olevan aktiivinen (active). Tämän perusteella totesin asentaneeni rsyslogin sijaan toisen syslog-toteutuksen. Kyseessä on Inetutils-ohjelmistokokoelmaan kuuluva syslog-daemon.

<img width="1159" height="325" alt="2026-11-28 at 11 07 35" src="https://github.com/user-attachments/assets/858f3602-8f63-4ec4-97f3-15372af2a138" />

#

Tarkistin vielä asennetun ohjelmistopaketin tiedot paketinhallintatyökalulla. Käytin komentoa `dpkg -l | grep inetutils`, joka listaa annettuun hakusanaan liittyvät paketit.

<img width="1229" height="63" alt="2026-11-28 at 11 17 08" src="https://github.com/user-attachments/assets/ca73ae73-c66e-4c5e-ba47-231266373a2c" />

#

`11:39` Tarkistin Ansible-roolin nykyisen sisällön ja varmistin mitä tehtäviä rooli sisälsi sekä miten asennus oli määritelty. Tässä yhteydessä huomasin YAML-tiedostossa virheellisen ohjelmistopaketin (rsyslog). Koska olin asentanut Inetutilsin syslog-daemonin, korjasin tiedoston vastaamaan oikeaa ohjekmistopakettia. 

```Bash
cat roles/syslog/tasks/main.yml
nano roles/syslog/tasks/main.yml
```


<img width="1220" height="194" alt="2026-11-28 at 11 39 19" src="https://github.com/user-attachments/assets/b3bc7643-34df-4ba1-9ada-67f279f7cb94" />

#

`11:59` Ajoin Ansible-playbookin komennolla `ansible-playbook site.yml` Suoritus epäonnistui, koska Ansible ei saanut tarvittavia sudo-oikeuksia. Lisäsin parametrin -K, joka pyytää käyttäjän salasanan. Tämän jälkeen playbook suoritettiin onnistuneesti.

<img width="1259" height="533" alt="2026-11-28 at 11 59 13" src="https://github.com/user-attachments/assets/842f78d2-6006-499b-b420-87395a63e778" />

#

c) Asetus. Asetustiedoston muutokset

`12:14` Listasin paketin asentamat tiedostot ja suodatin syslogiin tai asetuksiin liittyvät polut. Listasta löysin syslog.conf -tiedoston.

```Bash
dpkg -L inetutils-syslogd | grep -E 'conf|syslog'
cat /etc/syslog.cof
```

<img width="1202" height="352" alt="2026-11-28 at 12 14 58" src="https://github.com/user-attachments/assets/3a7213ad-a140-4f9c-8070-ee5f98ccc6ec" />

<img width="1231" height="325" alt="2026-11-28 at 12 29 57" src="https://github.com/user-attachments/assets/816800ae-01a0-4085-b9df-7bc0a634027d" />

`13:14` Muokkasin syslogin asetustiedostoa ja tavoitteeni oli ohjata tietyt lokitiedot omaan lokitiedostoonsa. Ennen muutosten tekemistä kopioin alkuperäisen asetustiedoston Ansible-roolin files hakemistoon komennolla `cp /etc/syslog.conf roles/syslog/files/syslog.conf` Varmistin kopioinnin onnistumisen komennolla `ls -l roles/syslog/files` 

<img width="1211" height="81" alt="2026-11-28 at 13 17 33" src="https://github.com/user-attachments/assets/47174a74-9802-4a5e-8277-8e9d52d429c6" />

#

`14:39` Loin syslog-roolia varten oman handlers-hakemiston ja loin uuden tiedoston. Määrittelin sen käynnistämään syslog-palvelun uudelleen aina kun Ansible havaitsee asetustiedostossa muutoksia. 

```Bash
mkdir roles/syslog/handlers # loi uuden hakemiston
nano roles/syslog/handlers/main.yml # tiedoston luominen ja muokkaaminen
cat roles/syslog/handlers/main.yml # tulosti tiedoston sisällön terminaaliin
```

<img width="1251" height="295" alt="2026-11-28 at 14 39 45" src="https://github.com/user-attachments/assets/4c57a68a-6061-4785-88f9-1a2c39c469f2" />

Tarkistin playbookin syntaksin mahdollisten virheiden varalta komennolla `ansible-playbook site.yml --syntax-check` Komento palautti virheilmoituksen, joka osoitti virheen tarkan sijainnin. Virheen aiheutti puuttunut välilyönti. Korjasin syntaksivirheen ja suoritin tarkistuksen uudelleen. Tämän jälkeen playbook toimi odotetusti.

<img width="1115" height="253" alt="2026-11-28 at 14 42 17" src="https://github.com/user-attachments/assets/4a083b47-559b-4624-af3f-5a4dff06f842" />

```Bash
ansible-playbook site.yml -K
```

<img width="1242" height="428" alt="2026-11-28 at 14 43 20" src="https://github.com/user-attachments/assets/cd23b146-501d-43fe-814c-8a699c557568" />



#

Tehtävissä käytin OpenAI:n ChatGPT-tekoälyä apuna teknisten käsitteiden selventämiseen sekä Ansible-konfiguraatioiden ja syslog-daemonin toiminnan ymmärtämiseen. Työn toteutus, komentojen suorittaminen ja tulosten todentaminen on tehty itse.

#

Lähteet:

Debian. Man-pages. Syslogd. Luettavissa: https://manpages.debian.org/testing/inetutils-syslogd/syslogd.8.en.html Luettu 28.11.2026

