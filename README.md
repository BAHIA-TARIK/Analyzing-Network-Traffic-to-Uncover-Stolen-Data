DESCRIPTION: Identifying Stolen Data through Network Traffic Examination 
Bahia Tarik

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

                              STEP 2 

 First we should have the archive download.7z, we wish to crack on our filesystem. 
![11](https://github.com/user-attachments/assets/d8e8a103-2133-4455-9cee-dacd3769fc72)
Handle compressed files with the LZMA algorithm: 
![12](https://github.com/user-attachments/assets/7a090e3a-4117-47ef-ad0d-e38193647b3d)
With the package installed, we can now find the location of 7z2john and copy its full path. 
![13](https://github.com/user-attachments/assets/c185923c-c270-4674-b727-26cbe9319d51)
Extract hash information from the 7z file download.7z 
![14](https://github.com/user-attachments/assets/aa630c4e-3ead-4128-8151-070773b26ccc)
Now we rerun the command and save the results to a file named lightweight7z.hash. 
![Capture d’écran 2024-07-11 154759](https://github.com/user-attachments/assets/a5ee5238-90da-42fe-b181-86d5473da953)
We delete the first characters . 
![15](https://github.com/user-attachments/assets/25d442a3-97a4-492e-9ed9-dd602a288ecf)
Try to break the hash contained in lightweight7z.hash using the word list rockyou.txt.gz with Hashcat 
![2](https://github.com/user-attachments/assets/46d56ad2-ddfb-4bff-abc8-47c02715cd81)
![3](https://github.com/user-attachments/assets/b77e1568-2fad-4dac-b80e-ff9f31621109)
Our password is cracked :hellokitty 

After extracting the zip, we find another password-protected PDF. Let's crack it using pdfcracker. 

 ![7](https://github.com/user-attachments/assets/a635248d-851d-4e1a-9d03-1b17944fffc3)

![8](https://github.com/user-attachments/assets/9917f34c-5da7-48f1-9be9-02b3231d7b09)
The password is : meow 

FLAG : 
AKASEC{PC4P_DNS_3xf1ltr4t10n_D0n3!!} 
![9](https://github.com/user-attachments/assets/b7984197-9105-43ae-bae5-9e227d6a1b20)
