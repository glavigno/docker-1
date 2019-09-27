FROM alpine:latest

RUN apk --no-cache add \
		--repository http://dl-cdn.alpinelinux.org/alpine/edge/community/ \
		emacs

CMD ["/usr/bin/emacs", "-f", "tetris"]

# docker build -t <name> .

# docker run -it --rm <name>
