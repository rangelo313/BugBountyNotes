# Recon
Look for acquisitions and ASN's of this company on Crunchbase.
the older the acquisitions the less likely we get anything out of them, look for sub 2 year acquisitions.
Large scale bounty on these targets...

Grab the ASN's (reference # for all of their registered ip space) for these companies. 
bgp.he.net 

Run some tooling to see what other seed domains we can get out of these ranges. One way to do that is to use amass.
amass intel --asn <#>
What this will do is it will take the AS # and go out and scan that large piece of IP Space, check for sites that respond to HTTPS/SSL connections
then it will parse out of the certificate data any seed data that it finds (certificate pulls). 

The more seeds/roots we get, the more subdomains we are able to enumerate. The more subdomains we enumerate the more websites we can find.

 ASN enumeration tools include: Metabigor by j3ssiejjj or ASNLookup by Yassine Aboukir
 
 
 Reversewhois
 Goes to websites that aggregates whois data... whoxy.com
 whoxy gives many api searches.
ex:  Officedepot gives lookups on other domains that have registered with office depot inc.
 Much of this will result in parked data... reversewhois is a medium fidelity technique, you may be able to find something in what returns.
 
 You can automate this with DomLink by Vincent Yiu which will recursively query the whoxy whois api. 
 It will start by querying our targets whoisrecord, then analyze all of the data and look for other records which contain the organization name or are registered to emails in the record. It does this recursively until it finds no more records of match....
 
 
Builtwith.com allows you to enter in a website/address/etc and allows you to view analytics tracker tags...
You can surmise they use the same analytics codes in the same sites they have...
You can also use this in the command line with getrelationship.py 

Google-Fu....
copyright policy
ex: "by Office Depot LLC All rights reserved" www.officedepot.com


You can use shodan to continuously spider infrastructure on the internet.


Linked Discovery with Burpsuite Pro
1.) Scope (ex: office) accumulate outside of scope data (No)
2.) Crawl these domains. 
3.) Crawl Strategy: Faster -never stop crawl due to application error
4.) Resource pool: 100 max concurrent requests

Cool Burp Extensions:
Flow extension (logger for all tools) and Error Extension (gives if certain errors are found). Burp JS Link finder (parses any js file found through burp).. Hunt RMX. BurpBounty (ActiveScan Maker). Software Vulnerability Scanner. 

Other tools: GoSpider or Hakrawler

## Subdomain Enumeration
Subdomainizer or Subscraper

In burp pro, right click on a site under site map, search .js and grab all of the .js files, copy the selected urls and run subdomainizer or wslder 

Subdomain Scraping
Tools: Amass enum, github-subdomains.py, showsubgo, and subfinder...
Usage:
amass enum -d <target>
  This will go out to every source -> infrastructure sources, search sources, etc.
  tries to find references for subdomains of this target
  
Another tool- Runs several tools like amass 
  /hunter3.sh <target>
 
  Points out Github Dork Links
  
 Subfinder, github-subdomains.py (Gwendal) and Github-search also works out for this.
  gwen001
  
 GH subdomains will go out to the gh api and look for all subdomains in that sourcecode. That will run as part of automation.

  Subdomain Scraping (Cloud Ranges)
  amass you can parse the extensions for all of the http sites
 
  ## Subdomain takeover
 Use EdOverflow can-i-take-over-xyz
 404 not found do content discovery
  
  -Nuclei: scanner that looks for CVE's, login portals, interestig pages. Has the most subdomain takeover signatures.
    nuclei -l httprobe.txt -t subdomain-takeover/*
  -httpprobe outfile 
  
waybackurls fetches all old urls known for a domain
  meg: directory bruteforcing across many hosts 
 
View Page Source- see when it was last updated

## Subdomain bruteforcing
  amass enum -brute -d <domain> -src
 ShuffleDNS also does bruteforcing, it is a wrapper around massDNS
 all.txt is a good file to use with bruteforcing
 
  Favicon Analysis (Favfreak)
  Favicon icon is used for the specific company. You can scan ip ranges to look for the favicon icon or use shodan to look for the favicon hash.
  
  cat urls.txt | python3 favreak.py -o output
  shodan search org:"Target" http.favicon.hash:<number> --fields ip str,port --separator " " | awk '{print $1": "$2}'
  
## Port Analysis
  dnmassan
  one limitation of masscan is that it only scans IP addresses
  You can write your own simple converter sccript or use something like dnsmassscan
  
 ## Frameworks
  bountyRecon
  offhoruscoding/recon
  Sambal0x/Recon-tools
  AutoRecon
  yourbuddy25/hunter
  venom26/ultimate_recon.sh
  
 ## XSS Hunter 
  Create a new active scan, and load your xss hunter payload and append to everything (every insertion point). 
  No response- and now you have a blind xss scan. This should be added under Burp Bounty.
  
