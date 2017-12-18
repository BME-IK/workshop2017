# Workshop gyakorlat

## Egyszerű gépindítás

Jelentkezzen be, majd indítson gépet a CIRCLE felhasználói felületén!
Az indításhoz válasszon ki egy Ubuntu sablont a listából!

Az események fülön jelzést kap a gép elindulásáról.
Ha megkapta jelzést, másolja a vágólapra az SSH csatlakozási parancsot,
majd jelenkezzen be a virtuális gépre!

Írja be az `uname -a` parancsot!
Írja be az `nproc` parancsot!
Jól látható a virtuális gép egy processzorral rendelkezik.

Állítsa le gépet, majd a felhasználói felületen az Erőforrások fülön
növelje meg processzorok számát 2-re!
Mentse el a beállítást majd indítsa el ismét a virtuális gépet!
Ellenőrizze a processzorok számát ahogy azt nem rég is tette!

## Környezet telepítlés és megosztás
Telepítse az nginx webszervert!
```bash
    sudo apt update
    sudo apt install nginx
```
A telepítés után az nginx már fut.
A CIRCLE felhasználói felületén kattintsunk a Hálózat fülre, majd nyissuk ki a 
80-as portot a tűzfalon.
A port nyitás átnavigál minket az Események fülre.
Navigáljunk vissza a Hálózat-hoz.
A virtuális gép 80-as portját egy véletlen szerű portszám értékhez rendelte hozzá
a tűzfal modul.
Segítségképpen a felhasználó felület a gépünk elérhetőségét linkként jeleníti meg.
Kattintsunk a linkre majd ellenőrizzük betölt-e az nginx köszöntő oldala!

Módosítsuk a `/usr/share/nginx/html/index.html` fájlt, írjuk be a nevünket a **h1** tagbe!
Ellenőrízzuk a változást!

A felhasználói felületen a Hozzáférés fülön ossza meg a gépet a szomszédjával!
Garázdálkodjon kedvére a a kapott gépen!

## Template készítése
Kattintson a floppy lemez ikonra majd mentse el virtuális gépet sablonként!
A sablon neve tartalmazza az ön nevét!
A mentés befejézése után ossza meg a sablont a szomszédjával!
Törölje le a virtuális gépet!

Majd, indítson virtuális gépet a szomszédjától kapott sablonból!

## Diszk hozzáadása
Adjon hozzá újdiszket a virtuális géphez, az Erőforrások fülön!
Formázza meg a kedvenc fájlrendszerére majd csatolja fel a /mnt alá!

```bash
    sudo mkfs.ext4 /dev/vdb
    sudo mount /dev/vdb /mnt
```

A felhasználói felületen nyújtson be átméretezési kérvényt az adminisztrátornak!
Nagyobb méretet igényeljen mint a jelenlegi!
Az igény elfogadásáról kapni fog értesítést a felületen.

Ellenőrizze a fájlrendszer jelenlegi méretét, majd csatolja le azt!
```bash
    sudo df -h
    sudo umount /mnt
```
Az átméretezést elfogadó értesítés után, a lemez mérete megváltozik.
Méretezzük át a fájlrendszert majd csatoljuk fel a /mnt alá és ellenörizzük a méretét.
```bash
    sudo e2fsck -f /dev/vdb
    sudo resize2fs /dev/vdb
    sudo mount /dev/vdb /mnt
```

## Kiegészítő szolgáltatások
A felhasználói felületen a Kezdőlap fülön kattintsunk a táhely csatolása gombra!
A virtuális gépen belül /store elérési út alá már felcsatolásra is került a felhasználói
perzisztens tár.
Hozzon létre fájlokat /store alá!
A felhasználói felület főoldalán a Fájlok dobozban megjelennek a létrehozott fájlok.
Itt igényszerint fájlokat tölthet le, illetve újakat is tölthet fel kívűlről a tárhelyre.

Lehetőség nyilik ssh kulcsok feltöltésére egy gombnyomásra.
Ehhez generáljuk egy ssh kulcsot a kliens gépen.
```bash
    ssh-keygen  # majd 3 enter
    cat ~/.ssh/id_rsa.pub
```
Jelenítse meg a publikus kulcsot a parancssorban majd, másoljuk a vágólapra!

Navigáljon a CIRCLE-ben a profilunkhoz (a menüben a felhasználó nevünkre kattíntva)!
Lentebb kattintson az SSH kulcs hozzáadása gombra!
Másolja be a kulcsot, nevezze el, majd mentse el!

Navigáljon vissza a virtuális gépünk kezdő oldalára majd kattintson az SSH kulcs hozzáadása gombra!
A kulcs felmásolódott a gépre.
Probáljon meg jelszó helyett kulcs segítségével bejelentkezni.

## VNC konzol

Tipikus probléma mikor sikerül kizárni magunkat a virtuális gépről.
Egy mentő őv a VNC konzol.

Zárja ki magát a virtuális gépről az alábbi parancs segítségével!
```bash
    sudo iptables -I INPUT -j REJECT
```

Most próbáljon meg ssh-zni! Láthatóan nem működik, sikeresen kizárta magát!
A felhasználói felületen navigáljon a Konzol fülre, ekkor megjelenik a gép konzolja!
Írja be a felhasználó nevet, majd kattintson a Jelszó begépelése gombra, a jelszó beírásához!

A sikeres bejelentkezés után adja ki az alábbi parancsot, hogy ismét szabadon hozzáférjen a géphez
SSH-n keresztül is!
```bash
    sudo iptables -D INPUT -j REJECT
```

Ha mindent jól csinált, akkor ismét müködni fog az SSH hozzáférés.
