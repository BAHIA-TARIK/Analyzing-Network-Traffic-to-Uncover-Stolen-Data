   STEP 1 

In this challenge, we are provided with a pcap file :packet .pcapng  

Initial analysis has identified some potentially suspicious requests.  

 ![c1](https://github.com/user-attachments/assets/ec4822d2-efa6-4eae-9b8c-2a41aa28eb5a)


After installing the file :packet .pcapng , now we will run the command : 

tshark -T fields -e dns.qry.name -r packet.pcapng | grep akasec.ma | uniq | sed 's/.akasec.ma//' | tr -d '\n' 

And the result will be as follows: 

 ![0](https://github.com/user-attachments/assets/408f3a4d-773d-4ede-ac14-75a0813edf91)

Decoding the data from hex, we find a 7z extension : 

 ![Capture d’écran 2024-07-10 183816](https://github.com/user-attachments/assets/c8674ff7-7374-489a-b717-c8c6947212b8)

We find that the 7z file is secured with a password. 
![Capture d’écran 2024-07-10 184347](https://github.com/user-attachments/assets/dbd4b0ae-cbab-4b30-8719-324f1b160e24)

Let's crack it !!! 
