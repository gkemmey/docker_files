FROM ubuntu:16.10
MAINTAINER Gray Kemmey <gray.kemmey@gmail.com>

# get apt ready
RUN apt-get update

RUN apt-get install -y build-essential wget

# install ruby-install
RUN wget -O ruby-install-0.6.0.tar.gz https://github.com/postmodern/ruby-install/archive/v0.6.0.tar.gz
RUN tar -xzvf ruby-install-0.6.0.tar.gz
RUN make -C ruby-install-0.6.0 -f Makefile install

# cleanup ruby-install
RUN rm -rf ruby-install-0.6.0/
RUN rm -f ruby-install-0.6.0.tar.gz

# install ruby
RUN ruby-install ruby 1.9.3-p392

# link ruby stuff, we know this is where ruby-install will put everything when installed as root
RUN ln -s /opt/rubies/ruby-1.9.3-p392/bin/erb /usr/local/bin/erb
RUN ln -s /opt/rubies/ruby-1.9.3-p392/bin/gem /usr/local/bin/gem
RUN ln -s /opt/rubies/ruby-1.9.3-p392/bin/irb /usr/local/bin/irb
RUN ln -s /opt/rubies/ruby-1.9.3-p392/bin/rake /usr/local/bin/rake
RUN ln -s /opt/rubies/ruby-1.9.3-p392/bin/rdoc /usr/local/bin/rdoc
RUN ln -s /opt/rubies/ruby-1.9.3-p392/bin/ri /usr/local/bin/ri
RUN ln -s /opt/rubies/ruby-1.9.3-p392/bin/ruby /usr/local/bin/ruby
RUN ln -s /opt/rubies/ruby-1.9.3-p392/bin/testrb /usr/local/bin/testrb

# clean cached files
RUN apt-get clean
