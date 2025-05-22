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

Plik zawiera listę wszystkich użytkowników w systemie. Każdy wiersz odpowiada jednemu użytkownikowi i zawiera:

    nazwę użytkownika

    UID (User ID) i GID (Group ID)

    katalog domowy

    powłokę logowania (shell)

Przykład wpisu:
adam:x:1000:1000:Adam,,,:/home/adam:/bin/bash

UID 0 zarezerwowany jest dla użytkownika root (pełne uprawnienia).
Obecność /bin/bash oznacza możliwość logowania do powłoki.
cat /etc/group

Wyświetla listę wszystkich grup użytkowników w systemie.

Dzięki grupom można zarządzać dostępem do zasobów takich jak pliki, urządzenia czy usługi.

Każdy użytkownik należy do co najmniej jednej grupy, a może należeć do wielu.

Przykład wpisu:
sudo:x:27:adam

Oznacza, że użytkownik adam należy do grupy sudo i może korzystać z polecenia sudo (czyli ma uprawnienia administratora).
who

Pokazuje wszystkich aktualnie zalogowanych użytkowników i źródła ich sesji.

Przykład:
adam tty2 2025-05-02 14:34 (tty2)

    adam – użytkownik

    tty2 – terminal lokalny (np. fizyczna konsola)

    14:34 – godzina logowania

    (tty2) – źródło sesji

id

Wyświetla identyfikatory użytkownika i listę grup, do których należy.

Przykład:
uid=1000(adam) gid=1000(adam) groups=1000(adam),27(sudo),46(plugdev),114(lpadmin)

    uid – identyfikator użytkownika

    gid – identyfikator grupy głównej

    groups – wszystkie grupy, do których należy użytkownik

whoami

Pokazuje nazwę aktualnie zalogowanego użytkownika (tego, który uruchomił terminal).
groups

Wyświetla wszystkie grupy, do których należy zalogowany użytkownik.
Pozwala sprawdzić, czy ma dostęp np. do poleceń administracyjnych (jak sudo).














