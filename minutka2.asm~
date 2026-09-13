disp equ P3          ; port P3 ovládá displej
klv equ P1           ; port P1 čte tlačítka
 
org 0                ; začátek programu v paměti
	jmp start        ; přeskočení na hlavní část

start:
	mov R3, #0       ; nastav sekundy na 0
	mov R4, #0       ; nastav minuty na 0
 
smycka:
	call displej     ; zobraz aktuální čas
	call zpomal      ; krátké zpomalení programu
	call tlacitka    ; načtení stisku tlačítka do registru A

	cjne A, #2, dale1 ; kontrola hodnoty tlačítka
	inc R4           ; přičtení 1 minuty
	cjne R4, #60, dale1 ; kontrola limitu minut
	mov R4, #0       ; vynulování minut při 60

dale1:
	cjne A, #5, dale2 ; kontrola tlačítka
	dec R4           ; odečtení 1 minuty
	cjne R4, #255, dale2 ; kontrola podtečení
	mov R4, #59      ; nastavení na 59

dale2:
	cjne A, #3, dale3 ; kontrola tlačítka
	inc R3           ; přičtení 1 sekundy
	cjne R3, #60, dale3 ; kontrola limitu sekund
	mov R3, #0       ; vynulování sekund

dale3:
	cjne A, #6, dale4 ; kontrola tlačítka
	dec R3           ; odečtení 1 sekundy
	cjne R3, #255, dale4 ; kontrola podtečení
	mov R3, #59      ; nastavení na 59

dale4:
	cjne A, #16, dale5 ; kontrola start tlačítka
	call cas         ; spuštění odpočtu času
	call blikej      ; spuštění blikání displeje

dale5:
	jmp smycka       ; návrat na začátek smyčky
 
blikej:
	mov disp, #00001111b ; zobrazení na displeji
	mov disp, #00011111b ; změna zobrazení
	mov disp, #00101111b ; změna zobrazení
	mov disp, #00111111b ; změna zobrazení
	call zpomal      ; krátká pauza
	call displej     ; zobrazení času
	call zpomal      ; krátká pauza
	call tlacitka    ; načtení tlačítka
	cjne A, #9, blikej ; opakování blikání
	ret              ; návrat
 
tlacitka:
	mov A, klv       ; načtení stavu tlačítek
	cpl A            ; převrácení bitů (1 ↔ 0)
	ret              ; návrat
 
cas:
	call displej     ; zobrazení času
	call pauza_1s    ; čekání 1 sekundu
	
	dec R3           ; snížení sekund o 1
	cjne R3, #255, cas1 ; kontrola podtečení
	mov R3, #59      ; nastavení sekund na 59
	
	dec R4           ; snížení minut o 1
	cjne R4, #255, cas1 ; kontrola podtečení
	mov R4, #0       ; vynulování minut
	mov R3, #0       ; vynulování sekund
	ret              ; konec odpočtu

cas1:
	call tlacitka    ; načtení tlačítka
	cjne A, #32, cas ; pokračování odpočtu
	ret              ; ukončení odpočtu
		
displej:
	mov A, R3        ; načtení sekund
	mov B, #10       ; nastavení dělitele
	div AB           ; rozdělení na desítky a jednotky
	mov disp, B      ; zobrazení jednotek sekund
	orl A, #00010000b ; nastavení pozice na displeji
	mov disp,A       ; zobrazení desítek sekund

	mov A, R4        ; načtení minut
	mov B, #10       ; nastavení dělitele
	div AB           ; rozdělení na desít ky a jednotky
	orl A , #00110000b ; nastavení pozice
	mov disp, A      ; zobrazení desítek minut
	mov A, B         ; načtení jednotek minut
	orl A,#00100000b ; nastavení pozice
	mov disp, A      ; zobrazení jednotek minut
	ret              ; návrat
 
zpomal:
	mov R5, #1       ; nastavení krátké smyčky
	jmp cekej        ; skok na čekání
 
pauza_1s:
	mov R7, #185     ; nastavení počítadla
	mov R6, #205     ; nastavení počítadla
	mov R5, #4       ; nastavení počítadla
 
cekej:
	djnz R7, cekej   ; opakování smyčky R7
	djnz R6, cekej   ; opakování smyčky R6
	djnz R5, cekej   ; opakování smyčky R5
	ret              ; návrat

end                ; konec programu