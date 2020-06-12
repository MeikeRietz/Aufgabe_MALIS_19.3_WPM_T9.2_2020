# Python und Shell - Bearbeitung der Aufgaben aus dem Wahlpflichtmodul Data Science/IT Praxis

In diesem Repositorium sind die Bearbeitungen der Aufgabe T9.2_2020 des Wahlpflichtmoduls Data Science/IT Praxis zu finden. Da es sich bei Aufgabe 1 um das Erstellen von Python-Scripten handelt, führt die Lösung zu einem Jupyter Notebook. Dieses beinhaltet ausführliche Erläuterungen der Vorgehensweise. Die Lösung der Aufgabe 2 ist hingegen hier vollständig zu entnehmen.

### Inhaltsverzeichnis       
**1.** [Aufgabe 1: Python](#Python)     
**2.** [Aufgabe 2: Shell](#Shell)     
       2.1 [Aufgabenstellung](#Aufgabenstellung)          
       2.2 [Vollständiger Weg mit Git Bash](#Git)      
       2.3 [Script](#Script)           
**3.** [Quellen](#Quellen)    

## Aufgabe 1: Python <a name="Python" /></a>

Die Bearbeitung des Datensets "Checkouts" ist hier zu finden: https://github.com/MeikeRietz/Aufgabe_MALIS_19.3_WPM_T9.2_2020/blob/master/Jupyter%20Notebook%20zu%20Checkouts.ipynb  

Die Bearbeitung des Datensets "Inventory" ist hier zu finden:
https://github.com/MeikeRietz/Aufgabe_MALIS_19.3_WPM_T9.2_2020/blob/master/Jupyter%20Notebook%20zu%20Inventory.ipynb     

## Aufgabe 2: Shell <a name="Shell" /></a>       

### 2.1 Aufgabenstellung <a name="Aufgabenstellung" /></a>     

Aufgabenstellung 2 bestand daraus, aus einer bereitgestellten sogenannten "dirty" .tsv-Datei eine bereinigte neue .tsv-Datei zu erstellen. Ziel dieser neuen Datei sollte eine tabellarische Ordnung in die Spalten ISSNs und Veröffentlichungsjahren darstellen. Als Ergebnis zählt ein selbst erstelltes Shell-Script.

Nachfolgenden wird erst der vollständige Verlauf aus Git Bash dargestellt. Im Anschluss folgt das fertige, zusammengeführte Script.     

### 2.2 Vollständiger Weg mit Git Bash <a name="Git" /></a> 

Die Ursprungs-Datei "2020-05-23-Article_list_dirty.tsv" wurde nach dem Download auf dem Desktop abgelegt. Deswegen wird als erster Schritt - nach dem Starten von Git Bash - über den Befehl _cd desktop_ auf den Desktop des PCs zugegriffen.      

meike@DESKTOP-FCP35GO MINGW64 ~                      
**$ cd desktop**   

Mit dem Befehl _less 2020-05-23-Article_list_dirty.tsv_ wird mir der Inhalt der Datei in einer tabellarischen Ordnung angezeigt. Dadurch erhalte ich Einblick in die Definition der einzelnen Spalten: Creator Issue Volume Journal ISSN ID Citation Title Place Label Language Publisher und Date. Hieraus kann ich mir durch zählen die gewünschten Spalten ermitteln (5 und 12) und den Pager mit der Eingabe der Taste _Q_ wieder schließen.     

meike@DESKTOP-FCP35GO MINGW64 ~/desktop (master)     
**$ less 2020-05-23-Article_list_dirty.tsv**     

Als nächstes möchte ich die Spalten ISSN und Date aus der Datei extrahieren und in einer neuen Datei ablegen. Dafür wähle ich den Befehl _cut -f 5,12_ in dem cut für das Herausschneiden steht, _-f_ für das "field" bzw. die Spalten und _5,12_ die ermittelten Spalten ISSN und Date definiert. Mit dem Befehl _> Zwischenergebnis1.tsv_ gebe ich das Ergebnis in einer neuen Datei aus.
     
meike@DESKTOP-FCP35GO MINGW64 ~/desktop (master)                                 
**$ cat 2020-05-23-Article_list_dirty.tsv | cut -f 5,12 > Zwischenergebnis1.tsv**   

Nun kann ich mir das erste Zwischenergebnis anzeigen lassen und stelle fest, dass das Extrahieren funktioniert hat, allerdings die ISSN in unterschiedlich dargestellt wird und die Datei leere Zeilen oder nicht gewünschte Zeilen enthält, die ich bereinigen möchte.
       
meike@DESKTOP-FCP35GO MINGW64 ~/desktop (master)                                                                             
**$ cat Zwischenergebnis1.tsv**     
     
ISSN    Date                                                                                                                 
ISSN: 0004-9522 1995                                                                                                         
0013-8266       1995                                                                                                         
0262-7280       1995                                                                                                    
0022-4529       1995                                                                                                   
0022-4529       1995                                                                                                               
0022-1953       1996                                                                                                    
1056-8190       1995                                                                                                    
0030-8684       1995                                                                                                    
0129-797X       1995                                                                                                    
0018-2648       1996                                                                                                    
ISSN:0265-6914  1996                                                                                                    
0265-6914       1996                                                                                                    
ISSN:0008-4107  1995     
0950-9224       1995     
0707-5332       1995     
0019-7211       1996     
0022-2801       1995     
0022-2801       1995     
0018-2613       1996     
0968-7475       1995     
0003-813X       1996     
0013-2683       1995     
6       eng     
6       eng     
27      eng     
39      eng     
29      eng     
29      eng     
29      eng     
44      eng     
0022-2801       1996     
0022-2801       1996     
0707-5332       1996     
issn: 0707-5332 1996     
0707-5332       1996     
0707-5332       1996     
0707-5332       1996     
Issn:  0029-3652        1995     
0305-8034       1996     
0022-5037       1996     
0315-7997       1996     
0095-1390       1995     
0095-1390       1995     
0095-1390       1995     
0095-1390       1995     
0095-1390       1995     
0009-4455       1995     
0018-2753       1996     
[…]     

Als erstes möchte ich die Zeilen entfernen, die die Silbe "eng" enthalten, da sie für das Ergebnis irrelevant sind. Dazu arbeite ich mit dem Befehl _grep_ und geben an, dass aus der Datei alle Zeilen (_-v_) entfernt werden sollen, die die Buchstabenfolge "eng" enthalten. Das Ergebnis soll in einer neuen Datei ausgegeben werden. (_> Zwischenergebnis2.tsv_)     

meike@DESKTOP-FCP35GO MINGW64 ~/desktop (master)     
**$ cat Zwischenergebnis1.tsv | grep -v eng > Zwischenergebnis2.tsv**     
     
Nun widme ich mich den Zeilen, in denen der ISSN die Worte "ISSN:", "Issn:" und "issn:" vorausgehen. Diese möchte ich aus meiner Ergebnisdatei herausnehmen, wofür ich den Befehl _sed_ benutze. Dieser ersetzt in meinem Script _/ISSN:/_, _/Issn:/_ und _/issn:/_ durch eine Leerstelle _//_. Das Ergebnis soll in einer neuen Datei ausgegeben werden. (_> Zwischenergebnis3.tsv_)     

meike@DESKTOP-FCP35GO MINGW64 ~/desktop (master)                                                                             
**$ sed 's/ISSN:/ /g;s/Issn:/ /g;s/issn:/ /g' Zwischenergebnis2.tsv > Zwischenergebnis3.tsv**     

Wenn ich mir nun die Datei anschaue, stelle ich fest, dass zwar die Wörter fehlen, aber dort wo sie waren Leerstellen entstanden sind. Hierfür nutze ich ebenfalls _sed_, um mich der Leerstellen zu entledigen und alles linksbündig anzuordnen. Das Ergebnis soll in einer neuen Datei ausgegeben werden. (_> Zwischenergebnis4.tsv_)     

meike@DESKTOP-FCP35GO MINGW64 ~/desktop (master)                                                                            
**$ sed 's/^[ \t]*//' Zwischenergebnis3.tsv > Zwischenergebnis4.tsv**    

Was nun übrig bleibt, sind Zeilen ohne Inhalt und Dopplung. Diese kann ich entfernen, indem ich meine Werte sortiere. Durch den Befehl _sort -u_ werden doppelte Zeilen entfernt. Dies bezieht sich nicht nur auf die leeren Zeilen, sondern auch doppelte ISSNs. Das Ergebnis soll in einer neuen Datei ausgegeben werden. (_> Zwischenergebnis5.tsv_)     

meike@DESKTOP-FCP35GO MINGW64 ~/desktop (master)                                                                             
**$ sort -u Zwischenergebnis4.tsv > Zwischenergebnis5.tsv**     
     
Zwar sind die doppelten Zeilen nun entfernt, jedoch möchte ich die Überschriften an den Beginn der Liste setzen und die ISNNs numerisch sortieren. Dafür nutze ich _sort -n_ und gebe das Ergebnis in der Zieldatei _> 2020-05-23-DATES_and_ISSNs.tsv_ aus.

meike@DESKTOP-FCP35GO MINGW64 ~/desktop (master)                                                                             
**$ sort -n Zwischenergebnis5.tsv > 2020-05-23-DATES_and_ISSNs.tsv**           
     
Ein letzter Blick in die Datei, mit dem Befehl _cat_ ausgeführt, zeigt mir, dass die Liste nun sauber die ISSNs in reiner numerischer Form angibt und keine störenden Zeilen und Dopplungen mehr vorhanden sind.       
     
meike@DESKTOP-FCP35GO MINGW64 ~/desktop (master)                                                                             
**$ cat 2020-05-23-DATES_and_ISSNs.tsv**     
     
ISSN    Date                                                                                                                 
0003-598X       1996                                                                                                          
0003-813X       1996                                                                                                         
0004-9522       1995                                                                                                         
0008-4107       1995     
0008-4107       1996     
0009-4455       1995     
0010-4175       1996     
0011-3212       1996     
0012-8449       1996     
0013-2683       1995     
0013-8266       1995     
0013-8266       1996     
0018-246X       1996     
0018-2613       1996     
0018-2648       1996     
0018-2753       1996     
0019-7211       1996     
0020-8590       1996     
0021-8537       1996     
0021-9118       1996     
0022-0094       1996     
0022-1953       1996     
0022-2801       1995     
0022-2801       1996     
0022-4529       1995     
0022-4529       1996     
0022-4634       1996     
0022-5037       1996     
0023-656X       1996     
0029-3652       1995     
0030-8684       1995     
0037-6779       1996     
0037-6795       1996     
0048-8003       1995     
0079-4848       1996     
0095-1390       1995     
0095-1390       1996     
0129-797X       1995     
0142-7962       1996     
0143-781X       1996     
0262-7280       1995     
0265-6914       1996     
0265-7325       1996     
0305-8034       1996     
0313-6221       1996     
0315-7997       1996     
0707-5332       1995     
0707-5332       1996     
0950-9224       1995     
0968-7475       1995     
0968-7475       1996     
1056-8190       1995     
1069-5834       1996     
1078-6279       1996     
1331-3134       1994     
1350-7486       1996     
1361-2343       1994     
1361-9462       1994     
 
      
### 2.2 Script <a name="Script" /></a>

Das Script enhält die oben genannten Schritte. Zusätzlich wurde der Befehl _rm_ hinzugefügt, mit dem ich die verwendeten Zwischendateien wieder lösche und so meinen Desktop bereinige.     

     
#!/bin/bash     
#Bereinigung der Dirty-Datei     

cat 2020-05-23-Article_list_dirty.tsv | cut -f 5,12 > Zwischenergebnis1.tsv                                                  
cat Zwischenergebnis1.tsv | grep -v eng > Zwischenergebnis2.tsv                                                             
sed 's/ISSN:/ /g;s/Issn:/ /g;s/issn:/ /g' Zwischenergebnis2.tsv > Zwischenergebnis3.tsv                                      
sed 's/^[ \t]*//' Zwischenergebnis3.tsv > Zwischenergebnis4.tsv     
sort -u Zwischenergebnis4.tsv > Zwischenergebnis5.tsv                                                                        
sort -n Zwischenergebnis5.tsv > 2020-05-23-DATES_and_ISSNs.tsv                                                              
rm Zwischenergebnis1.tsv Zwischenergebnis2.tsv Zwischenergebnis3.tsv Zwischenergebnis4.tsv Zwischenergebnis5.tsv
cat 2020-05-23-DATES_and_ISSNs.tsv      

## Quellen: <a name="Quellen" /></a>
Deutsche Nationalbibliothek, _Metadienste_     URL:https://www.dnb.de/DE/Professionell/Metadatendienste/Metadaten/Nationalbibliografie/nationalbibliografie_node.html, abgerufen am 06.05.2020  

https://wiki.ubuntuusers.de/cut/     
https://wiki.ubuntuusers.de/sed/     
https://wiki.ubuntuusers.de/grep/     
https://wiki.ubuntuusers.de/sort/

