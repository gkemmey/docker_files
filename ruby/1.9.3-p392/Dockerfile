# we're gonna use the buildpack-deps after waging an internal struggle on the right way to do things
# because it seems fairly par for the course
FROM buildpack-deps:jessie

# global configuration to skip installing gem documentation
RUN mkdir -p /usr/local/etc \
	&& { \
		echo 'install: --no-document'; \
		echo 'update: --no-document'; \
	} >> /usr/local/etc/gemrc

ENV RUBY_VERSION 1.9.3-p392
ENV RUBY_INSTALL_VERSON 0.6.0

# i think it's fine just to use the most recent here, not positive
ENV BUNDLER_VERSION 1.13.2

# if i install this ruby version on my system using ruby-install this looks to be what i get
# for a rubygems version. solid decision making there...
ENV RUBYGEMS_VERSION 1.8.23

# intall ruby-install, because why intall ruby ourselves when smarter guys then us have made it easy
RUN set -ex \
        && wget -O ruby-install.tar.gz "https://github.com/postmodern/ruby-install/archive/v$RUBY_INSTALL_VERSON.tar.gz" \
        && tar -xzvf ruby-install.tar.gz \
        && make -C ruby-install-$RUBY_INSTALL_VERSON -f Makefile install \
        && rm -rf ruby-install-$RUBY_INSTALL_VERSON/ \
        && rm -f ruby-install.tar.gz

# prepare to install ruby
RUN apt-get update

# install ruby
RUN ruby-install ruby $RUBY_VERSION

# add ruby executable path to PATH
ENV PATH /opt/rubies/ruby-$RUBY_VERSION/bin:$PATH

# install bundler
RUN gem install bundler --version "$BUNDLER_VERSION"

# silence bundler warnings
ENV BUNDLE_SILENCE_ROOT_WARNING=1

CMD [ "irb" ]
