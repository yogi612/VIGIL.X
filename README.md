# VIGILI.X - A subdomain enumeration tool




VIGILI.X is a fast and reliable python script that makes active and/or passive scan to obtain subdomains and search for open ports. This tool is recommended for bug bounty hunters and pentester in their reconnaissance phase.


>the more surface area exposed the faster a rock with break down



If you want to use more OSINT engines, fill the **config.api** file with the needed API tokens

### Passive Mode:
Use OSINT techniques to obtain subdomains from the target. This mode will not make any connection to the target so it is **undetectable**.
The basic use of this mode is:
```sh
python VIGILI.X.py -m passive -d domain
```

### Active Mode:
Perform bruteforce attacks to obtain alive subdomains. 
There are 2 types of bruteforce:
- **Pure Bruteforce**: Check subdomains from a.domain.com to zzz.domain.com (26 + 26^2 + 26^3 = 18278 subdomains) this bruteforce can be disabled with `-nb, --no-bruteforce`
- **Wordlist based**: Use a custom wordlist provided by the user using the flag `-w, --wordlist`. If no wordlists is specified, this mode won't be executed

This mode will also make passive mode attack but in this case, the connection is tested to ensure the subdomain is still alive. To disable passive scan in active scan mode, use `--no-passive` flag

The basic use of this mode is:
```sh
python VIGILI.X.py -m active -d domain -w wordlist.txt
```

Add `-p` option or a built-it port option (see usage menu) to perform port scanning

```sh
python VIGILI.X.py -m active -d domain -w wordlist.txt -p 80,443,8080
```

## Installation

You can run VIGILI.X with [Python](https://www.python.org/) 2 or 3. **Python3 is recommended**

Install the dependencies and run the program

```sh

cd VIGIL.X
pip install -r requirements.txt
python VIGIL.X.py --help
```


## Top Features

- Easy to use. Just install the requirements.txt and run
- Active and Passive scan (read above)
- Faster than other subdomain enumeration tools
- 7 different resolvers/nameservers including google, cloudfare (fastest), Quad9 and cisco DNS (use --resolvers filename.txt to use a custom list of resolvers, one per line)
- Up to 21 different OSINT sources
- Subdomains obtained via OSINT are tested to know if they are alive (only in active mode)
- Support for webs that requires API token
- Detects when api key is no longer working (Other tools just throw an error and stops working)
- Wildcard detection and bypass
- Custom Port scaning and built-in params for Top100,Top1000 and Top Web ports
- Colored and uncolored output for easy read
- Windows and Python 2/3 support (Python 3 is recommended)
- Highly customizable through arguments
- Scan more than one domain simultaneously
- Possibility to use threads for faster bruteforce scans
- Export output in different formats such as txt, json, html



## OSINT Search Engines

VIGILI.X uses these web pages to obtain subdomains

Without API:

- AlienVault
- HackerTarget
- RapidDNS
- ThreatMiner
- web.archive.org
- crt.sh
- CertSpotter
- Anubis-DB
- SiteDossier
- DNSrepo

With API:

- VirusTotal
- Shodan
- FullHunt
- SecurityTrails
- PassiveTotal
- BinaryEdge


## TODO List

Feel free to implement this features

- [x] Add arguments
- [x] Add DNS wildcard detection and bypass
- [x] Add port scan and port argument
- [x] Add colored screen output (also option for no-colour)
- [x] Add -i option to show the subdomains' IP address
- [x] Add --silent argument to show nothing on screen
- [x] Create a dicc structure like {"ip": "domain"} to avoid duplicate port scans
- [x] Generate output in html and json format, also a txt for subdomains found during scan
- [x] Add timestamps
- [x] Add more OSINT engines with API token (create config file)
- [x] Add compatibility with Windows 
- [x] Add compatibility with Python 2.7
- [x] Add Shodan for passive open ports? (Check requests limit with api key)
- [x] Add support for domains like .gov.uk (at this moment, the program only works with one level domain like domain.com) (https://publicsuffix.org/list/public_suffix_list.dat)
- [x] Added DNS resolvers
-
	




## Usage

| Arguments | Description | Arg example |
| ------ | ------ | ------ |
| -m, --mode | Scan mode. Valid options: active or passive | active
| -d, --domain | Domains name to enumerate subdomains (Separated by commas) | hackerone.com,facebook.com
| -w, --wordlist | Wordlist containing subdomain prefix to bruteforce | subdomains-5000.txt
| -i, --ip | When a subdomain is found, show its ip | 
| --no-passive | Do not use OSINT techniques to obtain valid subdomains |
| -nb, --no-bruteforce | Dont make pure bruteforce up to 3 letters |
| -p, --ports | Scan the subdomains found against specific tcp ports | 80,443,8080
| --top-100-ports | Scan the top 100 ports of the subdomain (Not compatible with -p option) |
| --top-1000-ports | Scan the top 1000 ports of the subdomain (Not compatible with -p option) |
| --top-web-ports | Scan the top web ports of the subdomain (Not compatible with -p option) |
| -s, --silent | Silent mode. No output in terminal |
| --no-color | Dont print colored output |
| -t, --threads | Number of threads to use (Default: 25) | 20
| -o, --output | Save the results to txt, json and html files |
| --max-response-size | Maximun length for HTTP response (Default:5000000 (5MB)) | 1000000
| --r, --resolvers | Textfile with DNS resolvers to use. One per line | resolvers.txt
| -h, --help | Help command | 
| --version | Show VIGILI.X version and exit| 
| -v, --verbose | Show more information during execution | 


## Examples


Perform active and passive scan, show the ip adress of each subdomain and make a port scan using top-web-ports. Data will also be written in /results folder:
```sh
python VIGILI.X.py -m active -d domain -w wordlist.txt -i --top-web-ports -o
```

Perform passive scan in silent mode and write output to files.
```sh
python VIGILI.X.py -m passive -d domain --silent --output
```


Perform active scan without passive and port scan
```sh
python VIGILI.X.py -m active -d domain -w wordlist.txt --no-passive
```

Only bruteforce with wordlist
```sh
python VIGILI.X.py -m active -d domain -w wordlist.txt --no-bruteforce
```

Scan active and passive and perform port scan ONLY in ports 22,80,3306
```sh
python VIGILI.X.py -m active -d domain -w wordlist.txt -p 22,80,3306
```
