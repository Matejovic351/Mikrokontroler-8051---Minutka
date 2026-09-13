# Mikrokontroler-8051---Minutka
Projekt minutky na mikrokontroleru 8051 programovaného v jazyku assember. Použitý software MCU ide. Konfigurace uvedena v README.


Konfigurace:

2 porty:   k portu 1 je připojena klasická klávesnice
           k portu 3 je připojen klasický 4x 7segmentový displey

Jedná se o krátký program takže není potřeba řešit paměť. Časově je naprosto přesný na 10 minut žádná odchylka. 

Kód je napsán začátečníkem na procvičení základů programovacího jazyka assember. Kód je řádně okomentovaný.


Jak program Spustit?

Potřebný hardware je klasické USB a Převodník USB-UART. Komunikace PC-8051 probíhá přes komunikaci USART její konfigurace je vás.

Soubor .ASM obsahuje okomentovaný kód. Soubor .hex je připraven k nahrání přes USART komunikaci.
