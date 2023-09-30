# Active Recon
## Start actively hunting for DNS and subdomains
- amass
- sublist3r
- crtsh
- knockpy
- virustotal
- subfinder
- ffuf
- subbrute
- assetfinder
- find domain
- aquatone
- security trails
- netlas
## Apply permutations based on common Third level domain names like qa, uat, dev, prod, etc
- alt-dns
- shuffledns

Now, sort uniq subdomains(DNS hosts) from above process and ping the subdomains and check if the hosts are up extract these hosts in a file

- extract ip address of these hosts and perform port scan of all the hosts 
- Use httpx to get hosts where web service are running
- Check for dns zone takeovers and subdomain takeovers

## After httpx
- Use eyewitness, webscreenshot tools

## Note
- Use notify to find any new subdomains added by company on a timely basis
```
From above process we will get alive hosts, nmap results of these hosts, web screenshots of hosts where web service is running,
Dns zone takeovers and subdomain takeovers attacks will be checked and made note of. Make 
sure to place every result in a separate directory with proper naming conventions, make note of every interesting detail
```

# Branch Determination and Separation
NOw since we have so many subdomains we forget to separate these into branches
Example we have these subdomains:
```
login.hello.example.com
example.com
test.example.com
api-login.example.com
api.hello.example.com
dev.example.com
login.dev.example.com
login.example.com
api.test.example.com
api.dev.example.com
```
Here we forget that example.com is the company and hello is the branch of that company and api, login, uat, etc are functionalities existing in hello branch of example.com
Similarly dev is another branch of example.com company where login.dev.example.com, api.dev.example.com are functionalities of dev branch of example.com company.

## Bash script to 
- Parse the subdomains to identify the branches.
- For each identified branch, create a file named after the branch and append all subdomains of that branch to the file.

```
#!/bin/bash

input_file=$1


branches=$(awk -F. '{ if (NF > 2) print $(NF-2) }' $input_file | sort -u)

for branch in $branches; do
  matching_subdomains=$(grep "\.$branch\." "$input_file")
  if [[ ! -z "$matching_subdomains" ]]; then
    echo "$matching_subdomains" > "$branch"
  fi
done

grep -Ev "\.($(echo $branches | tr ' ' '|')\.)" "$input_file" > "others"

```
# Passive Recon
- Google what is the company and its primary purpose
- Use google dork with specific extensions, filenames, language,logins,etc (https://github.com/alexdhital/google-dorks) forked from provisec
- Search company's trademark or copyright and use them in shodan 
- Use censys to check what services, softwares, platform the company is using 
- Search company employees name, branches in linkedin
- Keep notes( login panels, software frameworks, grafana endpoints, JIRA, SSL VPNs, etc)
- Perform github recon with company name or domain and filter results using NOT operator 
- perform gists recon
- Perform github recon on organizations's employees working for that organization
- Keep notes from github recon apikeys, secret, password, pwd, etc
- Past data breaches? if some encrypted hash found use https://dehashed.com

## Github recon tools
- gitrob
- githound
- sshgit
- trufflehog
- git-all-secrets
- gitgrabber

# Attack

## After eyewitness results have been completed
- Take each single domain where web service is running
- Stack/Technology identification
- See branches and related functionalities api,login,etc for this domain
- Gau to identify urls
- Default logins? admin:admin, demo:demo, test:test
- Maybe try bypassing 403, 401?
- Protected by .htaccess bruteforce?
- AWS S3 bucket pentesting
- Found api keys like algolia, firebase, salesforce during git recon? => https://github.com/alexdhital/keyhacks 
- Functioanlities attacks(OWASP TOP 10)
- Fuzz input fields or GET parameters, Post paremeters using big-list-of-naughty-strings.txt
- Arjun, FFUF, param discovery, param spider
- CRUD operations performed by the application => PUT, GET, POST, PATCH, DELETE
- Always try understanding the functionality. Frontend => API => Database? Frontend => Backend=> Database? , MVC pattern?
- Always test OWASP bugs on api endpoints

## Content Discovery
- directory discovry
- common filenames discovery
- Discovery based upon stack? CMS,.php, .asp, .aspx, .jsp, etc
- JS Files discovery

## Tools for JS Files discovery 
- JSParser
- LinkFinder
- GetJS
- InputScanner
- JSScan
- Manually discovering

# Check Previous run nmap results then
- Identify services
- Find outdated version and their exploits
- Find services misconfigurations and exploits
- Gather information(eg: username identification)
- Test gathered usernames or passwords from previous/above test on network services like mssql, mysql, ftp, web logins, smtp, etc
- Take notes
- Utilize Hacktricks
