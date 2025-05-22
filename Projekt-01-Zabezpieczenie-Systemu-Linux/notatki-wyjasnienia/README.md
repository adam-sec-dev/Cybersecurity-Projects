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

systemctl list-units --type=service --state=running

Wyświetla wszystkie aktualnie działające usługi (w stanie „running”) zarządzane przez systemd.
Dzięki temu można sprawdzić, co dokładnie działa w tle w systemie Linux (np. NetworkManager, ssh, snapd).
Polecenie bardzo przydatne do diagnostyki i podstawowego audytu systemu.
2. Sprawdzanie statusu konkretnej usługi

sudo systemctl status NAZWA_USLUGI

Wyświetla szczegółowy status podanej usługi — m.in. czy jest aktywna, logi startowe, czas działania.
Przykłady:

    sudo systemctl status ssh

    sudo systemctl status snapd

    sudo systemctl status cups

    sudo systemctl status NetworkManager

Jeśli usługa nie istnieje, system zwróci komunikat „Unit ... could not be found.”
3. Uruchamianie, zatrzymywanie i restartowanie usług

sudo systemctl start NAZWA_USLUGI
sudo systemctl stop NAZWA_USLUGI
sudo systemctl restart NAZWA_USLUGI

    start – uruchamia usługę natychmiast,

    stop – zatrzymuje działanie usługi,

    restart – wykonuje restart.

4. Włączanie i wyłączanie autostartu usług

sudo systemctl enable NAZWA_USLUGI
sudo systemctl disable NAZWA_USLUGI

    enable – usługa automatycznie uruchamiana przy starcie systemu,

    disable – usługa nie będzie startować automatycznie.

5. Sprawdzanie otwartych portów i usług nasłuchujących

ss -tuln

    -t – tylko TCP,

    -u – tylko UDP,

    -l – tylko porty nasłuchujące,

    -n – bez rozwiązywania nazw (adresy IP i numery portów, a nie „http”, „localhost” itp.).

To polecenie pozwala ustalić, które usługi aktualnie nasłuchują połączeń.
Używane w praktyce do bezpieczeństwa, np. do wykrywania nieautoryzowanych serwisów działających w tle.
6. Weryfikacja stanu SSH

sudo systemctl status ssh

Jeśli SSH nie jest zainstalowany, system zwróci komunikat:
Unit ssh.service could not be found.

