# Info

Some patches I'm doing for Lego Soccer. I'm using a version of the game exe from which I removed the SafeDisc protection. MD5 Hashes:

Game.exe (Original file that is installed, with SafeDisc): 09FD678C2E4B7D8CEF89E4E0F7CFF738
Game.exe (SafeDisc removed): B1C77C044754F9785F69BC78BF5A71CC

# Remove game exe name DAT file check

The game checks if a file with the same name as the exe file (but with .DAT extension) exists, then it checks if the content of the files matches content in the game memory.

To remove this check, change:

.text:004010E9                 call    004012D0  
.text:004010EE                 test    al, al

into:

004010E9   EB 0B            JMP SHORT 004010F6  
004010EB   90               NOP  
004010EC   90               NOP    
004010ED   90               NOP  

# Remove Support/Soccer Mania_Code.exe launch check

The game does a check if it's able to launch Support/Soccer Mania_Code.exe. I'm not sure why this EXE is needed, maybe it checks for game crashes and launches a dialog?

To remove the launching and checking, change:

.text:00401142                 call    004013E0  

into:

00401141   EB 0F            JMP SHORT 00401152  
00401143   90               NOP  
00401144   90               NOP  
00401145   90               NOP  
00401146   90               NOP  


