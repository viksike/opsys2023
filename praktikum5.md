# Praktikum 5 aruanne

Viiendas praktikumis lahendasime ülesandeid linuxi käsureal. Sellele praktikumile kulus kokku umbes 1.5 tundi ja esimest korda jõudsin suurema osa materjalist praktikumitunnis juba valmis. Tunnen, et mõistan nüüd ubuntu käsurida veidi paremini ja ei tee kogu aeg liigseid käske. Järgnevalt on lisatud nii vastused küsimustele kui ka vajalikud kuvapaugud.

	•	Ülesanne 5-1:
	◦	a) Kaustale on vaja execute ja failile read õiguseid.
	◦	b) Kaustale on vaja write ja execute ning failile write õiguseid.

	•	Ülesanne 5-2: Kuna sisu on vaja teada, et skripti käivitada, on vaja lisaks executeile ka read õigust. Vastasel juhul ei saa teada, mida üldse käivitada.


	•	Ülesanne 5-3: Igale kasutajale on oma grupp kasulik, sest sel juhul pole kasutajad ühes samas "users" grupis, seega ei saa tavakasutajad ligipääsu teiste kasutajate failidele ja andmetele


	•	Ülesanne 5-4: Read õigused
 ![Screenshot 2023-10-09 at 11 13 42](https://github.com/viksike/opsys2023/assets/144438506/4f76e955-21e0-4319-97f0-a903aefba825)

￼

	•	Ülesanne 5-5: 
 ![Screenshot 2023-10-09 at 11 38 42](https://github.com/viksike/opsys2023/assets/144438506/e5ab615e-0c9a-47a2-b20d-e56c2a982f2d)

￼

	•	Ülesanne 5-6:	Jah, sest setuid kasutamisel võib mõni kasutaja saada root ligipääsu, kui programm/fail on setuid’ga seadistatud käivituma root õigustega, kuigi talle seda otseselt antud ei ole. Peamiselt kehtib see tundlike andmete puhul, muidu otsest ohtu pole.
	•	
	•	Ülesanne 5-7: Kustutada saavad opetaja, root ja peeter.


	•	Ülesanne 5-8: 
 <img width="521" alt="Screenshot 2023-10-10 at 13 23 39" src="https://github.com/viksike/opsys2023/assets/144438506/03f1d21a-3c24-43fe-a81d-4d317cc12016">


	•	Ülesanne 5-9: Modifitseerida ei saa keegi. Faili saab kustutada, kui kõigepealt sisestada sudo chattr -i testfail-2 ja pärast rm testfail-2.


