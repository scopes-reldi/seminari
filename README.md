# Upute za praktične zadatke iz lingvističke obrade i ekstrakcije varijabli iz korpusa

Namena ovih praktičnih zadataka je simulirati postupak lingvističke obrade korpusnih podataka te ekstrakcije varijabli iz obrađenih podataka. Ekstrahirani će se podaci koristiti danas za mašinsko učenje te sutra za statistički opis i zaključivanje.

## Tehnički preduvjeti

Ove vežbe prilagođene su radu na OS Microsoft Windows XP (no radiće minimalno izmenjene i na drugim MS OS-ovima) s instaliranim Pythonom 2.7.9+ (vežbe su proverene na verziji 2.7.13). Prilikom instalacije Pythona potrebno je odabrati instalaciju pip-a te postavljanje Pythona u putanju (<i>path</i>).

## Dodatni materijali za učenje programiranja u Pythonu

Unutar ovih vežbi koristićemo gotove Python skriptove u koje ćemo minimalno intervenirati.

Za učenje osnova programiranja u Pythonu preporučujemo materijale prilagođene lingvistima koji su dostupni na https://github.com/nljubesi/python-for-linguists.

## Preuzimanje i instalacija biblioteke ReLDI

Pokrenite komandni prompt:

* Kliknite na Start/Run
* Ukucajte `cmd` u dato polje (ukoliko već nije ukucano)

Uđite u direktorijum Python27

```  
$ cd c:\Python27
```

Izlistajte sadržaj

```
$ dir
```

Uđite u direktorijum Scripts

```
$ cd Scripts
```

Izlistajte sadržaj. Ukoliko se u spisku nalazi pip.exe, možete preći na instalaciju ReLDI biblioteke komandom  

```
$ pip install reldi
```

Kako biste proverili da li je biblioteka dobro instalirana, otvorite Python interaktivno

```
$ python
```

Uvezite biblioteku komandom

```
$ import reldi
```

Ukoliko program ne javlja nikakve greške, biblioteka je instalirana i spremna za korišćenje. Vratite se u komandni prompt pomoću

```
$ Ctrl+Z
```


## Obrada teksta pomoću ReLDI biblioteke

Obrada teksta uključuje pokretanje programa za tokenizaciju, lematizaciju i morfološko tagiranje nad zadatim tekstovima. Programi se izvršavaju daljinski (na serveru), a pokreću se pozivom skripta `tag_all.py`. Materijali pripremljeni za isprobavanje obrade nalaze se u repozitorijumu [https://github.com/scopes-reldi/seminari](https://github.com/scopes-reldi/seminari), koji treba sačuvati na lokalnom računaru (Clone or downlowad/Download ZIP). 

Sačuvana arhiva će se nalaziti u direktorijumu "Downloads". Otvorite i otpakujte arhivu (Extract to).  Kao lokaciju za otpakovan direktorijum odaberite "Local Disk (C:)". Time ćete na lokalnom disku kreirati direktorijum "seminar-master".
 
Pronađite i razgledajte direktorijum. Zatim se vratite u komandni prompt i dođite do istog direktorijuma pomoću komande  

```
$ cd <neki direktorijum>
```

Za promenu direktorijuma na gore koristi se komanda

```
$ cd ..
```

Tekstovi nad kojima ćemo isprobati obradu nalaze se u pod-direktorijumu "proba". Kada se nađete u direktorijumu "seminar-master", proverite da li on sadrži skript `tag_all.py` i direktorijum "proba". Ako je sve tu, onda možemo da pokrenemo obradu teksta komandom 

```
$ python tag_all.py hr proba
```

koja poziva ReLDI servise i obrađuje sve datoteke s ekstenzijom ```.txt``` u zadatom direktorijumu. Obrađen tekst je sačuvan u datotekama sa ekstenzijom ```.taglem``` u zadatom direktorijumu.

Segment ```hr``` definiše jezik na kom su napisani ulazni tekstovi, a ```proba``` direktorijum u kom se tekstovi nalaze.  

Program će tražiti lozinku. Za ovu priliku, pipremili smo probnu lozinku koja je ista za sve korisnike. Za kasnije korišćenje potrebno je otvoriti sopstveni nalog za ReLDI servise, prateći uputstva na [http://nl.ijs.si/services](http://nl.ijs.si/services). Kad dobijete nalog, korisničko ime treba uneti u kod skripta, a lozinka se unosi pri izvršavanju.  

Datoteke koje su obrađene za potrebe statističkih vežbi nalaze se u pod-direktorijumima "hrwac", "srwac.cyr", "srwac.lat". Kako bismo izbegli dugu obradu te moguće preopterećenje web servisa, ove datoteke su unapred obrađene na isti način kao i probne, dakle pokretanjem:

Za sada **ne pokretati**!  
```
$ python tag_all.py hr hrwac
$ python tag_all.py sr srwac.cyr
$ python tag_all.py sr srwac.lat
```

## Ekstrakcija podataka pomoću namenskog programa

Obrađene datoteke se dalje mogu dati kao input za ekscerpciju podataka. Skript ```extract.py```, koji se nalazi pod "seminar-master", napisan je namenski za ove vežbe. Pokreće se na sledeći način
 
```
$ python extract.py hrwac hrwac
$ python extract.py srwac.cyr srwac
$ python extract.py srwac.lat srwac
```

i proizvodi tabularne datoteke, gde kolone sadrže vrednosti unapred određenih varijabli. Prvi segment nakon imena skripta (```(hrwac|srwac.cyr|srwac.lat)```) definiše direktorijum u kom se nalaze obrađene datoteke, a drugi (```(hrwac|srwac|srwac)```) definiše referentni korpus koji se koristi za izračunavanje vrednosti nekih od varijabli. Izlaz ovih skripti nalazi se u datotekama  ```(hrwac|srwac.cyr| srwac.lat).out(1|2)```. 

Kao poslednji korak u pripremi podataka za R, potrebno je ekscerpirane varijable sačuvati u datotekama tipa  ```.tsv```, tako što će se sadržaj svih izlaznih datoteka sa indeksom 1 spojiti u ```reldi1.tsv```, sa indeksom 2 u ```reldi2.tsv```. Treba voditi računa o tome da konačni ```.tsv``` dokument može sadržati samo jedno zaglavlje. 

Konačno, proveru valjane strukture svojih ```tsv``` datoteka možete proveriti skriptom ```check_tsv.py``` koji kao argument prima ```tsv``` datoteku te ispisuje brojeve linija koje imaju drugačiji broj argumenata od prve linije.

```
python check_tsv.py reldi1.tsv
```

U slučaju da nema ispisa, datoteke su verovatno ;-) u redu.

## Mašinsko učenje na ekstraktima

Kao zamenu za predavanje po pozivu pripremili smo iPython beležnicu [Machine learning example.ipynb](https://github.com/scopes-reldi/seminari/blob/master/Machine%20learning%20example.ipynb) u kojoj prikazujemo predikciju jezika / korpusa na temelju drugih varijabli prisutnih u datoteci ```reldi2.tsv```.

What follows is... RRRRR!
