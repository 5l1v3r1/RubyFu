# Virustoral 
Virsuttotal is one of the most known online service that analyzes files and URLs enabling the identification of viruses, worms, trojans and other kinds of malicious content detected by antivirus engines and website scanners. At the same time, it may be used as a means to detect false positives, i.e. innocuous resources detected as malicious by one or more scanners.


## Getting Virustotal 
1. Register/Sign-in to Virustotal
2. Go to **My API key**
3. Request a private APT key
 - Do not disclose your private key to anyone that you do not trust.
 - Do not embed your private in scripts or software from which it can be easily retrieved

## Virustotal gem 
ruby-virustotal is virustotal automation and convenience tool for hash, file and URL submission.

- Install virustotal gem 
```
gem install virustotal
```

## Command line usage
You can use ruby-virustotla gem as command line tool 

- Create virustotal local profile 
 
to interact with virustotal as 
```
virustotal --create-config
```

- Searching a file of hashes
```
virustotal -f <file_with_hashes_one_per_line>
```

- Searching a single hash



## uirusu gem 
uirusu is an Virustotal automation and convenience tool for hash, file and URL submission.

- Install uirusu 
```
gem install uirusu
```

