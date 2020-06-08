# Aufgabe_MALIS_19.3_WPM_T9.2_2020

meike@DESKTOP-FCP35GO MINGW64 ~                                                                                         
$ cd desktop    
     
meike@DESKTOP-FCP35GO MINGW64 ~/desktop (master)                                                                        
$ less 2020-05-23-Article_list_dirty.tsv     
     
meike@DESKTOP-FCP35GO MINGW64 ~/desktop (master)                                                                                 
$ cat 2020-05-23-Article_list_dirty.tsv | cut -f 5,12 > Zwischenergebnis1.tsv          
       
meike@DESKTOP-FCP35GO MINGW64 ~/desktop (master)                                                                             
$ cat Zwischenergebnis1.tsv     
     
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
     
meike@DESKTOP-FCP35GO MINGW64 ~/desktop (master)     
$ cat Zwischenergebnis1.tsv | grep -v eng > Zwischenergebnis2.tsv
     
meike@DESKTOP-FCP35GO MINGW64 ~/desktop (master)                                                                             
$ sed 's/ISSN:/ /g;s/Issn:/ /g;s/issn:/ /g' Zwischenergebnis2.tsv > Zwischenergebnis3.tsv     
     
meike@DESKTOP-FCP35GO MINGW64 ~/desktop (master)                                                                            
$ sed 's/^[ \t]*//' Zwischenergebnis3.tsv > Zwischenergebnis4.tsv     
     
meike@DESKTOP-FCP35GO MINGW64 ~/desktop (master)                                                                             
$ sort -u Zwischenergebnis4.tsv > Zwischenergebnis5.tsv     
     
meike@DESKTOP-FCP35GO MINGW64 ~/desktop (master)                                                                             
$ sort -n Zwischenergebnis5.tsv > 2020-05-23-Article_list_dirty.tsv     
     
meike@DESKTOP-FCP35GO MINGW64 ~/desktop (master)     
$ mv 2020-05-23-Article_list_dirty.tsv 2020-05-23-DATES_and_ISSNs.tsv     
     
meike@DESKTOP-FCP35GO MINGW64 ~/desktop (master)                                                                             
$ cat 2020-05-23-DATES_and_ISSNs.tsv     
     
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
     
     
