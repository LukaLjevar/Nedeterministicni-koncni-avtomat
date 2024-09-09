# Nedeterministični Mooreov avtomat - iskalnik podniza
Projektna naloga pri predmetu Programiranje 1.

Projekt vsebuje implementacijo nedeterminističnega Moorovega avtomata, ki kot vhod sprejme dva niza - niz1 in niz2. Nato avtomat preveri, ali niz2 vsebuje niz1 kot strnjeni podniz. Na podlagi prejetega niza1, program pripravi avtomat, ki bo preverjal, ali nek niz vsebuje niz1 kot podniz. Avtomat je nedeterminističen, kar pomeni, da se lahko nahaja v večih stanjih naenkrat. Niz2 je sprejet, če je po koncu izvajanja programa vsaj eno izmed (lahko večih) stanj, v katerih se nahaja avtomat, sprejemno. Avtomat je opremljen še z dodatno funkcijo, odvisno od trenutnih stanj, ki po koncu izvajanja enega preverjanja vrne element tipa unit in natisne seznam vseh trenutnih stanj. Zato govorimo o Moorovem avtomatu. 

## Matematična definicija
Nedeterministični Mooreov avtomat opišemo kot šesterico $(S, \ s_{0}, \ \Sigma , \ O, \ \delta , \ G)$, kjer je: 
- $S$ končna množica stanj, v katerih se lahko avtomat nahaja,
- $s_{0} \in S$ začetno stanje, torej stanje, v katerem avtomat prične,
- $\Sigma$ končna množica simbolov oziroma abeceda, ki jo sprejme naš avtomat,
- $O$ končna množica simbolov, ki jo naš avtomat vrača,
- $\delta :S'\times \Sigma \rightarrow S''$ prehodna funkcija, ki $S' \subset S$ preslika v $S'' \subset S$, torej starim stanjem priredi nova stanja,
- $G: S' \rightarrow O$ izhodna funkcija, ki trenutnim stanjem $S' \subset S$ priredi izhod.

V primeru iskalnika podniza, iz niza1 generiramo množico stanj na naslednji način. Najprej ustvarimo **začetno stanje (-1, 'X')**. Če je niz1 prazen, je to tudi edino stanje. Sicer vsakemu znaku x v nizu1 priredimo stanje, predstavljeno s parom indeksa tega znaka x v nizu1 in tem znakom x. Množico stanj bomo v tej implementaciji predstavili s **tabelo**. Če torej za niz1 vnesemo *"anbanpetpodgan"*, dobimo naslednjo tabelo stanj: 
[|(-1, 'X'); (0, 'a'); (1, 'n'); (2, 'b'); (3, 'a'); (4, 'n'); (5, 'p'); (6, 'e'); (7, 't'); (8, 'p'); (9, 'o'); (10, 'd'); (11, 'g'); (12, 'a'); (13, 'n')|]. Za predstavitev stanj z urejenimi pari sem se odločil zato, da ločimo med sabo iste črke, kadar se neka črka v nizu1 pojavi večkrat, na primer črka 'p' v *"anbanpetpodgan"*. Poleg indeksa pa sem na drugo komponento dodal še znak zato, da lahko vhodni znak iz niza2 kar takoj primerjamo z znaki iz niza1.

## Kako avtomat deluje?
![Screenshot 2024-09-09 072945](https://github.com/user-attachments/assets/2ad4af0c-d0f5-4563-9431-19af87b269e8)


## avtomat.ml
Na začetnute datoteke definiramo funkcijo, ki iz niza1 tvori ustrezno tabelo možnih stanj. S pomočjo te tabele bomo ustvarili avtomat, ki išče ta podniz. Definiramo tudi njen "inverz", ki ustrezno tabelo stanj pretvori nazaj v niz. To funkcijo bomo potrebovali zato, da lahko tekstovni vmesnik natisne iskani niz1. Sprejemno stanje je preprosto zadnje mesto v tabeli. Ker je avtomat nedeterminističen, je lahko v večih stanjih hkrati. Seznam trenutnih stanj je implemntiran s seznamom, zato da lahko zlahka dodajamo na začetek. Prehode definiramo s pomočjo dveh funkcij. Prva enemu izmed trenutnih stanj priredi vsa naslednja stanja, druga pa združi slike vseh posameznih stanj v niv seznam. Sledi definicija tipa avtomat in navodilo, kako iz danega niza1 ustvariti avtomat, ki bo ta niz iskal v drugih nizih. Tako lahko ustvarimo različne avtomate, glede na to kateri niz1 smo vnesli na začetku. Na koncu definiramo še izhodno funkcijo v odvisnosti od trenutnih stanj in tako iz končnega avtomata ustvarimo Mooreov avtomat.
## stanje.ml
Stanja sem implementiral z urejenim parom int * char. Nato te urejen pare v datoteki avtomat.ml zložim v tabelo in na ta način predstavim množico stanja avtomata.
## trak.ml
V tej datoteki definiramo tip trakov, ki jih bomo ustvarili iz niza2, torej niza v katerem bomo iskali podniz. Trak je implementiran z zapisnim tipom, ki na prvi komponenti hrani niz, na drugi pa indeks trenutnega znaka, tj. na katerem indeksu niza2 se trenutno nahajamo. Nato definiramo pomožne funkcija za delo s trakovi. Z njihovo pomočjo določimo indeks trenutnega znaka na traku, ali se nahajamo na koncu traku, se premaknemo do naslednjega znaka na traku, it niza tvorimo trak in iz traku tvorimo niz.
## zagnani_avtomat.ml
Tukaj definiramo tip zagnanega avtomata, ki ga predstavimo z zapisnim tipom, ki vsebuje avtomat, trak in seznam trenutnih stanj avtomata. Definiramo, kako se naj avtomat premika med stanji in funkcijo, ki sporoča, ali je katero izmed trenutnih stanj, v katerih se avtomat nahaja sprejemno.

## Navodila za uporabo
**TO DO**

