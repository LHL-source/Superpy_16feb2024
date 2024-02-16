Datum:6 feb 2024 
In deze Read.md kun je lezen:
1)de gebruikers gids
2)de eisen aan het rapport: hierin zijn ook de 3 highlights te vinden

Gebruikers gids/User guide:
SuperPy -project beschrijving:
Een grote supermarktketen heeft  gevraagd  opdrachtregelprogramma’s te schrijven die hun voorraad kan bij houden: ze willen het applicatie Superpy noemen. Dit project is een demo en bevat uitsluitend fruit producten. In een latere ontwikkelingsfase fase zullen andere producten zoals jam, pinda kaas toe gevoegd worden.
De kernfunctionaliteit gaat over het bijhouden en genereren van rapporten over verschillende soorten gegevens zoals bijvoorbeeld:
1)Welke producten de supermarkt aanbiedt;
2)Hoeveel van elk type product heeft de supermarkt momenteel in voorraad;
3)Voor hoeveel elk product is gekocht en wat de houdbaarheidsdatum is;
4)Voor hoeveel elk product is verkocht en of het is verlopen, het feit dat dit het geval is.
Alle gegevens moeten worden opgeslagen in CSV-bestanden. Indien er een uitzondering is dan wordt dat in de uitleg aangegeven.
De gebruiker maakt gebruik van opdrachtsregels (in het engels: commands) die in de terminal display van VS code wordt geplaats. Hieronder volgen de opdrachtregels die gebruikt kunnen worden en de bijbehorende uitleg eventueel inclusief een test data set om een idee krijgen hoe het werkt:
Opdrachtregel_1: buy
Uitleg van opdrachtregel_1:In onderstaande opdrachtregel wordt een product die is aangekocht met de naam: orange, prijs 0.8 euro, expiratie_datum 2024-01-01 via de terminal ingevoerd. Dus de gebruiker kan de opdrachtregel kopiëren en vervolgens plakken in de terminal. De applicatie Superpy zal zorgen dat de gegevens van de opdrachtregel in het bestand met de naam bought.csv wordt geplaatst.
De opdrachtregel is de input: python main.py buy –product_nam orange --price 0.8 –expiration_date 2024-01-01
Resultaat als output: in het bestand: bought.csv  te zien:
id,product_name,buy_date,buy_price,expiration_date
1,orange,2023-11-25,0.8,2024-01-01
Uitleg over regel met id 1: 
1)	De id wordt automatisch gegenereerd
2)	Buy_date : is afhankelijk wat er in het bestand met naam internal_date.csv is gezet als datum. In dit geval : 2023-11-25
Opdrachtregel_2  inventory –now
Uitleg van opdrachtregel_2:De opdrachtregel: python main.py report inventory –now laat zien in een schema wat de voorraad op dit moment is. Dit moment wordt bepaald wat er in het bestand internal_date.csv als datum staat. In dit geval is het :2023-12-31. In dit rapport komen alleen producten waarvan de houdbaarheidsdatum (expiration-date) nog niet verstreken zijn. Voorwaarde is er is minimaal 1 rij in bestand bought.csv.
De opdrachtregel is de input: python main.py report inventory –now

Voor de test zijn er hier enige test data voor het bestand bought.csv. Indien er producten zijn die dezelfde gegevens hebben dan worden deze 2 bij elkaar opgeteld en via kolom “ count” om aan te geven hoeveel ervan zijn.
Resultaat: hieronder is een voorbeeld van output schema in de terminal (hieronder alleen de data in de terminal zie je belijning van de bijbehorende tabel)
Product Name count Buy Price Expiration Date
Orange             1          0.8            2024-01-01

Opdrachtregel_3: advance-time 2
Uitleg van opdrachtregel_3:Er wordt gebruik gemaakt van het bestand met naam:internal_date.csv daarin staat de datum:2024-01-01 met de opdachtregel: python main.py --advance-time 2 wordt de datum in het bestand python main.py --advance-time 2, 2 dagen verder gezet. De wordt dus 2024-01-03
De opdrachtregel is de input: python main.py --advance-time 2
Resultaat: de datum in het  bestand  met naam: 2024-01-01 wordt 2024-01-03
Opdrachtregel 4: report inventory –yesterday
Uitleg van opdrachtregel_4: Er wordt gebruik gemaakt van het bestand met naam:internal_date.csv daarin staat de datum:2023-12-06. Omdat er “ yesterday” staat wordt de datum in internal_date.csv bewijzigd naar (1 dag terug): 2023-12-05. In dit rapport komen alleen producten waarvan de houdbaarheidsdatum (expiration-date) nog niet verstreken zijn.
De test dataset voor bought.csv is:
bought.csv
id,product_name,buy_date,buy_price,expiration_date
1,appel,2023-11-25,0.4,2023-12-06
2,appel,2023-11-25,0.4,2023-12-06
3,appel,2023-11-25,0.4,2023-12-05
4,appel,2023-11-25,0.4,2023-12-07
5,banana,2023-11-25,0.5,2023-12-06
6,banana,2023-11-25,0.5,2023-12-05
7,banana,2023-11-25,0.5,2023-12-07

De opdrachtregel is de input: python main.py report inventory –yesterday

Resultaat in Rich(Rich is een module die zorgt er voor dat de tabel mooi kan worden opgemaakt
Bijvoorbeeld met speciale kleuren):

product name count buy price expiration_date
appel         2     0.4      2023-12-06  
appel         1     0.4      2023-12-07 
banana        1     0.5      2023-12-06
banana        1     0.5      2023-12-07
Opdrachtregel 5:Sell
Uitleg: doel van deze opdrachtregel is : indien een product wordt verkocht dan wordt dit vastgelegd in het stand sold.csv. Dit bestand heeft diverse kolommen te weten:
id,bought_id,sell_date,sell_price,product_name,buy_date,buy_price,expiration_date
Deze kolommen worden gevuld. Een opmerking hierbij is dat de waarde van kolom bought_id komt uit de gegevens van bestands bougt.csv en de sell_date komt van de datum uit het bestand .de internal_date. Tevens wordt in het bestand bought.csv waarvan het product is verkocht verwijderd
Hierbij heb je test data nodig om eerst klaar te wachten daarna kan je de opdrachtregel gebruiken om de resultaat te zien:
Test data:
bought.csv
id,bought_id,sell_date,sell_price,product_name,buy_date,buy_price,expiration_date

id,product_name,buy_date,buy_price,expiration_date
1,orange,2023-11-25,0.5,2023-12-5
2,appel,2023-11-23,0.4,2023-11-23 
3,appel,2023-11-25, 0.4,2023-12-6
4,banana,2023-11-24,0.6,2023-12-8
5,appel,2023-11-25,0.4,2023-12-9
6,orange,2023-11-25,0.5,2023-12-5
7,orange,2023-11-25,0.5,2023-12-5
8,appel,2023-11-23,0.4,2023-12-10


internal_date.csv:
internal_date
2023-12-07
Sold.csv
Geen rij

De opdrachtregel/input: python main.py sell --product_name appel --price 2

Resultaat/output: het bestand sold.csv zou zo behoren uit te zien, toegevoegd is regel 2 met id 2:
sold.csv
id,bought_id,sell_date,sell_price
1,5,2023-12-7,2.0
2,8,2023-12-7,2.0

Opdrachtregel 6: report inventory --now
Uitleg van opdracht_6 : De opdrachtregel: python main.py report inventory –now laat zien in een schema wat de voorraad op dit moment is. Dit moment wordt bepaald wat er in het bestand internal_date.csv als datum staat. In dit geval is het :2023-12-31. In dit rapport komen alleen producten waarvan de houdbaarheidsdatum (expiration-date) nog niet verstreken zijn. Voorwaarde is dat er 0 rij in bestand bought.csv. Ten gevolge hiervan krijg je alleen een leeg tabel te zien zonder rij.

De opdrachtregel is: python main.py report inventory --now 
Note: Er zijn GEEN rijen in bestand bought.csv
Resultaat/uitput, hier wordt de kolommen weer gegeven in de terminal display in csv code zie je een tabel met alleen kolom namen en 0 rijen:
Product Name count Buy_price Expiration_date

Opdrachtregel 7: report revenue --yesterday
Uitleg:doel van deze opdrachtregel: python main.py report revenue –yesterday, is de opbrengst (aantal verkochte producten x verkoopprijs) te berekenen van gisteren. De datum van gisteren is afhankelijk van de datum die staat in het bestand internal_date.csv. In de terminal display krijg he het resultaat te zien.
Voordat je de opdrachtregel invoert moet je eerst de test data klaar zetten van:
Internal_date.csv
internale_date 
2023-12-07
sold.csv :
id,bought_id,sell_date,sell_price,product_name,buy_date,buy_price,expiration_date
1,5,2023-12-6,2.0,appel,2023-11-25,0.4,2023-12-31
2,4,2023-12-6,2.0,appel,2023-11-25,0.4,2023-12-31
3,3,2023-12-6,1.5,banan,2023-11-25,0.4,2023-12-31
4,2,2023-12-5,2.0,appel,2023-11-25,0.4,2023-12-31
5,1,2023-12-4,1.5,banan,2023-11-25,0.4,2023-12-31
6,6,2023-12-9,2.0,appel,2023-11-25,0.4,2023-12-31
7,7,2023-12-10,1.0,orange,2023-11-25,0.4,2023-12-31

De opdrachtregel/input: python main.py report revenue --yesterday
Resultaat als output is ALLEEN de laatste regel de rest is uitwerking:
expected result:
id 1,2,3
id sell_price
1  2.2
2  2.2
3  1.5
totaal:5.9

Opdrachtregel_8: report revenue --today 
Uitleg van deze opdachtregel is: python main.py report revenue --today, is de opbrengst (aantal verkochte producten x verkoopprijs) te berekenen van vandaag. De datum van vandaag is afhankelijk van de datum die staat in het bestand internal_date.csv. In de terminal display krijg he het resultaat te zien.
Voordat je de opdrachtregel invoert moet je eerst de test data klaar zetten van:
internale_date.csv:
internale_date 
2023-12-07
sold.csv :
id,bought_id,sell_date,sell_price,product_name,buy_date,buy_price,expiration_date
1,5,2023-12-7,2.0,appel,2023-11-25,0.4,2023-12-31
2,4,2023-12-7,2.0,appel,2023-11-25,0.4,2023-12-31
3,3,2023-12-7,1.5,banan,2023-11-25,0.4,2023-12-31
4,2,2023-12-5,2.0,appel,2023-11-25,0.4,2023-12-31
5,1,2023-12-4,1.5,banan,2023-11-25,0.4,2023-12-31
6,6,2023-12-9,2.0,appel,2023-11-25,0.4,2023-12-31
7,7,2023-12-10,1.0,orange,2023-11-25,0.4,2023-12-31

De opdrachtregel: python main.py report revenue --today
Het resultaat/output, in de terminal display zie je alleen de laatste regel, totaal bedrag :
expected result:
id 1,2,3
id sell_price
1  2.0
2  2.0
3  1.5
totaal:5.5

Opdrachtregel_9: python report revenue --date 2023-12 --file_type_excel
Uitleg van deze opdachtregel: de gebruiker geeft via de opdrachtregel in de terminal en haalt op de totale omzet(verkoop) van de maand december 2023. Hier wordt totale omzet weg geschreven in een microsoft excel met de naam revenue_report.xlxs.
Voordat je de opdrachtregel invoert moet je eerst de test data klaar zetten van:
2)sold.csv :
id,bought_id,sell_date,sell_price,product_name,buy_date,buy_price,expiration_date
1,5,2023-12-7,2.0,appel,2023-11-25,0.4,2023-12-31
2,4,2023-11-7,2.0,appel,2023-11-25,0.4,2023-12-31
3,3,2023-12-1,1.5,banan,2023-11-25,0.4,2023-12-31
4,2,2023-12-30,0.5,appel,2023-11-25,0.4,2023-12-31
5,1,2023-10-4,1.5,banan,2023-11-25,0.4,2023-12-31
6,6,2023-9-9,2.0,appel,2023-11-25,0.4,2023-12-31
7,7,2023-11-10,1.0,orange,2023-11-25,0.4,2023-12-31


De opdrachtregel_9: python main.py report revenue --date 2023-12 --file_type_excel
Resultaat /output:
expected result:
output:Revenue from December 2023: 4.0
Teven ook te vinden in bestand met de naam: revenue_report.xlxs. Deze is te vinden in de file manager en te openen met Microsoft Excel.

De opdrachtregel_10:python main.py report profit –today
Uitleg: De datum van “vandaag” is afhankelijk van wat in de internal_data.csv staat. Hier wordt de winst van “ vandaag” uitgerekend. De definitie van winst is totale verkoop minus de totale kosten.
Voordat je de opdrachtregel invoert moet je eerst de test data klaar zetten van:
Internal_date.csv:
Internal_date
2023-12-07
sold.csv
id,bought_id,sell_date,sell_price,product_name,buy_date,buy_price,expiration_date
1,5,2023-12-7,2.0,appel,2023-11-25,0.4,2023-12-31
2,4,2023-12-7,2.0,appel,2023-11-25,0.4,2023-12-31
3,3,2023-12-6,1.5,banan,2023-11-25,0.4,2023-12-31
4,2,2023-12-5,2.0,appel,2023-11-25,0.4,2023-12-31
5,1,2023-12-10,1.5,banan,2023-11-25,0.4,2023-12-31
6,6,2023-12-9,2.0,appel,2023-11-25,0.4,2023-12-31
7,7,2023-12-7,1.0,orange,2023-11-25,0.3,2023-12-31

De opdrachtregel_10: python main.py report profit –today

Resultaat: profit of today=3,9
 xx xx

Eisen voor het rapport:
2.1Voeg een kort rapport van 300 woorden toe waarin drie technische elementen van uw implementatie worden belicht die u opmerkelijk vindt.
2.2 Leg uit welk probleem ze oplossen en waarom je ervoor hebt gekozen ze op deze manier te im plementeren
2.3	Neem dit op in uw repository als een report.md-bestand
Ad 2.1 en 2.2:Uitwerking van :2.1 en 2.2: Aangezien deze 2 eisen gerelateerd zijn aan elkaar wordt hieronder 3 tal technische elementen belicht die opmerkelijk zijn. Tevens wordt ook uitgelegd (ad 2.2) wat voor soort probleem wordt opgelost  en de rede van de keuze van de oplossing.

Technische_element_1:functions: string_to_datetime() en functie: datetime_to_string()
Door het geheel van de applicatie wordt regelmatig de datum geconverteerd van data type string naar data type datetime object en andersom. Vanwege de veelvuldigheid van dit gebruik zijn er twee tal functies gemaakt om dit op te lossen te weten:
1 functie: string_to_datetime()
2 functie: datetime_to_string()
De rede waarom voor de keuze van deze oplossing is omdat de beide functies herbruikbaar is en makkelijker is te onderhouden.

Technische_element_2:de id van functie: add_buy_product() van de opdrachtregel buy 
Voor de opdrachtregel : python main.py buy –product_nam orange --price 0.8 –expiration_date 2024-01-01, wordt in de bought.csv de kolom “ id”  aangehouden. De kolom “id” wordt automatisch door de applicatie Superpy opgehoogd indien er een nieuw product wordt toegevoegd. Om dit op te lossen is gekozen voor de volgende oplossing: voor elke iteratie van de rij in de bought.csv wordt een variabel bijgehouden b.v. id_bijhouden. Bij elke iteratie wordt de de variabel id_bijhouden opgehoogd met 1. Indien er een NIEUW product wordt toegevoegd dan wordt de variabel id_eenOphogen gebruikt daarbij wordt bewerkt dat id_bijhouden met 1 wordt opgehoogd. De waarde van id_eenOphogen is dan de waarde van de kolom ‘id’ van de nieuw toegevoegde rij. De naam van de variabelen die hierboven zijn genoemd zijn fictie gekozen om de functionaliteit te laten begrijpen voor de lezer. In de functie: add_buy_product() zie je de beschreven constructie terug.

Technische_element_3:door inzicht in fuctionaliteit van het proces kan je programmeren vergemakkelijken
In de opdracht van het project werd voor de bought.csv en sold.csv als voorstel gedaan de volgende kolommen:
id,product_name,buy_date,buy_price,expiration_date
Sold.csv, kolommen:
id,bought_id,sell_date,sell_price
Aangezien de opdrachtregel van b.v.  rapport: python main.py report profit --today  in de bought.csv van het verkochte product de rij wordt verwijderd is het handig de kolommen van sold.csv UIT TE BREIDEN met de volgende kolommen van bought.csv: product_name,buy_date,buy_price,expiration_date
Ten gevolge hiervan zien  de namen van de “ nieuwe”  kolommen van sold.csv als volgt uit:
id,bought_id,sell_date,sell_price,product_name,buy_date,buy_price,expiration_date
Door de ‘nieuwe’ kolommen van sold.csv aan te houden worden de bijbehorende data ook zodanig geplaatst. Ten gevolge hiervan is het relatief makkelijk om b.v. voor  de command: python main.py report profit –today, een functie te maken met de naam: report_profit_today(), om de winst(‘profit’) te berekenen.
Ad2.3 In de report.md zijn de 3 Technische_elementen opgenomen conform de opdracht.
Xx einde alle Eisen aan report xx 6-2-2024























