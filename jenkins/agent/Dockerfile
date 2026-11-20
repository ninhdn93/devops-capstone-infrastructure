
# Node.js toolchain
FROM node:22-bookworm-slim AS node-runtime

# Jenkins inbound agent
FROM jenkins/inbound-agent:latest-jdk21

USER root

# Copy Node.js and npm toolchain
COPY --from=node-runtime /usr/local/bin/node /usr/local/bin/node
COPY --from=node-runtime /usr/local/lib/node_modules /usr/local/lib/node_modules

RUN ln -s /usr/local/lib/node_modules/npm/bin/npm-cli.js /usr/local/bin/npm \
    && ln -s /usr/local/lib/node_modules/npm/bin/npx-cli.js /usr/local/bin/npx \
    && node --version \
    && npm --version

# Run Jenkins agent without root privileges
USER jenkins
