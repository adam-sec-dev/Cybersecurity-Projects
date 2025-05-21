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




ZARZDZANIE URZYTKOWNIKAMI I GRUPAMI W SYSTEMIE LINUX



cat /etc/passwd

Plik /etc/passwd zawiera dane wszystkich użytkowników systemu. Każdy wiersz odpowiada jednemu użytkownikowi i zawiera informacje takie jak:

    nazwa użytkownika,

    identyfikator UID i GID,

    katalog domowy,

    oraz shell (powłoka logowania).

   Np. adam:x:1000:1000:Adam,,,:/home/adam:/bin/bash

Użytkownicy, którzy posiadają /bin/bash jako powłokę, mogą logować się do systemu.
Użytkownik root ma UID 0 i pełne uprawnienia administracyjne.


cat /etc/group

Wyświetla zawartość pliku /etc/group, czyli listę wszystkich grup użytkowników w systemie Linux.

    W systemie Linux grupy służą do zarządzania uprawnieniami.

    Dzięki nim można ustawić, kto ma dostęp do jakich zasobów (np. plików, urządzeń, drukarek, sieci).

    Każdy użytkownik należy do co najmniej jednej grupy, a może należeć do wielu.

    Np. sudo:x:27:adam

sudo	Nazwa grupy
x	Hasło (zazwyczaj niewidoczne – x)
27	GID – Group ID
adam	Lista użytkowników należących do tej grupy


who

Komenda who pokazuje listę aktywnych sesji użytkowników.

Przydatna do sprawdzenia, kto jest aktualnie zalogowany do systemu lokalnie lub zdalnie.

W systemach wieloużytkownikowych lub serwerowych pozwala szybko wykryć nieautoryzowane logowania.

Np. adam     tty2         2025-05-02 14:34 (tty2)


adam – zalogowany użytkownik

tty2 – fizyczna konsola (terminal 2)

2025-05-02 14:34 – czas logowania

(tty2) – źródło sesji


id – informacje o aktualnym użytkowniku

Polecenie id wyświetla identyfikatory użytkownika i grup, do których należy aktualnie zalogowany użytkownik.

Np. uid=1000(adam) gid=1000(adam) groups=1000(adam),27(sudo),46(plugdev),114(lpadmin)


uid=1000(adam) – identyfikator użytkownika (user ID),

gid=1000(adam) – identyfikator grupy głównej (group ID),

groups=... – wszystkie grupy, do których użytkownik należy.


whoami – nazwa aktualnie zalogowanego użytkownika

Wyświetla nazwę użytkownika aktualnie zalogowanego w tej sesji terminala.


groups – lista grup użytkownika

Polecenie groups wyświetla wszystkie grupy, do których należy aktualnie zalogowany użytkownik.












Użytkownicy tej grupy mogą używać komendy sudo.

