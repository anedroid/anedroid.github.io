# Wprowadzenie

Witajcie na moim blogu poświęconym tematyce GNU/Linuxa i programowania, a to jest pierwszy artykuł w którym opowiem o tym, czym jest GNU/Linux, dlaczego warto się nim zainteresować, oraz jak go zainstalować na swoim komputerze.

Nie mam jeszcze dokładnych planów co do bloga, chciałbym aby był on sposobem w jaki będę się dzielił z wami wiedzą którą zdobywam. Mam nadzieję, że dzięki niemu moje zarwane noce poświęcone na szukaniu rozwiązań problemów i odpowiedzi na pytania przydadzą się nie tylko mnie. Kiedyś prowadziłem kanał na YouTubie, ale wkrótce z niego zrezygnowałem, bo nie miałem czasu ani chęci na nagrywanie, a montowanie sprawiało mi ogromne trudności.

# Wybór dystrybucji

Jeżeli nie jesteś jeszcze użytkownikiem GNU/Linux, prawdopodobnie oczywistym jest dla ciebie, że system operacyjny jest "pojedynczy" - tworzony i rozwijany przez jedną firmę, a jego rozwój polega na wydawaniu aktualizacji, jedna po drugiej. System GNU/Linux jest wyjątkowy, ponieważ rozwija się w wielu wersjach równolegle, przez niezależne osoby lub organizacje. Jest to możliwe dzięki temu, że jego [kod źródłowy](https://github.com/torvalds/linux) jest dostępny publicznie. Każdy kto potrafi programować, może go modyfikować i wprowadzać własne ulepszenia, oraz je rozpowszechniać bez ograniczeń. W ten sposób powstają tzw. dystrybucje GNU/Linuxa.

Czym jest dystrybucja? Jest to gotowy do użytku system operacyjny. Składa się z jądra, powłoki graficznej bądź tekstowej, oraz zestawu aplikacji użytkowych. Często zawiera także repozytoria z wolnym (jak wolność) i darmowym oprogramowaniem, ale nic nie stoi na przeszkodzie aby instalować pakiety spoza tych repozytoriów.

Niektóre dystrybucje GNU/Linuxa są ogólnego przeznaczenia, inne przeznaczone do specjalistycznych zadań. Najczęściej system GNU/Linux jest wykorzystywany w serwerach internetowych ze względu na jego niezawodność i wydajność, ale wiele dystrybucji doskonale się sprawdza jako narzędzie do codziennej pracy. Niektóre dystrybucje są łatwe w użyciu, "prowadzą za rączkę" użytkownika, inne trzeba samodzielnie skonfigurować, a w skrajnych wypadkach nawet skompilować własne jądro! Ale za to jaki jest potem szybki...

Na początek warto jest znaleźć taką dystrybucję, która ułatwi użytkownikowi zaadoptowanie się w nowym środowisku, bez przytłaczania od razu tymi wszystkimi skomplikowanymi zagadnieniami. Swoją przygodę z GNU/Linuxem zacząłem od [Linuxfx](https://www.linuxfx.org) (zmienił potem nazwę na Windowsfx). Jego interfejs jest skonstruowany w taki sposób, że niemal do złudzenia przypomina Windowsa 10. Jednak po paru dniach zacząłem testować inne dystrybucje: [Deepin](https://www.deepin.org/en/), [Zorin OS](https://zorinos.com/), [Linux Mint](https://linuxmint.com/). Ten artykuł piszę na [Kubuntu](https://kubuntu.org/). Używam go już ponad pół roku. Miałem też do czynienia z [Ubuntu](https://ubuntu.com/). Inne popularne dystrybucje to: [Debian](https://www.debian.org/), [Fedora](https://getfedora.org/), [Arch](https://archlinux.org/), [SUSE](https://www.suse.com/). Mirosław Zelent w [jednym z filmów](https://youtu.be/n_FffFwqBLA) zaprezentował [Elementary OS](https://elementary.io/) jako dobry dla początkujących.

# Nagrywanie obrazu dysku

System operacyjny możecie zainstalować na maszynie wirtualnej lub fizycznie na dysku twardym. Osobiście rekomenduję zapomnieć o maszynie wirtualnej. Dlaczego? Po pierwsze, to spowalnia system, bo trochę mocy obliczeniowej schodzi na wirtualizację i system nadrzędny. Po drugie, GNU/Linux będzie wtedy pod kontrolą Windowsa, który nagle z niewiadomych przyczyn może odmówić posłuszeństwa. Ale możecie też zainstalować kilka systemów równolegle, nawet na jednym dysku. I wbrew pozorom wcale nie jest to takie trudne zadanie. Jedyne czego będziecie potrzebować, to trochę wolnego miejsca, pendriva który można sformatować, nie zaszkodzi również szybkie łącze internetowe do pobrania obrazu dysku ważącego 3-4 GiB.

Wejdźcie na stronę systemu i pobierzcie stamtąd plik *.iso. Następnie przygotujcie program do nagrywania obrazów iso, na przykład popularny wśród użytkowników Windowsa [Rufus](https://rufus.ie/) (nie wymaga instalacji). Podłączcie pendrive i upewnijcie się, że nie skasujecie na nim ważnych danych. Po uruchomieniu Rufusa powinno się wyświetlić takie okno:

![okno Rufusa](https://rufus.ie/pics/rufus_pl.png)

Wybierzcie urządzenie i obraz dysku. Najczęściej pozostałe opcje możecie pozostawić bez zmian. Po wciśnięciu "start" powinna rozpocząć się procedura formatowania i nagrywania obrazu. Po jej zakończeniu zrestartujcie komputer pozostawiając pendrive w porcie USB.

# Instalacja GNU/Linuxa

Instalator powinien wystartować automatycznie. Jeżeli jednak tak się nie stało, jeszcze raz zrestartujcie komputer, i w chwili gdy będzie się wyświetlać motherboard naciskajcie klawisz uruchamiający boot menu. Najczęściej będzie to F12, ale może się różnić w zależności od modelu komputera. Wystarczy sprawdzić w internecie, na przykład tu: https://pl.wikipedia.org/wiki/Program_rozruchowy.

![boot menu](https://cdn1.expertreviews.co.uk/sites/expertreviews/files/2015/08/boot_menu.png?itok=puiPdZ7b)

Gdy uruchomi się instalator GNU/Linuxa, poprowadzi nas przez proces instalacji krok-po-kroku. Często na tym etapie można już przetestować system w trybie Live CD. Podczas instalacji należy zwrócić szczególną uwagę na sekcję partycjonowania. Partycjonowanie to dzielenie dysku twardego na części o stałym rozmiarze, na których znajdują się system operacyjny i pliki. Partycje mają niezależne systemy plików, a ponad nimi jest system partycjonowania. W popularnym obecnie systemie MBR można utworzyć maksymalnie 4 partycje, ale można ten mechanizm trochę oszukać, stosując tzw. partycje rozszerzone, które z punktu widzenia systemu partycjonowania należą do tej samej partycji, ale system operacyjny widzi je jako oddzielne.

Utworzone partycje można rozszerzać lub zwężać, ale tylko z prawej strony, usuwać, oraz przesuwać, ale jest to proces czasochłonny. Wizualizacja partycji przedstawiona w programie odpowiada rzeczywistym ułożeniu partycji na dysku. Nie mogą one przenikać między sobą, ulegać fragmentacji, ani dynamicznie zmieniać rozmiaru, w przeciwieństwie do danych w systemach plików.

Instalując GNU/Linuxa obok Windowsa zmniejszcie partycję z Windowsem pozostawiając przynajmniej 20 GiB wolnego miejsca, a w to miejsce utwórzcie nową partycję ext4 i zamontujcie w niej root systemu (`/`). Jeżeli zamierzacie korzystać na Linuxie z plików na partycji z Windowsem, możecie zamontować w systemie również tę partycję, ale można to zrobić w dowolnym momencie, nie tylko podczas instalacji.

W dalszych ustawieniach możecie utworzyć swoje konto, często z opcją szyfrowania katalogu `home`. Jeżeli ją włączycie, nikt nie będzie mógł uzyskać dostępu do waszych plików bez hasła. Jeżeli stracicie hasło, stracicie również dane. Obecnie nie znam żadnego sposobu na skonfigurowanie tego później, ale jeżeli będzie taka potrzeba, dowiem się i napiszę o tym artykuł.

# Boot manager

Po zainstalowaniu dystrybucji GNU/Linuxa możecie zrestartować swój komputer i odłączyć pendriva. Przed uruchomieniem systemu na ekranie powinna się wyświetlić lista systemów operacyjnych które możemy uruchomić.

![GRUB](https://upload.wikimedia.org/wikipedia/commons/1/12/GRUB_screenshot.png)

GNU/Linux będzie na pierwszym miejscu, dalej recovery mode i Windows. Wyświetla się tam również opcja *Memtest*, ale nigdy mi się nie przydała. Program który się właśnie uruchomił, to tzw. *GRUB*. Nie należy on do BIOS-u, tak jak *boot menu*, ale został zainstalowany razem z nowym systemem, dlatego należy uważać aby go nie uszkodzić. Może się to zdarzyć podczas usuwania partycji lub plików w katalogu `/boot` (nie polecam). Można go wprawdzie naprawić używając programu *boot repair*, ale trzeba wiedzieć jak.

GRUB zawiera także inne opcje: edycję komend przed uruchomieniem (klawisz E) i prowizoryczny wiersz polecenia (klawisz C), pomocny przy uruchamianiu systemu w niestandardowy sposób.

# Co dalej?

Cóż... Zalogujcie się do systemu, zapoznajcie się z interfejsem, zainstalujcie aktualizacje, sterowniki. Zaprzyjaźnijcie się z terminalem, który początkowo może wydawać się groźny, ale po poznaniu parunastu programów okazuje się fantastycznym narzędziem. Nauczcie się korzystać z menedżera pakietów.

GNU/Linux jest trudny w nauce w porównaniu do innych, komercyjnych systemów operacyjnych, ale dzięki jego elastyczności i otwartości da się na nim zrobić praktycznie wszystko. W razie problemów zawsze możecie pytać społeczność na forach, jak [stackoverflow](https://stackoverflow.com), czy chociażby [pasja-informatyki.pl](https://forum.pasja-informatyki.pl).

Możecie się zastanawiać, dlaczego piszę GNU/Linux, a nie Linux. Otóż "Linux" staram się pisać tylko na określenie samego kernela stworzonego przez Linusa Torvaldsa. Jednak ważną rolę w społeczności Linuxa odgrywa również projekt GNU na którym opiera się cała filozofia Linuxowej społeczności, a używanie nazwy GNU/Linux, ma na celu zwrócenie na niego uwagi. Co ciekawe skrót ten możecie znać też z innych miejsc: *GIMP* (GNU-Image-Manipulation-Program), GNU GPL, *gcc* (GNU-C-Compiler), etc. Polecam zainteresować się GNU. Kiedyś napiszę o nim artykuł.

Nie wiem dokładnie kiedy na moim blogu pojawi się kolejny artykuł, ale wkrótce zrobię do niego kanał RSS dzięki któremu będziecie mogli łatwiej śledzić zmiany. Pozdrawiam i życzę wam przyjemnej nauki i użytkowania nowego systemu, oraz nowych ekscytujących doświadczeń z nim związanych.
