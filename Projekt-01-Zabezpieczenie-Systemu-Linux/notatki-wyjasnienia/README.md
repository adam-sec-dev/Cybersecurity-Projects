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

 cat /etc/group

Wyświetla zawartość pliku /etc/group, czyli listę wszystkich grup systemowych i użytkowników w nich zawartych.

    Grupy służą do zarządzania dostępem i uprawnieniami.

    Użytkownik może należeć do jednej lub wielu grup.

    Można nimi kontrolować dostęp do plików, urządzeń, usług (np. sieci, drukarki).

Przykład:
sudo:x:27:adam

Gdzie:

    sudo – nazwa grupy

    x – hasło (zazwyczaj niewidoczne – x)

    27 – GID (Group ID)

    adam – użytkownik należący do tej grupy

 who

Wyświetla listę aktualnie zalogowanych użytkowników i ich sesji.

Przykład:
adam tty2 2025-05-02 14:34 (tty2)

Opis:

    adam – nazwa użytkownika

    tty2 – fizyczna konsola (terminal nr 2)

    2025-05-02 14:34 – czas logowania

    (tty2) – źródło sesji

 Przydatne w systemach serwerowych do wykrywania nieautoryzowanych logowań.
 id

Wyświetla szczegóły aktualnie zalogowanego użytkownika:

Przykład:
uid=1000(adam) gid=1000(adam) groups=1000(adam),27(sudo),46(plugdev),114(lpadmin)

Składniki:

    uid=1000(adam) – identyfikator użytkownika

    gid=1000(adam) – identyfikator głównej grupy

    groups=... – lista wszystkich grup, do których użytkownik należy

🔹 whoami

Zwraca nazwę aktualnie zalogowanego użytkownika.
To skrótowe polecenie pomocne przy szybkim sprawdzeniu, kim jesteś w systemie.
🔹 groups

Wyświetla listę grup przypisanych do aktualnie zalogowanego użytkownika.
Przykład: adam sudo plugdev lpadmin

 Grupa sudo oznacza, że użytkownik ma uprawnienia administracyjne.












Użytkownicy tej grupy mogą używać komendy sudo.

