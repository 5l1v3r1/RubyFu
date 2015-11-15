# Parsing HTML, XML, JSON

Generally speaking the best and easiest way for parsing HTML and XML is using **Nokogiri** library

- To install Nokogiri
```
gem install nokogiri
```

## HTML


```ruby
require 'nokogiri'
require 'open-uri'

page = Nokogiri::HTML(open("http://rubyfu.net/content/"))
page.css(".book .book-summary ul.summary li a, .book .book-summary ul.summary li span").each { |css| puts css.text.strip.squeeze.gsub("\n", '')}
```

## XML
There are 2 ways we'd like to show her, the standard library `rexml` and `nokogiri` external library 


### REXML




### Nokogiri


## JSON
