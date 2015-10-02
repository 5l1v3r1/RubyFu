# SSH
Here we shows some SSH using ruby
we'll need to install net-ssh gem for that

```
gem install net-ssh
```


## Simple SSH client
This is a very basic ssh client which sends and executes commands on a remote system 
```ruby
require 'net/ssh'

@hostname = "localhost"
@username = "root"
@password = "password"
@cmd = ARGV[0]

begin
  ssh = Net::SSH.start(@hostname, @username, :password => @password)
  res = ssh.exec!(@cmd)
  ssh.close
  puts res
rescue
  puts "Unable to connect to #{@hostname} using #{@username}/#{@password}"
end
```

more
https://gist.github.com/KINGSABRI/2860989

## SSH Tunneling




### Forward SSH Tunnel

```
                              |--------DMZ------|---Local Farm----|
                              |                 |                 |
|Attacker| ----SSH Tunnel---> | |SSH Server| <-SSH-> |Web server| |
                              |                 |                 |
                              |-----------------|-----------------|
```

#### Local Port Forwarding

```ruby
#!/usr/bin/evn ruby
require 'net/ssh'

Net::SSH.start("127.0.0.1", 'root', :password => '123132') do |ssh|
  # Forward connections coming on port 2222 to port 22 of attacker.zone
  ssh.forward.local('0.0.0.0', 2222, "attacker.zone", 22)
  
  puts "[+] Starting SSH port forward tunnel"
  ssh.loop { true }
end
```
- Now ssh to the SSH SSH server on port 2222, you'll be prompt for SSH server the Web Server ssh password

```
ssh SshServer -p 1234
```


**ssh-fw-tunnel.rb**
```
#!/usr/bin/env ruby 
require 'net/ssh/gateway'

```


### Reverse SSH Tunnel 
```
                              |--------DMZ------|---Local Farm----|
                              |                 |                 |
|Attacker| <---SSH Tunnel---- | |SSH Server| <-SSH-> |Web server| |
                              |                 |                 |
                              |-----------------|-----------------|
```








<br><br><br>
---





