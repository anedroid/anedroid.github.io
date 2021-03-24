*Utworzony 24.03.2021*

# Konfiguracja pamięci wymiany (swap)

Pamięć wymiany, to rozszerzenie pamięci RAM o część fizycznej pamięci na dysku twardym. Obie pamięci są ze sobą połączone. Dzięki temu na komputerze można uruchomić bardziej zasobożerne programy lub sprawić, że stary komputer będzie działał lepiej. W dzisiejszym artykule opowiem, w jaki sposób rozszerzyć pamięć w systemie Linux (funkcjonalność kernela).

## Sprawdzenie stanu

W systemie GNU/Linux wiele zadań administracyjnych wykonuje się w terminalu, używając komend które najczęściej są zainstalowanymi w systemie programami. Również dodanie pamięci swap będzie odbywało się w całości w powłoce bash.

Komenda `free` wyświetli nam bieżący stan pamięci RAM i swap. Najwygodniej jest ją używać z parametrem `-h`, który wyświetli dostępną i zajętą pamięć w przyjaznych dla człowieka jednostkach: GiB i MiB.

```
$ free -h
			razem	użyte	wolne	dzielone	buf/cache	dostępne
Pamięć:		2,8Gi	1,1Gi	484Mi	304Mi		1,2Gi		1,2Gi
Wymiana:	4,4Gi	967Mi	3,5Gi	
```

Komenda `swapon` jest przeznaczona do uruchamiania pamięci swap, ale użyta z parametrem `--show` wyświetli bieżący stan każdej z pamięci swap (można ich mieć kilka):

```
$ swapon --show
NAME		TYPE		SIZE	USED	PRIO
/swapfile	file		1,5G	833,7M	-2
/dev/sda6	partition	3G		130,1M	-3
```

Jak widać, ja mam ustawiony swap w pliku `/swapfile`, oraz na partycji `/dev/sda6`. O partycjach w Linuxie mówiliśmy w [poprzednim artykule](system-plików-linuxa.md) o systemie plików.

## Konfiguracja swap-u w pliku

Zarówno partycja *linux-swap*, jak i plik swap są stałego rozmiaru. Plik swap trzeba utworzyć ręcznie komendą:

```bash
sudo dd if=/dev/zero of=/swapfile bs=1M count=1536
```

To może zająć chwilę. Komenda skopiuje 1536 MiB (1.5 GiB) z wirtualnego urządzenia `/dev/zero` do pliku `/swapfile`. Plik ten może mieć dowolną nazwę i ścieżkę, jednak ta lokalizacja i nazwa jest ogólnie przyjętą konwencją. O urządzeniach wirtualnych również pisałem w poprzednim artykule, a `/dev/zero`, to niekończący się "zbiornik" zer (bitów). W efekcie utworzony zostanie plik o rozmiarze 1.5 GiB wypełniony pustymi bajtami.

Plik swap musi należeć do użytkownika `root`. Jeżeli wywołaliśmy powyższą komendą z sudo, utworzony plik powinien "z automatu" zostać przyporządkowany do użytkownika i grupy `root`. Jeżeli tego nie zrobiliście, zmieńcie użytkownika i grupę komendą `chown`.

```bash
sudo chown root: /swapfile
```

Następnie ustawcie uprawnienia dla właściciela do odczytu i zapisu, a dla grupy i pozostałych użytkowników odmówcie wszystkich uprawnień (-rw-------).

```bash
sudo chmod 600 /swapfile
```

Plik swapfile jest gotowy. Teraz ustawimy go jako rozszerzenie pamięci.

```bash
sudo mkswap /swapfile
```

Jeżeli plik nie ma odpowiednich uprawnień, program wyświetli błąd o treści:

*mkswap: /swapfile: niebezpieczne uprawnienia 0644, powinno być 0600.*

Komenda mkswap nie zmieni niczego w systemie, a jedynie zapisze w pliku `/swapfile` odpowiednie dane - coś podobnego formatowania partycji.

Na koniec włączymy swap do pamięci Linuxa. Po wykonaniu tej komendy dostępne miejsce powinno się natychmiast zwiększyć.

```bash
sudo swapon /swapfile
```

Jeżeli nie wykonamy poprzedniej operacji "formatowania" pliku, program wyświetli błąd:

*swapon: /swapfile: odczyt nagłówka swapa nie powiódł się*

Komenda `swapon --show` będzie teraz wyświetlać nowy rekord.

**To nie koniec artykułu. Resztę napiszę później.**