OpenBook – ESP32-C6 Based E-Paper System

OpenBook este un proiect open-source care integrează un microcontroler ESP32-C6 cu un ecran e-paper și senzori de mediu, orientat către aplicații portabile cu consum redus. 
Proiectul pune accent pe eficiență energetică, flexibilitate în conectivitate și ușurință în depanare.

Funcționalitate Hardware:
La baza acestui design stă ESP32-C6-WROOM-1-N8, care asigură atât conectivitate modernă (Wi-Fi 6 și Bluetooth 5.0 LE), cât și controlul perifericelor externe. Dispune de un procesor tactat la 160 MHz, 512 KB de SRAM și 8 MB de memorie Flash. Datorită numărului mare de pini GPIO, permite o gamă largă de interfețe.

Microcontrolerul gestionează:
Afisajul e-paper prin interfață SPI.
Senzorii de mediu pentru date ambientale.
Interacțiunea cu utilizatorul prin butoane tactile și LED-uri.
Monitorizarea și încărcarea bateriei prin USB-C.

Arhitectura Sistemului

Ecran E-Paper
Interfața de comunicare este SPI (pinii IO12, IO11, IO5, IO4).
Ecranul este controlat de driver-ul BD5229G-TR, care generează tensiunile necesare.
Alimentarea este comutată cu ajutorul unor MOSFET-uri pentru a permite oprirea completă atunci când ecranul nu este utilizat.

Senzor de Mediu – BME688
Măsoară temperatura, umiditatea, presiunea atmosferică și calitatea aerului (VOC).
Comunicarea se face prin magistrala I2C (pinii IO8 și IO10).
Funcționează la 3.3V și oferă date precise cu consum redus.

Card Micro SD
Este conectat prin SPI (pin IO7). Se folosește pentru stocare externă de date.

Modul RTC – DS3231
Se conectează prin aceeași magistrală I2C cu senzorul BME688. Păstrează ora și data în mod autonom, chiar și fără alimentare principală.

Sistem de Alimentare
Dispozitivul este alimentat de o baterie Li-Po de 3.7V, 2500 mAh.
Încărcarea este controlată de MCP73831, care permite un curent maxim de 500 mA prin portul USB-C.
Starea bateriei este monitorizată de modulul MAX17048G+T10, care oferă informații despre nivelul de încărcare și starea generală a acumulatorului.
Profil de Consum Estimat

În activitate cu Wi-Fi și e-paper: aproximativ 150 mA
În standby cu ecran static și fără activitate radio: aproximativ 10 mA
În deep sleep: peste 50 µA
Autonomia medie estimată este de aproximativ 250 de ore la un consum de 10 mA.

Alocarea Pinilor ESP32-C6
E-paper Display: IO12, IO11, IO5, IO4 – SPI (control și resetare)
Senzor BME688: IO8, IO10 – I2C (partajat cu RTC)
Card SD: IO7 – SPI (stocare externă)
Modul RTC: IO8, IO10 – I2C (ceas în timp real)
Serial USB: IO16, IO17 – UART (programare și depanare)

Observații de Proiectare

Punctele de test (TP-urile) au fost plasate strategic lângă marginile plăcii și în apropierea componentelor esențiale pentru depanare și testare rapidă.
Pentru diodele montate pe suprafață (SMD), dimensiunea pad-urilor a fost mărită față de valoarea implicită pentru a facilita o lipire mai sigură și eficientă.
Rutarea traseelor a fost realizată pe ambele straturi ale PCB-ului, iar planele de masă au fost introduse pentru o distribuție mai eficientă a curentului și reducerea interferențelor.
Traseele de alimentare, semnal și control au fost separate logic pentru o mai bună integritate electrică.
