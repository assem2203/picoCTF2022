# picoCTF2022
[assem] picoCTF 2022 Writeup

This is the writeup of Team(assem) competition picoCTF 2022.


[Forensics]


 #1 Enhance!
Download this image file and find the flag.
flag hint : (None)
₩₩₩
 score: 100
 flag : picoCTF{3nh4nc3d_56e87c96}
 solve : $ identify -verbose drawing.flag.svg
₩₩₩

 #3 Lookey here
Attackers have hidden information in a very large mass of data in the past, maybe they are still doing it. Download thr data here.
flag hint : Download the file and search for the flag based on the known prefix.
 score: 100
 flag : picoCTF{gr3p_15_@w3s0m3_0abe82b2}
 solve : $ strings anthem.flag.txt | grep -i "pico"


 #4 Packets Primer
Download the packet capture file and use packet analysis software to find the flag.
flag hint : Wireshark, if you can install and use it, is probably the most beginner friendly packet analysis software a product.
 score: 100
 flag : picoCTF{p4ck37_5h4rk_309456e4}
 solve : [Follow] -> [TCP Stream]


 #5 Redaction gone wrong
Now you DON’T see me. This report has some critical data in it, some of which have been redacted correctly, while some were not, Can you find an important key that was not redacted properly?
flag hint : How can you be sure of the redaction?
 score: 100
 flag : picoCTF{C4n_Y0u_S33_m3_fully}
 solve : Open file in web browser. Pasted note after drag file.


 #6 Sleuthkit Intro
DOwnload the disk image and use mmls on it to find the size of the Linux partition. Connect to the remote checker service to check your answer and get the flag. Note: if you are using the webshell, download and extract the disk image into /tmp not your home directory.
flag hint : (None)
 score: 100
 flag : picoCTF{mm15_f7w!}
 solve : $ mmls disk.img
  $ nc saturn.picoctf.net 52279
  $ 202752


 #7 Sleuthkit Apprentice
Download this disk image and find the flag. Note : if you are using the webshell, download and extract the disk image into /tmp not your home directory.
flag hint : (None)
 score: 200
 flag : picoCTF{by73_5urf3r_11b94644}
 solve : Open FTK Imager in Windows OS. [Partition 3] -> [NONAME] -> [root] -> [root] -> [my_folder] -> [flag.uni.txt]


 #9 Operation Oni
Download this disk image, find the key and log into the remote machine. Note: if you are using the webshell, download and extract this disk image into /tmp not your home directory. Remote machine : ssh –i key_file –p 57850 ctf-player@saturn.picoctf.net
flag hint : (None)
 score: 300
 flag : picoCTF{k3y_5l3u7h_d6570e30}
 solve : Open FTK Imager in Windows OS. [Partition 2] -> [NONAME] -> [root] -> [root] -> [.ssh], you find private key and public key. And login ssh after extraction files.
  $ ssh -i id_ed25519 -p 57850 ctf-player@saturn.picoctf.net
  $ ls -al
  $ cat flag.txt


 #11 Operation Orchid
Download this disk image and find the flag. Note: if you are using the webshell, download and extract the disk image into /tmp not your home directory.
flag hint : (None)
 score: 400
 flag : picoCTF{h4un71ng_p457_186cf0da}
 solve : Open FTK Imager in Windows OS. [Partition 3] -> [NONAME] -> [root] -> [root], you find two files. ".ash_history" is command history file and "flag.txt.enc" is encrypted file. You decryption file after read history with extraction files. 
  $ openssl aes256 -d -salt -in flag.txt.enc -out flag.txt -k unbreakablepassword1234567
   $ cat flag.txt


[Reverse Engineering]


 #1 file-run1
A program has been provided to you, what happens if you try to run it on the command line?
flag hint : To run the program at all, you must make it executable (i.e $ chmod +x run), To running it by adding a ‘.’ in front of the path to the file(i.e $ ./run)
 score: 100
 flag : picoCTF{U51N6_Y0Ur_F1r57_F113_2a4dec6a}
 solve : $ chmod +x run
  $ ./run


 #2 file-run2
Another program. but this time, it seems to want some input. What happens if you try to run it on the command line with input “Hello!”?
flag hint : Try running it and add the phrase “Hello!” with a space in front (i.e “,/run Hello!”)
 score: 100
 flag : picoCTF{F1r57_4rgum3n7_0097836e}
 solve : $ chmod +x run.1
  $ ./run.1 Hello!


 #3 GDB Test Drive
Can you get the flag? Here’s the test drive instructions : $ chmod +x gdbme, $ gdb gdbme, (gdb) layout asm, (gdb) break *(main+99), (gdb) run, (gdb) jump *(main+104)
flag hint : (None)
 score: 100
 flag : picoCTF{d3bugg3r_dr1v3_3eab6731}
 solve : $ chmod +x gdbme
  $ gdb gdbme
  (gdb) layout asm
  (gdb) break *(main+99)
  (gdb) run
  (gdb) jump *(main+104)


 #4 patchme.py
Can you get the flag? Run this Pyton program in the same directory as this encrypted flag.
flag hint : (None)
 score: 100
 flag : picoCTF{p47ch1ng_l1f3_h4ck_68aa6913}
 solve : You open python file and check "user_pw" somthing string is password. Just input String.
  $ python patchme.flag.py
  ak98-=90adfjhgj321sleuth9000


 #5 Safe Opener
Can you open this safe? I forgot the key to my safe but this program is supposed to help me with retrieving the lost key. Can you help me unlock my safe? Put the password you recover into the picoCTF flag format like: pickCTF{password}
flag hint : (None)
 score: 100
 flag : picoCTF{pl3as3_l3t_m3_1nt0_th3_saf3}
 solve : You open python file and check "encodedkey" somthing string is password. But this strings is Base64 encoding and you can decoding string.
       $ echo "cGwzYXMzX2wzdF9tM18xbnQwX3RoM19zYWYz" |base64 -d


 #6 unpackme.py
Can you get the flag? Reverse engineer this Python program.
flag hint : (None)
 score: 100
 flag : picoCTF{175_chr157m45_45a1a353}
 solve : You open python file and check "plain.decode()", this is flag. and you can print planin.decode().


 #7 bloat.py
Can you get the flag? Run this Python program in the same directory as this encrypted flag.
flag hint : (None)
 score: 200
 flag : picoCTF{d30bfu5c4710n_f7w_1763a697}
 solve : You open python file and check "a" and you find value in list. "arg133" is password.
  $ python bloat.flag.py
  happychance


 #8 Fresh Java
Can you get the flag? Reverse engineer this Java program.
flag hint : Use a decompiler for Java!
 score: 200
 flag : picoCTF{700l1ng_r3qu1r3d_84e23997}
 solve : This is ".class" file. I need decompiler program. Install decompiler program and you easy find flag.







[Cryptography]


 #1 basic-mod1
We found this weird message being passed around on the servers, we think we have a working decrpytion scheme. Download the message here. Take each number mod 37 and map it to the following character set: 0-25 is the alphabet(uppercase), 26-35 are the decimal digits, and 36 is an underscore. Wrap you decrypted message in the picoCTF flag format(i.e picoCTF{decrypted_message})
flag hint : Do you know what mod 37 means? mod 37 means modulo 37. It gives theremainder of a number after being divded by 37.
 score: 100
 flag : picoCTF{R0UND_N_R0UND_CE58A3A0}
 solve : Change message with using  mod 37.


 #3 credstuff
We found a leak of a blackmarket website’s login credentials. Can you find the password of the user cultiris and successfully decrypt it? Download the leak here. The firust user in username.txt corresponds to the first password in passwords.txt The second user corresponds to the second password, and so on.
flag hint : Maybe other passwords will have hints about the leak?
 score: 100
 flag : picoCTF{C7r1F_54V35_71M3}
 solve : Open usernames.txt. Find "cultirls" and remember lines. And open password.txt go to remember lines. Final copy line strings and decrypt rot13.


 #4 morse-code
Mores code is well known. Can you decrypt this? Download the file here. Wrap your answer with picoCTF{}, put underscores in place of pauses, and use all lowercase.
Audacity is really good program to analyze morse code audio.
 score: 100
 flag : picoCTF{WH47_H47H_90D_W20U9H7}
 solve : This file is audio file. Start audio you hear morse-code. And translate morse-code.



















[Web Exploitation]


 #1 Includes
Can you get the flag? Go to this website and see what you can discover.
flag hint : Is there more code than what the inspector initially show?
 score: 100
 flag : picoCTF{1nclu51v17y_1of2_f7w_2of2_5a94a145}
 solve : Open website. Push F12 and you find flag in "style.css", "script.js".


 #2 Inspect HTML
Can you get the flag? Go to this website and see what you can discover.
flag hint : What is the web inspector in web browsers?
 score: 100
 flag : picoCTF{1n5p3t0r_0f_h7ml_b101a689}
 solve : Open website. Push F12 and you find flag in "index".


 #3 Local Authority
Can you get the flag? Go to this website and see what you can discover.
flag hint : How is the password checked on this website?
 score: 100
 flag : picoCTF{j5_15_7r4n5p4r3n7_b964a657}
 solve : Open website. Before Push F12 you input something stringy in "Username", "Password" and you see "secure.js". Check file and login.


 #4 Search source
The developer of this website mistakenly left an important artifact in the website source, can you find it?
flag hint : How could you mirror the website on your local machine so you could use more powerful tools for searching?
 score: 100
 flag : picoCTF{1nsp3ti0n_0f_w3bpag3s_74784981}
 solve : Open website. Push F12 and move [css] -> [style.css] can find flag.



 #5 Forbidden Paths
Can you get the flag? Here’s the website. We know that the website files live in /usr/share/nginx/html/ and the flag is at /flag.txt but the website is filtering absolute file paths. Can you get past the filter to read the flag?
flag hint : (None)
 score: 200
 flag : picoCTF{7h3_p47h_70_5ucc355_32e3a320}
 solve : Open website. Input "divine-comedy.txt" and click "Read" button. See somthing text. Read "Fiddler" and change parameter "filename=divine-comedy.txt&read=" -> "filename=../../../../../../../../../../../flag.txt&read=/usr/share/nginx/html". Response and find flag.



 #6 Power Cookie
Can you get the flag? Go to this website and see what you can discover.
flag hint : Do you know how to modify cookies?
 score: 200
 flag : picoCTF{gr4d3_A_c00k13_87608ba8}
 solve : Open website. Click "Continue as guest". Push F12 you can see "isAdmin=0" in "guest.js". Change Value "0" -> "1". And find flag in "check.php".



 #7 Roboto Sans
The flag is somewhere on this web application not necessarily on the website, Find it.
flag hint : (None)
 score: 200
 flag : picoCTF{Who_D03sN7_L1k5_90B0T5_87ccf72a}
 solve : Open website and move "/robots.txt". And decoding page text delete one same strings(anMvbXlmaW). Result is "js/myfile.txt" and move it.



 #8 Secrets
We have several page hidden. Can you find the one with the flag?
flag hint : folders folders folders
 score: 200
 flag : picoCTF{succ3ss_@h3n1c@10n_08de81e4}
 solve : Open website you see three tabs. Push F12. You can see "secret/assets" in each tabs and show 403 error when go "/secret/assets". But you show other page when go to "/secret". You can see [secret] -> [hidden] when Push F12 and you show other page when go "/secret/hidden". One more you push F12. You can see "superhidden". Go to "/secret/hidden/superhidden" you find flag when push F12.


 #9 SQL Direct
Connect to this PostgreSQL server and find the flag!
flag hint : (None)
 score: 200
 flag : picoCTF{L3arN_S0m3_5qL_t0d4Y_472538a0}
 solve : # \dt
  # \d flags
  # select address from puvlic.flags


 #10 SQLiLite
Can you login to this website?
flag hint : admin is the user you want to login as.
 score: 300
 flag : picoCTF{L00k5_l1k3_y0u_solv3d_it_147ec287}
 solve : Open website. Using SQL injection. Username : admin, Password : ' OR '1' = '1. And find flag when push F12.

