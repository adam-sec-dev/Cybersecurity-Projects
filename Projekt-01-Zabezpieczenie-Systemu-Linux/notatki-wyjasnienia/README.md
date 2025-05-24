# Wyjaśnienia – Projekt 01: Zabezpieczenie systemu Linux

CZĘŚĆ 1: KOMENDY I ICH PEŁNE WYJAŚNIENIE

1. sudo apt update

Co robi: Odświeża lokalną listę dostępnych pakietów z repozytoriów. Dlaczego: Zanim coś zainstalujemy lub zaktualizujemy, system musi znać najnowsze wersje pakietów. Kiedy używać: Przed każdą instalacją nowego oprogramowania lub aktualizacją systemu. Na pamięć: TAK – bardzo podstawowa komenda.

2. sudo apt upgrade

Co robi: Aktualizuje zainstalowane pakiety do najnowszych dostępnych wersji (zgodnie z listą pobraną przez apt update). Dlaczego: Aby system był bezpieczny i aktualny. Na pamięć: TAK – jedna z najczęściej używanych komend administracyjnych.

3. cat /etc/passwd

Co robi: Wyświetla listę wszystkich kont użytkowników na systemie. Dlaczego: Można sprawdzić kto ma konto na systemie i jakie ma ustawione powłoki. Na pamięć: NIE – ale warto wiedzieć, co zawiera ten plik. Co zapamiętać: Konto użytkownika adam miało /bin/bash (czyli może się normalnie logować), a wiele systemowych kont ma /usr/sbin/nologin lub /bin/false.

4. cat /etc/group

Co robi: Wyświetla wszystkie grupy systemowe i użytkowników przypisanych do nich. Dlaczego: Grupy decydują o dostępie do zasobów. Na pamięć: NIE – ale trzeba wiedzieć jak sprawdzić grupy. Co zapamiętać: adam należy m.in. do sudo, lpadmin, plugdev, dip, cdrom, adm, users.

5. who

Co robi: Pokazuje kto jest aktualnie zalogowany do systemu. Dlaczego: Dla administratora to sposób na sprawdzenie aktywności użytkowników. Na pamięć: NIE – ale bardzo prosta komenda, łatwa do zapamiętania.

6. systemctl list-units --type=service --state=running

Co robi: Wyświetla listę wszystkich aktywnych usług systemowych. Dlaczego: Możemy sprawdzić, co działa w tle (np. ssh, cups, gdm, snapd, cron). Na pamięć: NIE – ale znać strukturę komendy. Zapamiętać: systemctl = zarządzanie usługami w systemach z systemd.

7. ss -tuln

Co robi: Pokazuje nasłuchujące porty TCP i UDP wraz z adresami IP. Dlaczego: Służy do sprawdzania bezpieczeństwa i otwartych usług sieciowych. Na pamięć: NIE – ale ważna do audytów i diagnostyki. Co zapamiętać: t – TCP, u – UDP, l – nasłuchiwanie, n – bez tłumaczenia nazw.

8. sudo systemctl status ssh

Co robi: Pokazuje stan usługi SSH (jeśli zainstalowana). Dlaczego: SSH to kluczowy protokół do zdalnego zarządzania. Na pamięć: TAK – przy pracy z serwerami. Warto wiedzieć: Jeśli usługa nie istnieje, system wyświetli odpowiedni komunikat.




CZĘŚĆ 2: UŻYTKOWNICY I GRUPY

1. Użytkownik adam

Konto lokalne z pełnym dostępem (należy do grupy sudo).

Może wykonywać komendy z uprawnieniami administratora.


2. Grupa scanner

Umożliwia dostęp do skanerów (np. przez aplikacje typu Simple Scan).

Domyślnie pusta lub z użytkownikiem saned.


3. Grupa gdm

Odpowiada za graficzny menedżer logowania GNOME (Gnome Display Manager).

Zarządza ekranem logowania i sesjami graficznymi.


4. Grupa lpadmin

Pozwala na zarządzanie drukarkami przez CUPS.


5. Grupa plugdev

Dostęp do urządzeń typu pendrive.


6. Grupa sudo


Zarządzanie użytkownikami i grupami w systemie Linux


cat /etc/passwd

Plik zawiera listę wszystkich użytkowników w systemie.
Każdy wiersz odpowiada jednemu użytkownikowi i zawiera:
– nazwę użytkownika
– UID (User ID) i GID (Group ID)
– katalog domowy
– powłokę logowania (shell)

Przykład wpisu:
adam:x:1000:1000:Adam,,,:/home/adam:/bin/bash

Użytkownicy, którzy posiadają /bin/bash jako powłokę, mogą logować się do systemu.
Użytkownik root ma UID 0 i pełne uprawnienia administracyjne.
cat /etc/group

Wyświetla listę wszystkich grup użytkowników w systemie.

Grupy pozwalają zarządzać dostępem do zasobów (np. plików, urządzeń, drukarek).
Każdy użytkownik należy do co najmniej jednej grupy, a może należeć do wielu.

Przykład wpisu:
sudo:x:27:adam

Oznacza, że użytkownik adam należy do grupy sudo i może używać polecenia sudo (czyli ma uprawnienia administratora).
who

Wyświetla aktualnie zalogowanych użytkowników i źródła ich sesji.

Przykład:
adam tty2 2025-05-02 14:34 (tty2)

Opis:
– adam – użytkownik
– tty2 – terminal lokalny (np. fizyczna konsola)
– 14:34 – godzina logowania
– (tty2) – źródło sesji
id

Pokazuje identyfikatory użytkownika i grup, do których należy.

Przykład:
uid=1000(adam) gid=1000(adam) groups=1000(adam),27(sudo),46(plugdev),114(lpadmin)

Opis:
– uid – identyfikator użytkownika
– gid – identyfikator grupy głównej
– groups – wszystkie grupy, do których należy użytkownik
whoami

Pokazuje nazwę aktualnie zalogowanego użytkownika.
groups

Wyświetla wszystkie grupy, do których należy aktualny użytkownik.



Zarządzanie usługami i połączeniami sieciowymi

1. Wyświetlanie aktywnych usług

Polecenie:
systemctl list-units --type=service --state=running

Opis:
Wyświetla wszystkie aktualnie działające usługi zarządzane przez systemd.
Umożliwia szybką ocenę stanu systemu – co działa, jakie procesy są aktywne.

2. Sprawdzanie statusu konkretnej usługi

Polecenie:
sudo systemctl status NAZWA_USLUGI

Opis:
Pokazuje szczegółowy status wskazanej usługi, jej stan, logi, błędy startowe.
Przykłady:
sudo systemctl status ssh
sudo systemctl status snapd
sudo systemctl status cups
sudo systemctl status NetworkManager

3. Uruchamianie, zatrzymywanie i restartowanie usług

Polecenia:
sudo systemctl start NAZWA_USLUGI
sudo systemctl stop NAZWA_USLUGI
sudo systemctl restart NAZWA_USLUGI

Opis:
Służą do manualnego zarządzania usługami (uruchomienie, zatrzymanie, restart).

4. Włączanie i wyłączanie autostartu usług

Polecenia:
sudo systemctl enable NAZWA_USLUGI
sudo systemctl disable NAZWA_USLUGI

Opis:
Pozwalają zdecydować, czy dana usługa ma się uruchamiać automatycznie przy starcie systemu.

5. Sprawdzanie otwartych portów i nasłuchujących usług

Polecenie:
ss -tuln

Opis:
Pozwala zobaczyć, które usługi nasłuchują na portach sieciowych.
Przydatne do wykrywania otwartych serwisów TCP/UDP.
Parametry:
t – TCP
u – UDP
l – porty nasłuchujące
n – bez tłumaczenia nazw (czyste IP i numery portów)

6. Weryfikacja dostępności SSH

Polecenie:
sudo systemctl status ssh

Opis:
Sprawdza, czy SSH jest zainstalowane i aktywne.
Jeśli nie, system zwróci informację, że usługa nie istnieje.
To ważne – jeśli SSH nie działa, zdalny dostęp do systemu nie będzie możliwy.

Bezpieczne zarządzanie użytkownikami:

cat/etc/passwd 

- Trzeba znać lokalizację pliku etc/passwd
- Znaczenie UID:UID = 0 -> root -> imie konto z UID 0 inne niż znane = zagrorzenie
- shell bin/bash = konto może się logować
- jest to komenda do przeglądania
- /usr/sbin/nologin - oznacza, że konto nie ma dostępu do powłoki, nie może się zalogować czy to przez terminal czy SSH


sudo passwd -l adam - po tej operacji użytkownik adam nie będzie mogł się zalogować nawet jeśli zna hasło 

sudo passwd -pu adam  - odblokowanie konta

sudo usermod -s/usr/sbin/nologin NAZWA UŻYTKOWNIKA - blokuje powłoke logowania, po tej operacji nei można się zalogowac przez terminal 

sudo usermod -s /bin/bash user NAZWA UZYTKOWNIKA - przywraca powłokę bash

last - pokazuję historię logowania użytkowników do systemu. Dane są pobierane z pliku var/log/wtmp
last -n5 - jeśli chcę zobaczyć 5 ostatnich wpisów

lastlog - pokazuje aktywnosc  logowabniu każdego użytkownika w systemie nawet tcyh którzy się noigdy mnie logoewali 

Zastosowanie:  

Można szybko zobaczyć konta które nigdy się nie logowały(np. fałszywe),
weryfikacja podejżanych aktywności(np. logowanie w nietypowych godzinach),monitorowanie administratorów.

Należy zwrócić uwagę na:  

Konto z "never logged in" mogą btyć nieużywane lub podejżane
Konto root powinno mieć ostatnie logoewanie  ZNANE I UZASADNIONE

uptime - Pokazuje jak długo system działą od ostatniego uruchomienia oraz dane o obciążeniu systemu, dzięki temu mozna zorientoewać sie czy 
lpmputer był nieużywane (np. po incydencie), lub był niedawno rerstartowany.

cat/etc/shadow/grep'^adamn' zwraca zakodowane hasło, datę ostatniej zmiany hasłai inne informacje

awk - czyli wyszukiwanie  z UID = 0 i pustym hasłem, sprawdzanie kto ma uprawnienia root

awk -F: '$3 == 0{print $1}' /etc/passwd

awk to narzędzie do przetwarzania tekstu w liniach 

-F ustawia separator pól na dwukropek (bo w etc/passwd dane sa oddzielone :)
$3 == 0 oznacza jesli trzecie pole UID jest równe zero
{print $1} wypisz nazwę użytkownika ( pierwsze pole)\

Wyszukiwanie użytkowników z pustym hasłem czyli:

awk -F: '($2 == "") {print $1}' /etc/shadow 

użytkownik bez hasło może się zalogować bez żadnej weryfikacji to ogromna luka w bezpieczeństwie

chage -l adam 

POKAZUJE KIEDY UŻYTKOWNIK ADAM :
- ostatnjio zmienił hasło
- czy hasło wygasa i kiedy
- ile dni wcześniej system ostrzeże o konieczności zmiany
-  ile dni konto może być nieaktywner przed zablokowaniem


  Uprawnienia i bezpieczenstwo plikow systemolwych w Linuxie 

  1. /etc/passwd
Przykład:

bash
Kopiuj
Edytuj
-rw-r--r-- 1 root root 2622 Apr 30 12:00 /etc/passwd
Wyjaśnienie:

-rw-r--r-- — uprawnienia:

rw- – właściciel (root) może czytać i pisać;

r-- – grupa może tylko czytać;

r-- – inni użytkownicy mogą tylko czytać;

1 – liczba linków;

root – właściciel pliku;

root – grupa właściciela;

2622 – rozmiar pliku w bajtach;

Apr 30 12:00 – data i godzina modyfikacji;

/etc/passwd – ścieżka do pliku.

Bezpieczeństwo:
Plik ten powinien być czytelny dla wszystkich (żeby np. polecenia takie jak getent passwd działały), ale nie powinien być modyfikowalny przez nikogo poza rootem.

2. /etc/shadow
Przykład:

bash
Kopiuj
Edytuj
-r-------- 1 root shadow 1523 Apr 30 12:00 /etc/shadow
Wyjaśnienie:

r-------- – tylko root ma prawo odczytu;

Grupa to często shadow, ale domyślnie nie ma dostępu;

Pozostali nie mają żadnych uprawnień.

Bezpieczeństwo:
Ten plik przechowuje zahaszowane hasła użytkowników – dlatego musi być maksymalnie chroniony (tylko root może go czytać).

3. /etc/group
Przykład:

bash
Kopiuj
Edytuj
-rw-r--r-- 1 root root 1320 Apr 30 12:00 /etc/group
Wyjaśnienie:

rw- dla właściciela root;

r-- dla grupy;

r-- dla innych użytkowników.

Bezpieczeństwo:
Plik przechowuje listę grup i ich członków – powinien być czytelny, ale tylko root może go modyfikować.

4. /etc/sudoers
Przykład:

bash
Kopiuj
Edytuj
-r--r----- 1 root root 784 Apr 30 12:00 /etc/sudoers
Wyjaśnienie:

r-- – root może czytać;

r-- – grupa może czytać (czasem root lub sudo);

Brak uprawnień zapisu (to ważne);

Powinien być edytowany tylko przez visudo!

Bezpieczeństwo:
Ten plik kontroluje dostęp do polecenia sudo – każdy błąd może zablokować dostęp administracyjny.








