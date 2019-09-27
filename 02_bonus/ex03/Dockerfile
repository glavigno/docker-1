FROM node:0.12.7-slim

ENV REICHAT_VERSION 0.0.35

RUN npm install -g reichat@${REICHAT_VERSION}
ENTRYPOINT ["/usr/local/bin/reichat"]

CMD ["--host","0.0.0.0","--port","10133"]

EXPOSE 10133

# docker build -t <name> .

# docker run -p 10133:10133 <name>
