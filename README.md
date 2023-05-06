# Motoros védőfelszerelés webshop
Varga Bence Kornél, BAP88J - Informatika 2 házifeladat


## Rövid leírás
A webalkalmazásom egy motoros védőfelszerelés webáruház, ami PHP nyelven íródott, HTML és CSS technológiákat használva. A termékeket, felhasználókat, kosarak tartalmát és megrendelésekkel kapcsolatos információkat relációs adatbázisban tárolja. Az oldalon kétféle kinézet közül választhat a felhasználó és a kiválasztás/megváltoztatás után a továbbiakban már kiválasztott megjelenés lesz látható. Lehetőség lesz még a pénznem kiválasztására (EUR és HUF). A termékek böngészésére lehetőség van kijelentkezett állapotban is, de ekkor a kosár funkció nem működik. A megrendelés leadásásra a kosár oldalról lehet eljutni. Egy admin oldal is lesz, ahol a megfelelő jogosultsággal rendelkezve törölni és hozzáadni lehet termékeket.


## Főoldal
A főoldalon található lesz egy navigációs sáv, ahol a 4 termékkategória lesz megtalálható, a kosár és beállítások gombja, valamint ha a felhasználó be van jelentkezve, akkor kijelentkezés, egyéb esetben pedig bejelentkezés és regisztráció gombok. A navigációs sávon kívül a főoldalon egy bemutatkozó szöveg lesz megtalálható.


## Az adatbázis sémája

Termékek (products) tábla:
| Oszlop neve | Típus   | Leírás                       |
|-------------|---------|------------------------------|
| id          | INT     | Egyedi azonosító              |
| name        | VARCHAR | Termék neve                   |
| description | TEXT    | Termék leírása                |
| image       | VARCHAR | Termék képének elérési útvonala |
| price_huf   | DECIMAL | Termék ára forintban          |
| price_eur   | DECIMAL | Termék ára euroban            |
| category    | INT     | A termék kategóriájának azonosítója |

Felhasználók (users) tábla:
| Oszlop neve | Típus | Leírás |
| --- | --- | --- |
| id | INT | Egyedi azonosító |
| name | VARCHAR | Felhasználó neve |
| email | VARCHAR | Felhasználó email címe |
| password | VARCHAR | Felhasználó jelszava |
| admin | INT | Van-e a felhasználónak adminisztrátori joga (termék törlése vagy hozzáadása) |

Kosár (carts) tábla:
| Oszlop neve | Típus | Leírás |
| --- | --- | --- |
| id | INT | Egyedi azonosító |
| user_id | INT | A kosár tulajdonosának azonosítója |
| items | TEXT | Változó hosszúságú string, amely a kosárban lévő termékeket tartalmazza |

Megrendelések (orders) tábla:
| Oszlop neve | Típus | Leírás |
| --- | --- | --- |
| id | INT | Egyedi azonosító |
| user_id | INT | A megrendelés tulajdonosának azonosítója |
| items | TEXT | Változó hosszúságú string, amely a megrendelt termékeket tartalmazza |
| total_amount | DECIMAL | A megrendelés teljes összege |
| created_at | TIMESTAMP | A megrendelés létrehozásának ideje |
| shipping_address | TEXT | Szállítási cím |

Táblák leírása:
| Tábla neve | Oszlopok | Primary key | Foreign key |
| --- | --- | --- | --- |
| users | id, email, password, name, admin | id | - |
| products | id, name, category, price_huf, price_eur, description, image | id | - |
| cart | id, user_id, items | id | user_id (users) |
| orders | id, user_id, items, total_amount, created_at, shipping_address | id | user_id (users) |

A kosár és megrendelések táblában az items oszlop értékei tartalmazzák a termék azonosítóit és mennyiségét, például "1:2:6,3:1:7,5:3:8", ami azt jelenti, hogy az 1, 3 és 5 azonosítójú termékből 2, 1, illetve 3 darab található a kosárban, a harmadik szám pedig a méret.
