CEH v12 Practical / CEH v12 Guia de estudio para examen practico

La siuiente es una guia de las herrramientas y comandos que se utilizaron en cada uno de los modulos de la certificación CEH v12, se tomo en cuenta el material de Ecourseware (Especialmente la sección de laboratios), para fines practicos se mencionaran las herramientas que se consideren más utiles, ya que bajo mi perspectiva la certificación utiliza multiples herramientas para con un mismo fin, es posible que se mencionen más solo se abordará una

# Introduction to Ethical Hacking - 01 
Este modulo esencialemente es teorico y no sé abordan herrramientas.

# Footprinting and Reconnaissance - 02 

## 1- Perform Footprinting Through Search Engines 

### 1.1- Gather Information using Advanced Google Hacking Techniques
Lista de todos los comandos : https://ahrefs.com/blog/google-advanced-search-operators/

Tabla de comandos funcionales

| Operador | Descripción | Ejemplo |
| :---: |     :---:      | :---:|
|  `“ ”` | Search for results that mention a word or phrase | 	“steve jobs”  |
| `OR`	 | Search for results related to X or Y. |	jobs OR gates |
| `\|` |	Same as OR: |	jobs `\|` gates |
| `AND` |	Search for results related to X and Y. | jobs AND gates | 
| `-` |	Search for results that don’t mention a word or phrase. | jobs -apple |
| `*` |	Wildcard matching any word or phrase. | steve * apple |  
| `( )` |	Group multiple searches. | 	(ipad OR iphone) apple |
| `define:` |	Search for the definition of a word or phrase.  | define:entrepreneur | 
| `cache:` |	Find the most recent cache of a webpage. | cache:apple.com |
| `filetype:` |	Search for particular types of files (e.g., PDF). | apple filetype:pdf |
| `ext:` | 	Same as filetype:	apple | ext:pdf |
| `site:` |	Search for results from a particular website. | site:apple.com |
| `related:` |	Search for sites related to a given domain. | related:apple.com |
| `intitle:` |	Search for pages with a particular word in the title tag. | intitle:apple |
| `allintitle:` |	Search for pages with multiple words in the title tag. | allintitle:apple iphone |
| `inurl:` |	Search for pages with a particular word in the URL. | inurl:apple |
| `allinurl:` |	Search for pages with multiple words in the URL. | allinurl:apple iphone |
| `intext:` |	Search for pages with a particular word in their content. | intext:apple iphone |
| `allintext:` |	Search for pages with multiple words in their content. | allintext:apple iphone |
| `weather:` |	Search for the weather in a location. | weather:san francisco |
| `stocks:` |	Search for stock information for a ticker. | stocks:aapl |
| `map:` |	Force Google to show map results. | map:silicon valley |
| `movie:` |	Search for information about a movie. | movie:steve jobs |
| `in` |	Convert one unit to another. | $329 in GBP |
| `source:` |	Search for results from a particular source in Google News. | apple source:the_verge |
| `before:` |	Search for results from before a particular date. | apple before:2007-06-29 |
| `after:` |	Search for results from after a particular date. | apple after:2007-06-29 |

Lista de ejemplos : https://www.exploit-db.com/google-hacking-database

| Ejemplo | Descripción | 
| :---: |     :---:     |
| inurl:page.php?id= site:.pk | SQL Injection  |
| inurl:"/wp-includes/user.php" -site:wordpress.org -site:github.com -site:fossies.org | Sitio Wordpress |
| inurl:/voice/advanced/ intitle:Linksys SPA configuration | Linksys VoIP |
| inurl:github.com intext:.ftpconfig -issues  | Regresa informacion de credenciales ftp guardadas en Github |

### 1.2- Gather Information from Video Search Engines

Lista los metadatos de un video de Youtube, como canal, fecha, ID del video, descripción, los pasos son los siguientes:
1. Ingresa a https://mattw.io/youtube-metadata/
2. Pega el link de tu video de Youtube
3. Da clic en Submit
4. Listo, se cargará la información del video

Ejemplo https://mattw.io/youtube-metadata/?url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DV_i3wCtn0qA&submit=true

**Nota** Con las minitaturas  (thumbnails) se puede hacer una busqueda inversa de las imagenes en google para obtener mayor información.

**Herramientas alternativas que no se aboradaran**
- Google videos (https://www.google.com/videohp)
- Yahoo videos (https://in.video.search.yahoo.com)
- Video analysis tools such as EZGif (https://ezgif.com)
- VideoReverser.com (https://www.videoreverser.com)

**Busqueda inversa de imagenes**
- Reverse image search tools such as TinEye Reverse Image Search (https://tineye.com)
- Yahoo Image Search (https://images.search.yahoo.com), etc. to gather
- Google Image https://images.google.com/

### 1.3- Gather Information from FTP Search Engines 
Los motores de búsqueda FTP proporcionan información sobre archivos y directorios críticos, incluyendo información valiosa como estrategias empresariales, documentos fiscales, registros personales de los empleados, registros financieros, software con licencia y otra información confidencial.

Link:https://www.searchftps.net/

1. Ingresa a https://www.searchftps.net/
2. Ingresa la empresa u objetivo en la caja de texto para buscar
3. Da lic en Search
4. Listo se muestran los resultados

Alternativa No aboradada
Link https://www.freewareweb.com 

### 1.4- Gather Information from IoT Search Engines 
Los motores de búsqueda de IoT rastrean Internet en busca de dispositivos de IoT que sean de acceso público. Estos motores de búsqueda proporcionan información crucial, incluido el control de sistemas SCADA (Supervisión, Control y Adquisición de Datos), sistemas de control de tráfico, electrodomésticos conectados a Internet, electrodomésticos industriales, cámaras CCTV, etc.

En la mayoría debes registratrte y en su versión gratuita las consultas estan limitadas, algunas de la plataformas son:
1.- Shodan - https://www.shodan.io/
2.- Censys - https://censys.com/

En ambas el procedimiento es simple, una vez registrado, puede buscar por:
- IP
- Nombre de la marca del dispositivo
- País
- Protocolo
- Puerto
- Organización / Empresa / Objetivo

## 2. Perform Footprinting Through Web Services

### 2.1 Find the Company’s Domains and Sub-domains using Netcraft
En este tema se muestra la herramienta de netfcrat, si bien cuenta con diferentes funcionalidades, solo se hace enfasis en la herramienta de Site Report, además la intención aquí es buscar subdominios
+ Sitio: https://www.netcraft.com/
+ Sitio de herramientas: https://www.netcraft.com/tools/ **Nota:** Esta URL puede cambiar con el tiempo antes era https://www.netcraft.com/security-testing/
+ Herramienta a utilizar: https://sitereport.netcraft.com/ **Nota:** Para ver los subdominios debes dar clic en **Domain: -> TuSitio.TLD**

**Alternativas para buscar subdominios de Council**
+ Sublist3r [(https://github.com)](https://github.com/aboul3la/Sublist3r) más adelante se aborda
+ Pentest-Tools Find Subdomains (https://pentest-tools.com)

**Recomendación personal para encontrar dominios o subdominios**
+ Para encontrar subdominios en la vida real y no en laboratios https://crt.sh/
+ Ataque de fuerza bruta con gobuster
+ Sublist3r

### 2.2 Gather Personal Information using PeekYou Online People Search Service
Las siguientes son plataformas que te pueden brindar informaciónde personas, sin embargo, son las la gente de USA, además de que todo se tiene que pagar, en los videos lo dan de referencia
- PeekYou (es de paga, solo debes ingresar el nombe de la persona) https://www.peekyou.com/

**Alternativas para no abordadas**
+ https://www.spokeo.com/
+ https://www.beenverified.com/
+ https://www.intelius.com/
+ https://pipl.com/ (Usuarios de redes sociales)

**Nota:** Me da la impresión que todas las plataformas tiene un mecanismo de cargando para solo quitar el tiempo

### 2.3 Gather an Email List using theHarvester

**theHarvester**  
Tipo: Script Python  
Objetivo: Extraer mails  
theHarvester -d  [empresa] -l [# resultados] -b [motor de busqueda]  
theHarvester -d  eccouncil -l 200 -b linkedin"  

**Photon**
Tipo: Script Python  
Objetivo: Es un rastreador web avanzado y una herramienta osint para un análisis exhaustivo de sitios web  

```"Es una crwler, Lista los links fuera del sitio, dentro del sitio y los scripts que utiliza
python3 photon.py -u [url]  
python3 photon.py -u [url] -l 3 -t 200 --wayback 

Comandos
usage: photon.py [options]

  -u --url              root url
  -l --level            levels to crawl
  -t --threads          number of threads
  -d --delay            delay between requests
  -c --cookie           cookie
  -r --regex            regex pattern
  -s --seeds            additional seed urls
  -e --export           export formatted result
  -o --output           specify output directory
  -v --verbose          verbose output
  --keys                extract secret keys
  --clone               clone the website locally
  --exclude             exclude urls by regex
  --stdout              print a variable to stdout
  --timeout             http requests timeout
  --ninja               ninja mode
  --update              update photon
  --headers             supply http headers
  --dns                 enumerate subdomains & dns data
  --only-urls           only extract urls
  --wayback             Use URLs from archive.org as seeds
  --user-agent          specify user-agent(s)"
```


### 2.4 Gather Information using Deep and Dark Web Searching
### 2.5 Determine Target OS Through Passive Footprinting 

##Perform Footprinting Through Social Networking Sites

### Gather Employees’ Information from LinkedIn using theHarvester
### Gather Personal Information from Various Social Networking Sites using Sherlock
### Gather Information using Followerwonk 

##Perform Website Footprinting

### Gather Information About a Target Website using Ping Command Line Utility
### Gather Information about a Target Website using Photon
### Gather information about a Target Website using Central Ops
### Extract a Company’s Data using Web Data Extractor
### Mirror a Target Website using HTTrack Web Site Copier
### Gather Information About a Target Website using GRecon
### Gather a Wordlist from the Target Website using CeWL

## Perform Email Footprinting

### Gather Information About a Target by Tracing Emails using eMailTrackerPro

## Perform Whois Footprinting 

### Perform Whois Lookup using DomainTools 

# Scanning Networks - 03 

# Enumeration - 04
# Vulnerability Analysis - 05
# System Hacking - 06
# Malware Threats - 07
# Sniffing - 08
# Social Engineering - 09
# Denial of Service - 10
# Session Hijacking - 11
# Evading IDS, Firewalls, and Honeypots - 12
# Hacking Web Servers - 13
# Hacking Web Applications - 14
# SQL Injection - 15
# Hacking Wireless Networks - 16
# Hacking Mobile Platforms - 17
# IoT and OT Hacking - 18
# Cloud Computing - 19
# Cryptography - 20
