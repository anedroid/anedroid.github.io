*Utworzony 22.04.2021*

# Integracja telefonu z komputerem

Telefon z komputerem najczęściej łączymy aby: bezproblemowo przesyłać dane między tymi dwoma urządzeniami, sterować komputerem przy użyciu telefonu jak pilotem, albo wyświetlać powiadomienia na dużym ekranie bez odrywania się od pracy. Istnieje wiele różnych programów do realizacji tego celu, a w dzisiejszym artykule przedstawię dwa z nich: KDE Connect, oraz AirDroid. Każdy ma swoje zalety i wady, oraz różni się oferowanym zestawem funkcjonalności.

## KDE Connect

Program dostarczony domyślnie wraz z środowiskiem KDE. Posiada zestaw przydatnych funkcji do obustronnej komunikacji, choć w mojej opinii wiele z nich jest niedopracowanych i może nie działać poprawnie na niektórych telefonach. Warto jednak wspomnieć, że jest aplikacją niekomercyjną i wydaną na licencji GNU GPL-v2, co oznacza że będzie szanować naszą wolność i prywatność.

Aplikację na Androida (*org.kde.kdeconnect_tp*) można pobrać [stąd](https://f-droid.org/packages/org.kde.kdeconnect_tp). Jest dostępna także w [Google Play](https://play.google.com/store/apps/details?id=org.kde.kdeconnect_tp), jednak rekomenduję pobieranie aplikacji z F-Droida jeżeli są dostępne[^1]. Do działania wymagane jest połączenie Wi-Fi. Gdy dwa urządzenia - komputer i telefon - znajdują się w tej samej sieci, mogą przesyłać między sobą dane. Po zainstalowaniu telefon musi się sparować z komputerem (jak Bluetooth). Jeżeli komputer jest dostępny, powinien wyświetlać się na stronie głównej, ale jeżeli tak się nie dzieje, spróbujcie dodać ręcznie jego adres IP.

![parowanie KDE Connect](images/integracja-telefonu-z-komputerem_2.png)

Podczas parowania system zapyta o pozwolenie. Potem udzielamy wszelkich koniecznych uprawnień do działania aplikacji. Oto najbardziej przydatne (według mnie) funkcje KDE Connect:

### Wspólny schowek

Wyobraźmy sobie, że oglądamy film na YouTubie na komputerze i w pewnym momencie postanawiamy wysłać komuś do niego link. Może to być nieco problematyczne. Możemy próbować znaleźć ten film w aplikacji YouTube, wejść w historię (jeżeli korzystamy z konta Google), lub zeskanować kod QR i skopiować w telefonie jego zawartość. Używając KDE Connect wystarczy, że tylko skopiujemy link na komputerze, a następnie wkleimy go w telefonie. Działa to również w drugą stronę, z tym że zawartość schowka nie wyśle się automatycznie bo Android na to nie pozwala: trzeba kliknąć przycisk "Send clipboard" w powiadomieniu persistent.

### Automatyczne zatrzymanie filmu gdy ktoś dzwoni

Może nie jest to zamierzone zachowanie, ale jednak bardzo wygodne. Gdy ktoś dzwoni, system Android automatycznie zatrzymuje wszystkie odtwarzane w telefonie multimedia, jeżeli wyświetlają na pasku powiadomień sterowanie, oraz wznawia je po zakończeniu rozmowy. KDE Connect wyświetla takie powiadomienie gdy odtwarzany jest na komputerze film lub muzyka aby sterować odtwarzaniem jak pilotem. Każde zatrzymanie i wznowienie w powiadomieniu odpowiada zatrzymaniu i wznowieniu w komputerze. Android automatycznie zatrzymując odtwarzanie, "myśli" że zatrzymuje lokalne odtwarzanie, które tak naprawdę odbywa się na zdalnym urządzeniu.

### Wyświetlanie powiadomień na dużym ekranie

Czy wy też znacie tą sytuację, gdy wykonujecie na komputerze jakąś ważną pracę, a tu nagle: ping! - powiadomienie w telefonie. I chcąc-nie chcąc bierzecie telefon do ręki i sprawdzacie. Wasza uwaga właśnie uległa rozproszeniu. Na szczęście istnieje wiele aplikacji, które wyświetlą powiadomienie na ekranie komputera, dzięki czemu będziecie mogli szybko sprawdzić czy to coś ważnego, nie odrywając wzroku od ekranu. KDE Connect również posiada tę funkcję. Powiadomienia z telefonu mają swoje oddzielne miejsce w interfejsie KDE, nie mieszają się z powiadomieniami GNU/Linuxa.

![powiadomienia telefonu](images/integracja-telefonu-z-komputerem_3.png)

Niestety funkcja ta jest nieco niedopracowana, ale w aktualizacjach zaobserwowałem drobne zmiany, na przykład czyszczenie powiadomień zaczęło powodować nie tylko usuwanie ich z interfejsu KDE, ale także z telefonu. Czasami gdy urządzenie się na jakiś czas rozłączy, a potem połączy ponownie, na ekranie pojawia się mnóstwo nowych powiadomień, nawet tych które zostały już usunięte.

### Zdalna klawiatura

Niekiedy pisanie na klawiaturze telefonu potrafi doprowadzić do szału. Albo autokorekta wariuje wpisując słowa których zazwyczaj nie używacie albo musicie stukać po jednej literce. Jeżeli korzystacie z KDE Connect, możecie albo napisać sobie tekst na komputerze, a potem go [skopiować](#wspólny-schowek), albo użyć klawiatury swojego komputera do pisania bezpośrednio w aplikacji. Aby to zrobić, przełączcie wirtualną klawiaturę na KDE Connect, a następnie otwórzcie panel pokazany powyżej. Zacznijcie pisać w polu które się pojawi, a każde naciśnięcie klawisza zostanie wysłane do telefonu i odtworzone. Mega fajny pomysł, ale również mógłby zostać trochę ulepszony, tak jak powiadomienia.

<img src="images/integracja-telefonu-z-komputerem_4.png" alt="zdalna klawiatura" style="zoom: 67%;" />

Po pierwsze, wpisywane znaki nie powinny być widoczne w polu, bo możemy wpisywać np. hasła. Zamiast tego mogłaby się tylko wyświetlać informacja, że zdalna klawiatura jest aktywna (jakiś krótki napis lub ikona), a samo uruchomienie zdalnej klawiatury mogło by zostać uproszczone aby wymagało mniejszej liczby kliknięć. Provider klawiatury mógłby zostać zastąpiony przez usługę ułatwień dostępu, co zredukowałoby konieczność przełączania domyślnej klawiatury na KDE Connect, albo klawiatura KDE Connect mogłaby również wyświetlać klawisze na ekranie gdy zdalna klawiatura nie jest aktywna, oraz aktywować się natychmiast gdy tylko otwarty zostanie panel.

### Wykonywanie komend

W ustawieniach KDE Connect na komputerze możemy dodać komendy które będzie można wywołać naciśnięciem przycisku, np. wyłączenie komputera, wykonanie jakiegoś skryptu bash, odblokowanie ekranu bez hasła, etc. Komendy zostaną wywołane jako login shell, podobnie jak komendy wpisywane w Krunner (przydaje się gdy interfejs padł żeby go uruchomić ponownie: `killall plasmashell ; plasmashell`).

## AirDroid

Od razu na starcie ostrzegam: **AirDroid jest aplikacją komercyjną, promuje niewolne usługi sieciowe, zawiera płatne funkcje, reklamy i trackery[^2] Google. Instalujecie na własną odpowiedzialność**. Aplikację *com.sand.android* możecie pobrać [stąd](https://play.google.com/store/apps/details?id=com.sand.airdroid). Przejdźmy do opisu aplikacji.

![interfejs AirDroid - wygląda jak iOS](images/integracja-telefonu-z-komputerem_5.png)

AirDroid jest przeznaczony do sterowania telefonem za pomocą komputera. Udostępnia nam ładny pulpit przypominający interfejs Apple (co potwierdzają screenshoty w Google Play), do którego to możemy uzyskać dostęp odwiedzając odpowiednią stronę w przeglądarce. AirDroid standardowo działa na porcie 8888, ponieważ system Android nie pozwala na otwarcie portu 80. Aby zobaczyć adres tej strony, należy wejść w *Urządzenia/AirDroid Web*.

Podczas każdego logowania telefon wyświetli okno podobne do pytania czy udzielić uprawnienia aplikacji. Strona nie używa cookies, więc niestety będzie pytać każdorazowo. Pytania można to wyłączyć w ustawieniach (mało bezpieczne).

![Mogę się połączyć?](images/integracja-telefonu-z-komputerem_6.png)

AirDroid udostępnia nam szereg funkcji do integracji telefonu i komputera na różnych płaszczyznach, które będę odtąd nazywać aplikacjami, ponieważ wyświetlają się w oknach jak aplikacje.

### Zarządzanie plikami

AirDroid udostępnia zestaw aplikacji do zarządzania plikami. Pliki można zarówno pobierać, jak i oglądać, co jest świetne jeżeli chcemy komuś pokazać zdjęcia które zrobiliśmy telefonem na dużym ekranie. Jeżeli włączamy w ten sposób muzykę, możemy ją puścić w tle. Niestety AirDroid nie obsługuje niektórych formatów multimedialnych, np. webm.

Fajną funkcją jest możliwość wgrania całego katalogu do telefonu, co można zrobić zarówno wybierając plik w oknie dialogowym, jak i przeciągając ikonę do okna przeglądarki. Niestety nie można tego robić w odwrotny sposób, a nie wydaje się to trudne do zaimplementowania. Wystarczyłoby pod tymi ikonami wstawić link do pliku który zostanie pobrany, ale zdarzenie kliknięcia zostałoby zablokowane `e.preventDefault()` .

Nie zabrakło oczywiście także podstawowych operacji na plikach, ale chyba nie muszę ich wymieniać. Archiwów nie obsługuje.

### Zarządzanie aplikacjami

AirDroid pozwala także na bardzo łatwą instalację aplikacji na telefonie. Wystarczy przeciągnąć ikonę pliku apk w odpowiednie miejsce. Plik automatycznie zostanie przesłany, a AirDroid uruchomi instalatora. Potem wystarczy już tylko potwierdzić zamiar instalacji. Dostępny jest także menedżer który pozwala na łatwe odinstalowanie aplikacji oraz zapisanie apk.

### Podglądanie kamery i ekranu

Przy pomocy aplikacji "Aparat" możemy zdalnie podejrzeć na żywo obraz z kamery telefonu, oczywiście po udzieleniu dostępu do kamery. O ile urządzenie nie jest wyposażone w sprzętowy lub programowy sygnalizator użycia kamery, nic nie zdradzi tego że kamera jest właśnie używana.

Obraz z kamery możemy wyświetlić na pełnym ekranie. Możemy także podsłuchiwać otoczenie, ale ta funkcja jest dostępna tylko w Chrome, mimo że w innych przeglądarkach, w tym używanym przeze mnie Firefoxie równie łatwo da się zaimplementować tą funkcjonalność.

Podobnie jak obraz kamery, możemy także wyświetlać na komputerze obraz z ekranu telefonu. Choć czasami liczba klatek na sekundę pozostawia wiele do życzenia. Do strumieniowania obrazu ekranu AirDroid używa API systemu Android, które może czasem odmówić nagrania niektórych rzeczy. Wtedy przesłany zostanie tylko czarny ekran. Ograniczenie to jest narzucane przez aplikacje których nagrywanie dotyczy.

Do czego takie ograniczenie nagrywania może być wykorzystane? Na przykład do ochrony prywatnych danych. Niektóre aplikacje dają użytkownikowi wybór czy zabezpieczać przed nagraniem czy nie, np. Nextcloud (*com.nextcloud.client*) lub TOR Browser (*org.torproject.torbrowser*). Ochrona przed nagrywaniem może zostać także wykorzystana w złym celu - do zabezpieczenia treści objętych prawami autorskimi przed nieautoryzowanym kopiowaniem. Prawa autorskie to temat na odrębny artykuł. Na WIELE odrębnych artykułów.

### Inne funkcje

Poza tymi najważniejszymi funkcjami w AirDroid możemy jeszcze:

- Odbierać i wysyłać SMS-y
- Inicjować połączenia telefoniczne
- Ustawiać dzwonki, oraz dźwięki powiadomień i alarmu
- Zarządzać kontaktami
- Wyświetlać powiadomienia w oknie przeglądarki

Poza tym AirDroid pozwala na jeszcze więcej, jeżeli zarejestrujemy się na [web.airdroid.com](https://web.airdroid.com/)

### Kwestie bezpieczeństwa

Ja zdecydowanie odradzam korzystanie z AirDroid z kilku powodów. Część z nich napisałem już wcześniej. Najważniejszy z nich, to że jest to aplikacja komercyjna, a takich powinno się unikać, ponieważ oprogramowanie własnościowe (proprietary software) nie zapewnia nam wolności, a często jest także szkodliwe. W przypadku AirDroida jest to szczególnie ważne zważywszy na to jak wiele uprawnień mu nadajemy:

- **ACCESS_BACKGROUND_LOCATION**
- **ACCESS_COARSE_LOCATION**
- **ACCESS_FINE_LOCATION**
- ACCESS_NETWORK_STATE
- ACCESS_WIFI_STATE
- **ANSWER_PHONE_CALLS**
- BATTERY_STATS
- BLUETOOTH
- BLUETOOTH_ADMIN
- **CALL_PHONE**
- **CAMERA**
- CHANGE_NETWORK_STATE
- CHANGE_WIFI_MULTICAST_STATE
- CHANGE_WIFI_STATE
- DISABLE_KEYGUARD
- FLASHLIGHT
- FOREGROUND_SERVICE
- **GET_ACCOUNTS**
- GET_TASKS
- INTERNET
- KILL_BACKGROUND_PROCESSES
- MODIFY_AUDIO_SETTINGS
- MODIFY_PHONE_STATE
- PACKAGE_USAGE_STATS
- **READ_CALL_LOG**
- **READ_CONTACTS**
- **READ_EXTERNAL_STORAGE**
- **READ_PHONE_STATE**
- **READ_SMS**
- RECEIVE_BOOT_COMPLETED
- **RECEIVE_SMS**
- **RECORD_AUDIO**
- REQUEST_DELETE_PACKAGES
- REQUEST_IGNORE_BATTERY_OPTIMIZATIONS
- REQUEST_INSTALL_PACKAGES
- RESTART_PACKAGES
- **SEND_SMS**
- SET_WALLPAPER
- SYSTEM_ALERT_WINDOW
- VIBRATE
- WAKE_LOCK
- **WRITE_CONTACTS**
- **WRITE_EXTERNAL_STORAGE**
- WRITE_SETTINGS
- com.android.launcher.permission.INSTALL_SHORTCUT
- com.google.android.c2dm.permission.RECEIVE
- com.google.android.providers.gsf.permission.READ_GSERVICES

Jak widzimy, AirDroid ma dostęp do naprawdę wielu rzeczy w telefonie. Aplikacja żądająca takiej ilości uprawnień powinna być godna zaufania, aby użytkownik nie był narażony na wyciek jego prywatnych danych lub przejęcie kontroli nad jego telefonem. W *com.sand.airdroid* znalazłem aż 6 trackerów[^2] , a strona www generowana dynamicznie ma załączony skrypt Google Analytics (http://www.google-analytics.com/analytics.js). Podczas połączenia przez Wi-Fi strona komunikuje się z domenami airdroid.com, a powinna tylko z telefonem.

Można oczywiście próbować modyfikować aplikację, chociażby usuwając z manifestu te klasy które nam się nie podobają, oraz filtrując jej ruch sieciowy, ale to nie rozwiązuje problemu. Znacznie lepszym i łatwiejszym rozwiązaniem jest znalezienie dobrej alternatywy. Jeżeli zależy wam na wolności, prywatności i bezpieczeństwie, szukajcie nowych aplikacji w zaufanych źródłach jak [F-Droid](https://f-droid.org).



I to by było na tyle, jeśli chodzi o te dwie aplikacje. Jak widzicie, napisałem tutaj trochę o prywatności. W kolejnym artykule napiszę dlaczego prywatność jest ważna, a także jak wysyłać zaszyfrowane wiadomości email. Życzę wam miłego dnia.

---

[^1]: Niektórzy developerzy wydają aplikacje na podwójnej licencji: komercyjnej i wolnej, a wersja dostępna w Google Play została skompilowana z innego źródła. Przykładem takiej aplikacji jest [org.tasks](https://github.com/tasks/tasks). Kod źródłowy dostępny na Githubie jest tym "właściwym" z którego F-Droid skompilował apk, ale ta sama aplikacja w tej samej wersji w Google Play (do której link developerzy zamieścili w README) zawiera złośliwy kod z trackerami Google Analytics i płatnościami za rzeczy które w rzeczywistości są (i powinny być) darmowe. Wersja F-Droid ma tylko opcję wsparcia twórcy za które nie otrzymujemy nic w zamian. <br /><br />Nawet gdybym wspierał programistów finansowo, to nigdy nie chciałbym aby taki oszust zarobił na swojej aplikacji choćby 10 z. Ale jeżeli wy chcecie go wesprzeć, tu jest jego strona wsparcia: [https://tasks.org/docs/donate](https://tasks.org/docs/donate). Dodam, że zarówno aplikacja w Google Play, jak i F-Droid są regularnie aktualizowane, a poniższe screenshoty dotyczą wersji 11.9.2.<br /><br />[<img src="images/integracja-telefonu-z-komputerem_1.png" alt="org.tasks Google Play vs org tasks F-Droid" />](images/integracja-telefonu-z-komputerem_1.png)<br /><br />Stąd wniosek, że Google Play nie jest dobrym źródłem aplikacji, nie wspominając już o tym że nie pozwala pobierać aplikacji bez konta, a przynajmniej nie normalnymi sposobami, oraz o paskudnej cenzurze przez którą wiele dobrych aplikacji zostało wykluczonych, bo nie są zgodne z polityką Google.

[^2]: Znalezione trackery to: Google Crashlytics, Google Anaytics, Google Firebase Analytics, Google Tag Manager, Google AdMob i µ?ACRA.

