FROM node:8-alpine

WORKDIR /app

# Copy app, expects the app to be in the ./bundle dir
COPY . .

# Install build dependencies
# Rebuild packages
# Clean up
RUN apk add --no-cache --virtual deps python g++ gcc make && \
  npm install --global npm@5 node-gyp node-pre-gyp && \
  npm install cfenv@1.0.4 && \
  cd bundle/programs/server && \
  npm install --unsafe-perm && \
  cd /app && \
  apk del --purge deps && \
  npm uninstall node-gyp node-pre-gyp && \
  npm cache clear --force && \
  rm -vrf /usr/share/* /tmp/* /var/cache/apk /home/node /root/* /opt \
   /usr/local/lib /usr/local/include /usr/local/share 

ENV PORT 8080
EXPOSE 8080

CMD ["node", "launcher.js"]
