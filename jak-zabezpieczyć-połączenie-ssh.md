*Utworzony 5.04.2021*

# Jak zabezpieczyć połączenie SSH?

Gdybym chciał włamać się do twojego komputera, na pewno zacząłbym od próby zalogowania się do powłoki bash przez ssh, a następnie na konto root, skąd mógłbym wyrządzić ogromne szkody. Otwarta usługa ssh to duża wygoda, ale też duże zagrożenie dla bezpieczeństwa. Nie musimy jednak z niej rezygnować, wystarczy zastosować się do tych kilku wskazówek które dzisiaj przedstawię.

Główna konfiguracja ssh znajduje się w pliku `/etc/ssh/sshd_config`. Po wprowadzeniu każdej zmiany przeładuj serwer ssh za pomocą:

```bash
sudo systemctl reload ssh
```

## Zmieńcie domyślny port

To zdecydowanie najszybszy i najłatwiejszy sposób zabezpieczenia serwera ssh, choć nadal będzie można przeskanować wszystkie porty poleceniem `nmap`. SSH działa domyślnie na porcie 22. Aby zmienić domyślny port, zmieńcie ustawienie `Port`. Wiele osób używa alternatywnych portów 2222 lub 8022. Może warto wymyśleć coś bardziej unikalnego?

Podczas logowania podajcie numer portu w parametrze `-p`:

```bash
ssh user@server -p 160
```

## Zablokujcie logowanie na konto root bezpośrednio z sieci

Niezależnie od tego, czy twój system pozwala na zalogowanie się do roota używając loginu i hasła, czy tylko przez sudo, ssh nigdy nie powinien pozwalać na zalogowanie się na roota bezpośrednio, a jedynie po ustanowieniu połączenia przy użyciu standardowego konta użytkownika używając su lub sudo.

Zmieńcie wartość `PermitRootLogin` na `no`.

## Ustawcie białą listę użytkowników którzy mogą się logować

Skoro uniemożliwiamy korzystanie z konta root w ssh, możemy pójść o krok dalej i wyraźnie określić KTO może łączyć się z serwerem. Być może z waszego komputera korzystają dwie osoby, ale tylko jedna z nich korzysta z ssh. W takim wypadku nie ma potrzeby pozwalać na zalogowanie z obu kont, szczególnie gdy ten drugi użytkownik należy do sudoers i być może ma słabe hasło.

Dodajcie wartość `AllowUsers` i wymieńcie po spacji użytkowników którzy mogą logować się przez ssh.

Możecie filtrować użytkowników i grupy przy użyciu białej i czarnej listy, używając następujących ustawień: `AllowUsers`, `DenyUsers`, `AllowGroups`, `DenyGroups`.

## I najważniejsze - uwierzytelnianie kluczem publicznym

Jak pisałem w [poprzednim artykule o konfiguracji serwera www](serwer-www-w-systemie-gnu-linux.md), w kryptografii asymetrycznej generowana jest para kluczy powiązanych ze sobą matematycznie. Jeden z nich jest prywatny i nigdy nie jest przesyłany przez sieć, a drugi publiczny i może być przesyłany przez sieć. Kryptografię asymetryczną można wykorzystywać nie tylko do szyfrowania end-to-end, ale także podpisywania cyfrowego. Jeżeli zaszyfrujemy wiadomość swoim kluczem prywatnym, każdy będzie mógł ją odszyfrować naszym kluczem prywatnym, ale nikt nie będzie mógł zaprzeczyć, że to właśnie my ją utworzyliśmy. Wiele protokołów sieciowych, w tym także ssh, stosuje zarówno szyfrowanie, jak i podpisywanie cyfrowe.

Aby wygenerować parę kluczy do uwierzytelniania ssh, skorzystamy z komendy `ssh-keygen`.

```
$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/home/user/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/user/.ssh/id_rsa
Your public key has been saved in /home/user/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:GLYO4jVkv6Lnpr0gwVns0nf6kGarrKnls7MelpTp8eg user@client
The key's randomart image is:
+---[RSA 3072]----+
|                 |
|  .              |
|   oo o          |
|. == o +         |
|.+*o+.+.S        |
| =.B.++.         |
|. X o*o          |
| *===.+          |
|o+E%=o .         |
+----[SHA256]-----+
```

Klucze domyślnie przechowywane są w katalogu ~/.ssh, więc każdy użytkownik ma własną parę kluczy. Domyślne nazwy kluczy to `id_rsa` - dla klucza prywatnego, i `id_rsa.pub` - dla klucza publicznego. Klucz prywatny możecie zabezpieczyć hasłem, wtedy przed każdym logowaniem będziecie pytani o hasło, ale do klucza, a nie użytkownika.

Następnie prześlijcie klucz publiczny do serwera.

```
$ ssh-copy-id user@server -p 160
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/user/.ssh/id_rsa.pub"
The authenticity of host '[server]:160 ([192.168.0.2]:160)' can't be established.
ECDSA key fingerprint is SHA256:TViPuTy2u6iO2t04TGoaFq1zTmEmfTglWmzaxy7c2fs.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
user@server's password: 

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh -p '160' 'user@server'"
and check to make sure that only the key(s) you wanted were added.

```

Po wprowadzeniu hasła klucz zostanie automatycznie zapisany w odpowiedniej lokalizacji na serwerze. Powtórzcie procedurę z generowaniem klucza i przesyłaniem na każdym urządzeniu z którego macie zamiar logować się do serwera. Warto to także zrobić na samym serwerze aby umożliwić łatwe sprawdzanie czy ssh w ogóle działa. Różne rzeczy mogą się zdarzyć.

Połączenie możecie przetestować komendą `ssh user@server`. Zwróćcie uwagę, że nie jesteście proszeni o podanie hasła do serwera. Teraz gdy macie zaakceptowane uwierzytelnianie kluczem publicznym, możecie wyłączyć w konfiguracji logowanie przy pomocy hasła aby zapobiec logowaniu się przy pomocy hasła. Dzięki temu włamanie się na serwer z zewnątrz będzie całkowicie niemożliwe, nawet gdy napastnik pozna wasze hasło, tak długo jak klucz prywatny pozostanie prywatny.

Ustawcie `PasswordAuthentication` na `no`. Pamiętajcie o przeładowaniu ustawień.

I to by było na tyle, jeżeli chodzi o zabezpieczanie usługi ssh. Mam nadzieję, że moje porady okazały się przydatne.