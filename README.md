# Apache Web-palvelimen asennus ja konfigurointi virtuaaliympäristössä

<strong> LAMP-stackin asennus </strong>

-Asennetaan Apache komennolla “sudo apt install apache2”. Annetaan oikeudet apachelle ufw palomuurin läpi. Ensin katsotaan ufw app list komennolla ”sudo ufw app list”.

-Suoritetaan secure installation komennolla ”sudo mysql_secure_installation”

![image](https://github.com/user-attachments/assets/009aee4d-3e81-4dd2-be75-6b704e4af2c6)

-Katsotaan status komennolla ”sudo ufw status”. Tämän jälkeen sallitaan Apache komennolla ”sudo ufw allow Apache”. Sitten katsotaan taas status jossa pitäisi näkyä että Apache on sallittu OpenSSH:n lisäksi.

![image](https://github.com/user-attachments/assets/5f74a8ae-ef60-4196-8579-f07061cec355)

-MySQL asennetaan komennolla ”sudo apt install mysql-server”. Kun asennus on valmis, siirrytään MySQL tietokantaan komennolla ”sudo mysql”. Sen jälkeen annetaan komento “ALTER USER ’root’@’localhost’ IDENTIFIED WITH mysql_native_password BY ’’;” “ALTER USER” 
 muokkaa olemassa olevan käyttäjän tietoja. ”’root’@’localhost’” kohdistaa muutoksen käyttäjään ’root’ joka, kirjautuu lokaalisti. ”IDENTIFIED WITH mysql_native_password” määrittää todennuslisäosan, jota käyttäjä käyttää kirjautumiseen. ”BY ’’” asettaa käyttäjän 
 salasanan.

![image](https://github.com/user-attachments/assets/08dfa3dc-710c-4167-8978-1a9f902d89aa)

-Poistutaan tietokannasta komennolla ”exit”.

-Suoritetaan secure installation komennolla ”sudo mysql_secure_installation”

![image](https://github.com/user-attachments/assets/8d06fd26-9ca5-4872-a6d7-3a288e43db5a)

-Tämän jälkeen annetaan salasana ’root’ käyttäjälle ja testataan kirjautuminen ’root’ käyttäjällä.

![image](https://github.com/user-attachments/assets/6798f933-076b-45cf-8da6-aaeb38ce3af9)

-Asennetaan PHP-paketti, jonka lisäksi tarvitaan myös php-mysql jonka avulla php kieli voi kommunikoida MYSQL -pohjaisten tietokantojen kanssa. libapache2-mod-php:n avulla Apache pystyy käsittelemään PHP-tiedostoja. Kaikki tämä komennolla ”sudo apt install php 
 libapache2-mod-php php-mysql”. Tämän jälkeen vahvistetaan PHP-versio komennolla ”php -v”.

 ![image](https://github.com/user-attachments/assets/3cb10a3e-cc31-4843-aaab-8bcd1185180e)

-Luodaan hakemisto ’vilho.harjajarvi.dy.fi’ polkuun ’/var/www/’ komennolla ”sudo mkdir /var/www/vilho.harjajarvi.dy.fi”. Tämän jälkeen määritetään hakemiston omistajuus komennolla ”sudo chown -R $USER:$USER /var/www/vilho.harjajarvi.dy.fi” muuttujalla ’$USER’, joka 
 tarkoittaa nykyistä järjestelmäkäyttäjää.

 ![image](https://github.com/user-attachments/assets/25679617-965f-41db-98b5-e02ea835dc11)

-Avataan uusi määritystiedosto Apache sites-available hakemistosta komennolla ”sudo nano /etc/apache2/sites-available/vilho.harjajarvi.dy.fi.conf”

![image](https://github.com/user-attachments/assets/c056f45e-d2e8-4703-837e-939642d9a024)

-Uusi virtual host otetaan käyttöön hyödyntämällä a2ensite:ä. Tämä suoritetaan komennolla ”sudo a2ensite vilho.harjajarvi.dy.fi”. Tämän jälkeen poistetaan Apachen olestussivusto käytöstä komennolla ”sudo a2dissite 000-default”. Tarkistetaan määritystiedoston syntaksi 
 komennolla ”sudo apache2ctl configtest”. Lopuksi ladataan Apache uudelleen ”sudo systemctl reload apache2”, jonka jälkeen muutokset tulevat voimaan.

 ![image](https://github.com/user-attachments/assets/76c0cc93-ae10-4dcb-b55a-70cf4e3467e8)

-Luodaan ’vilho.harjajarvi.dy.fi’ hakemistoon ’index.html’ -tiedosto komennolla ”touch index.html”.

![image](https://github.com/user-attachments/assets/46a57d23-db8e-4853-838f-ef01f9d73699)

-Avataan index.html tiedosto nano editorilla komennolla ”nano index.html” ja kirjotetaan pätkä HTML - koodia.

![image](https://github.com/user-attachments/assets/551a5f2f-3b1c-4ad7-a798-5ae6ee929e6c)

-Lisätään Demo-Ubuntu työasemalle /etc/hosts tiedostoon vilho.harjajarvi.dy.fi -palvelin. Komento ”sudo nano /etc/hosts”.

![image](https://github.com/user-attachments/assets/0fef6ee0-4a42-41c7-b0ce-5eefe4b019e2)

-Palvelin laitetaan kahteen kertaan, toinen ilman www -osaa, jotta sivu löytyy www kanssa, sekä ilman.
Seuraavaksi tarkastetaan selaimella, löytyykö sivusto osoitteesta vilho.harjajarvi.dy.fi.

![image](https://github.com/user-attachments/assets/b92a72a0-f891-4221-9d82-ca120c272eaf)

-Määritetään PHP tekemällä muutoksia /etc/apache2/mods-enabled/dir.conf -tiedostoon. Muutetaan järjestystä siten, että index.php tulee index.html sijaan ensimmäiseksi. Tällä tavalla tuodaan takaisin tavallinen sovellussivu. Tehdään tämä nano editorilla.

![image](https://github.com/user-attachments/assets/ce1be5bf-64a8-47ed-a4b3-902078550810)

-Kun muutokset on tehty, ladataan jälleen Apache uudelleen komennolla ”sudo systemctl reload apache2”.

-Testataan PHP-käsittely Web-palvelimella luomalla php-koodi varmistamaan, että Apache pystyy käsittelemään php-tiedostopyyntöjä. Uuden tiedoston nimeksi tulee info.php

![image](https://github.com/user-attachments/assets/cad7801c-4735-4574-a691-6f55bec7d45b)

-Tallennetaan tiedosto ja siirrytään Demo-Ubuntu työaseman selaimelle tarkistamaan näkyykö sivusto osoitteessa ’vilho.harjajarvi.dy.fi/info.php’

![image](https://github.com/user-attachments/assets/06ba4346-6347-4e12-a94d-cba8be745c0d)


-Sivusto toimii, jonka jälkeen poistetaan tiedosto komennolla ”sudo rm var/www/vilho.harjajarvi.dy.fi/info.php”, koska tiedosto sisältää tietoja jotka voivat johtaa tietoturvariskiin.

Tietokantayhteyden testaus PHP:stä:

-Avataan MYSQL tietokanta komennolla ”sudo mysqlp -u root -p”

![image](https://github.com/user-attachments/assets/c655d01c-84c6-41e8-859e-94d46d8b3d89)

-Luodaan tietokanta nimeltä ’test_database’.

![image](https://github.com/user-attachments/assets/68c5dc73-08a8-4501-8b85-2b8f99dac9e9)

-Luodaan käyttäjä nimeltä ’mysql_user’.

![image](https://github.com/user-attachments/assets/7788b474-3644-48c7-853c-9227e3eab922)

-’@’ merkin jälkeen voi myös laittaa IP -osoitteen mistä käyttäjä voi kirjautua tietokantaan. Tässä tapauksessa käytetään % -merkkiä, joka tarkoittaa että kirjautumisen voi suorittaa kaikkialta. ’IDENTIFIED BY ’’’ antaa käyttäjälle salasanan. Kun käyttäjä on luotu, sille annetaan kaikki oikeudet tietokantaan ’test_database’.

![image](https://github.com/user-attachments/assets/c7b1ff82-b8f3-4c61-afe0-4220096c4064)

-Poistutaan ’root’ käyttäjältä ’exit’ -komennolla ja kirjaudutaan uudelleen ’mysql_user’ -käyttäjällä.
Kokeillaan saiko käyttäjä oikeudet.

![image](https://github.com/user-attachments/assets/2707aa2d-9589-42f7-8e75-418099a92e2c)

-Luodaan ’test_database’ tietokantaan uusi taulukko ’todo_list’

![image](https://github.com/user-attachments/assets/027f2006-3d5d-42d6-8976-78eda41233dd)

-item_id INT AUTO_INCREMENT tarkoittaa että item_id on lukuarvo ja se annetaan automaattisesti. content VARCHAR(255) tarkoittaa että content sisältää kirjaimia maksimissaan 255 kappaletta. PRIMARY KEY(item_id) tarkoittaa että item_id on taulukon pääavain. Jokaisella esineellä on uniikki id -tunnus.

![image](https://github.com/user-attachments/assets/4048f293-e14a-4d4a-b74d-c294da1d3fa1)

-todo_list -taulukko on tällä hetkellä tyhjä. Seuraavaksi lisätään sisältöä taulukkoon.

![image](https://github.com/user-attachments/assets/07a5aaa1-11fc-4a7d-a510-b88865ea8901)

-Aiemmin annoin komennon ”USE test_database;”, joten tämä tietokanta on jo valmiiksi käytössä, jolloin ei tarvitse ”INSERT INTO” jälkeen laittaa erikseen ’test_database’. Seuraavaksi suljetaan MYSQL -yhteys ja luodaan ’todo_list.php’ -tiedosto /var/www/vilho.harjajarvi.dy.fi -hakemistoon.

![image](https://github.com/user-attachments/assets/28c754e3-f858-430e-b5eb-3c67e61003f0)

Kirjoitetaan sisällöksi:

![image](https://github.com/user-attachments/assets/5ae1caa9-1287-43f4-98db-1e33aa6b2480)

-Tallennetaan tiedosto, ja avataan Demo-Ubuntu työpöytä jonka jälkeen kokeillaan nähdäänkö MYSQL - tietokanta sivustolla.

![image](https://github.com/user-attachments/assets/52f9ef51-ed5d-4b84-a125-dfad17410511)

#

<strong>TLS-sertifikaatti ja WordPressin asennus</strong>

-Ennen asennusta suojataan sivusto TLS -sertifikaatilla. Tällä salataan sivuston liikenne siten että käyttäjän ja sivuston tekijän välinen yhteys on turvallinen.

-Otetaan käyttöön mod_ssl, Apache-moduuli, joka tukee SSL-salausta.

![image](https://github.com/user-attachments/assets/8467e91b-08fc-40b3-88a8-ece4c99d7737)

-Ajetaan komento ”systemctl restart apache2”, jotta mod_ssl-moduuli tulee käytäntöön.

![image](https://github.com/user-attachments/assets/9ced51dc-ff53-4ba1-9784-ac720e47240e)

-Tämän jälkeen luodaan TLS-avain ja varmennetiedostos openssl-komenolla. Tämän jälkeen terminaaliin pitää täyttää tietoja.

![image](https://github.com/user-attachments/assets/69bd096f-9488-493c-a6e1-ba08c9660472)

-Tämän jälkeen siirrytään ’sites-available’ hakemistoon määritelmätiedostoon ’vilho.harjajarvi.dy.fi’, ja luodaan uusi virtualhost porttiin 443 (https), joka sisältää ssl-tiedostoja.

![image](https://github.com/user-attachments/assets/e467e97f-568e-4833-aedd-a3d09bd9ed75)

-Virtualhostin määrittämisen jälkeen, tarkastetaan syntaksi ja jos kaikki on OK, ladataan uudelleen Apache. (sudo systemctl reload apache2). Sallitaan seuraavaksi palomuurissa liikenne portteihin 80 (http) ja 443 (https). Poistetaan samalla sisältö, joka kohdistuu pelkästään porttiin 80 (http)

![image](https://github.com/user-attachments/assets/e76ccf44-179a-4fe6-a3a9-199540597729)

![image](https://github.com/user-attachments/assets/ae54c810-2c8c-4cba-bf73-5aaa07c1a3b9)

-Siirrytään Demo-Ubuntu työpöydälle, ja katsotaan tuliko sivustolle muutoksia.

![image](https://github.com/user-attachments/assets/533c45db-f2f7-4b6d-9289-475cb157bdab)

-URL edessä näkyy että sivu käyttää https-protokollaa. Voidaan myös tarkistaa sertifikaatti sivuston infosta.

![image](https://github.com/user-attachments/assets/80de3f7d-3a82-4738-9af7-7571d3c37831)

-Sivusto sallii edelleen http liikenteen. Korjataan tämä siten, että liikenne muutettaisiin https protokollan mukaiseksi tekemällä muutoksia 80 portin Virtualhost määritelmään.

![image](https://github.com/user-attachments/assets/0c1566e0-e03b-484e-bdfd-3e76bddc6301)

-Redirect rivi ohjaa liikenteen suoraan https://vilho.harjajarvi.dy.fi/ sivustolle (portin 443 kautta) vaikka ylempänä lukee, että liikenne kulkee portin 80 kautta. Käynnistetään jälleen uudelleen apache ja testataan.

![image](https://github.com/user-attachments/assets/8280f212-e373-4b08-9cdc-6594e23e93cb)

-Painetaan hakua, jonka jälkeen käyttäjä ohjataan 80 portin sijaan 443 portin kautta.

![image](https://github.com/user-attachments/assets/97e294af-18bb-4817-934e-0f51c94ad0ef)

-Nyt kun sivustolle on luotu sertifikaatti, voidaan asentaa WordPress. Aloitetaan luomalla mysql-tietokantaan uusi tietokanta ’wordpress’.

![image](https://github.com/user-attachments/assets/fb4a36ee-817b-4cc9-90f5-49d60e123ff6)

-Luodaan uusi käyttäjä, jota käytetään vain wordpress tietokannassa. (Korjaus ’wordpressuser’@’%’)

![image](https://github.com/user-attachments/assets/b9de4d72-3c73-4c26-84f0-c15a20a3f610)

-Annetaan vielä ’wordpressuser’-käyttäjälle kaikki oikeudet ’wordpress’-tietokantaan. (Korjaus ’wordpressuser’@’%’)

![image](https://github.com/user-attachments/assets/8783b997-f58e-4e62-8a7e-ea06df12ef09)

-Poistutaan MYSQL:stä, ja asennetaan pohja lisäosien asentamiselle WordPress-sivustolle.

![image](https://github.com/user-attachments/assets/fd10d951-ed6a-4ff5-9de1-c2673911a084)

-Käynnistetään Apache uudelleen. Tämän jälkeen sallitaan .htaccess-tiedostot asettamalla AllowOverride-komento ’vilho.harjajarvi.dy.fi.conf’ tiedostoon. Koska AllowOverriden arvo on ALL, se sallii kaikki direktiivit .htaccess-tiedostoissa.

![image](https://github.com/user-attachments/assets/867f320f-e4d9-4e08-bf14-5a02a00e3f14)

-Tarkistetaan, että syntaksi on oikein komennolla 'sudo apache2ctl configtest'.

![image](https://github.com/user-attachments/assets/3af0d084-7c47-4928-8f79-1d4a916d4e10)

-Tämän jälkeen annetaan komento ”sudo a2enmod rewrite” joka ottaa käyttöön ’mod_rewrite’ moduulin Apache http serverissä. Kyseinen moduuli mahdollistaa URL-osoitteiden uudelleenkirjoittamisen ja uudelleenohjaukset.

![image](https://github.com/user-attachments/assets/a443e9ca-9681-431f-bc68-d3e17386b1e4)

-Lopuksi käynnistetään uudelleen Apache.
Siirrytään tmp-hakemistoon ja ladataan verkosta WordPress.

![image](https://github.com/user-attachments/assets/feadbb9b-8152-45d2-877f-3d7f58e6c867)

-Puretaan pakattu tiedosto komennolla ”tar xzvf latest.tar.gz” luodaksemme WordPress-hakemistorakenne. Luodaan ’.htaccess’ tiedosto wordpress hakemistoon. Luodaan myös päivityshakemisto jotta käyttöoikeudet ovat kunnossa ohjelmistopäivityksien jälkeen.

![image](https://github.com/user-attachments/assets/ca5d4c59-8cbe-435b-8529-957230874fef)

-Kopioidaan vielä WordPress-hakemiston koko sisältö oman verkkosivun sisältöön. ’.’ wordpress-hakemiston perässä kopioi myös piilotetut tiedostot kuten .htaccess.

![image](https://github.com/user-attachments/assets/ed5b29d3-eabc-48cd-9c2b-c02ee7a06013)

-Päivitetään omistajuus, jonka avulla voi muokata tiedoston omistajuutta.

![image](https://github.com/user-attachments/assets/8c161518-be94-4c52-ae2d-67b5cf3ff8a3)

-Asetetaan jokaisen hakemiston (type -d) oikeudet arvoon 750. (rootille täydet oikeudet, ryhmät luku- ja suoritusoikeudet, muille käyttäjille ei mitään oikeuksia).

![image](https://github.com/user-attachments/assets/7007617c-1781-4c6e-a01c-c31a5c96080a)

-Asetetaan seuraavaksi kaikille tiedostoille hakemistosta (type -f) oikeudet arvoon 640.(rootille luku- ja kirjoitusoikeudet, ryhmät lukuoikeus ja muille käyttäjille ei mitään oikeuksia).

![image](https://github.com/user-attachments/assets/84f45bcb-d9ec-4bb6-a35d-0cf291ce1a09)

-Parannellaan vielä asennuksen suojausta lataamalla WordPress-paketti joka on generoinut uniikit avaimet valmiiksi jotta niitä ei tarvitse itse keksiä.

![image](https://github.com/user-attachments/assets/75bb09be-0f40-4768-aeb3-958b8b2c4eed)

-Asetetaan oikeat arvot tietokannan muuttujiin samassa määrittelytiedostossa. Tässä tapauksessa ne ovat ne arvot, jotka syötettiin ’wordpress’ tietokannan luomisessa.

![image](https://github.com/user-attachments/assets/ae01d4bf-175e-4735-bf83-042e3f17af1e)

-Tallennetaan tiedosto ja kokeillaan Demo-Ubuntu työpöydän selaimessa toimiiko sivusto oikein.

![image](https://github.com/user-attachments/assets/a3a4bdda-e680-445b-ba79-fff8415eb125)

-Täytellään tiedot, jonka jälkeen WordPress sivu on valmis käyttöä varten.

![image](https://github.com/user-attachments/assets/ace3115f-7521-4e8e-84aa-b80df4aa6392)
#
<strong> MySQL-tietokannan varmuuskopiointi </strong>

![image](https://github.com/user-attachments/assets/2d753bde-eaee-4506-a4cf-17fd896e0932)

Tarkastetaan mitä tietokantoja löytyy. Tämän jälkeen poistutaan MYSQL:stä ja luodaan ’backup’-niminen hakemisto johon myöhemmin tehdään varmuuskopio tietokannasta.

![image](https://github.com/user-attachments/assets/c93dde30-a68d-4184-b40a-a052d5f10b7b)

-Siirrytään backup-hakemistoon ja luodaan varmuuskopio.

![image](https://github.com/user-attachments/assets/3600aad9-1e84-4e90-9b06-42f350345870)

-Kokeillaan vielä toimiiko WordPress-sivusto DemoUbuntu-työpöydällä.

![image](https://github.com/user-attachments/assets/9faaa5b8-22a4-409a-987e-f25c7f4779ed)

-Tarkastetaan vielä, löytyykö tietokanta MYSQL:ssä. Tämän jälkeen voidaan poistaa tietokanta MYSQL:stä, koska varmuuskopio on luotu.

![image](https://github.com/user-attachments/assets/90644242-cce5-442e-94f9-31027d50a27f)

![image](https://github.com/user-attachments/assets/c251beee-e239-432b-bc55-5df2a7ad5099)

-Katsotaan, toimiiko WordPress-sivu nyt, kun tietokanta on poistettu.

![image](https://github.com/user-attachments/assets/c90b5fa0-ccbe-4831-80c1-4e2f49a3ce4c)

-Jos halutaan että sivu toimisi taas, pitäisi tehdä uusi tietokanta, tai palauttaa varmuuskopio alkuperäisestä tietokannasta.
#
<strong>MySQL-varmuuskopion palauttaminen</strong>

-Tietokannan varmuuskopio sijaitsee ’backup’ hakemistossa, joka luotiin edellisessä vaiheessa.

![image](https://github.com/user-attachments/assets/d7a341d4-2cbd-4306-9a9a-8b075c2a7278)

-Ensin täytyy kuitenkin luoda uusi tietokanta, jotta varmuuskopioiduille tiedoille saadaan jokin tietokanta.

![image](https://github.com/user-attachments/assets/9db4a1c3-9965-427e-9dfa-1622770113d1)

-Palauttaminen tapahtuu melkein identtisellä komennolla, kuin varmuuskopion luomisessa paitsi että dumppia ei enään käytetä ja ’>’ on nyt toisinpäin. Käytin tässä komennossa käyttäjää ’wordpressuser’, koska palauttaminen ei vaadi käyttäjiltä poikkeavia oikeuksia.

![image](https://github.com/user-attachments/assets/bb6e3443-34ee-4142-b51b-e96b588d8167)

-Nyt ’wordpress’ tietokanta on palautettu, ja voidaan kokeilla Demo-Ubuntu työpöydältä, jos WordPress-sivusto toimisi taas.

![image](https://github.com/user-attachments/assets/dfecc9da-6b17-4b40-b262-964f33cdc9e0)
