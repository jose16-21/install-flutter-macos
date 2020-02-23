sudo yum install gcc
sudo yum install wget
wget http://download.redis.io/redis-stable.tar.gz
tar xvzf redis-stable.tar.gz
cd redis-stable
make
sudo cp src/redis-cli /usr/local/bin/
redis-cli -h yourhost.com -p 6379