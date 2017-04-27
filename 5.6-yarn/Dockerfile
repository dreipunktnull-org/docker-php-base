FROM dreipunktnull/docker-php-base:5.6

ENV NVM_DIR $HOME/.nvm

ENV NODE_VERSION 7.9

RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.1/install.sh | bash && \
  \. "$NVM_DIR/nvm.sh" && \
  nvm install $NODE_VERSION && \
  npm install -g yarn

# Expand path to opt
ENV PATH /opt/bin:$PATH
