CEH v12 Practical / CEH v12 Guia de estudio para examen practico

La siuiente es una guia de las herrramientas y comandos que se utilizaron en cada uno de los modulos de la certificación CEH v12, se tomo en cuenta el material de Ecourseware (Especialmente la sección de laboratios), para fines practicos se mencionaran las herramientas que se consideren más utiles, ya que bajo mi perspectiva la certificación utiliza multiples herramientas para con un mismo fin, es posible que se mencionen más solo se abordará una

# Introduction to Ethical Hacking - 01 
Este modulo esencialemente es teorico y no sé abordan herrramientas.

# Footprinting and Reconnaissance - 02 
## 1- Perform Footprinting Through Search Engines 
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

### 1.1- Gather Information from FTP Search Engines 
Como obtener los metadatos de un video de Youtube 

### 1.2- Gather Information using Advanced Google Hacking Techniques
### 1.3- Gather Information from Video Search Engines
### 1.4- Gather Information from IoT Search Engines 

## Perform Footprinting Through Web Services

### Find the Company’s Domains and Sub-domains using Netcraft
### Gather Personal Information using PeekYou Online People Search Service
### Gather an Email List using theHarvester
### Gather Information using Deep and Dark Web Searching
### Determine Target OS Through Passive Footprinting 

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
