FROM debian

RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y curl openssh-server ca-certificates postfix

RUN curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | bash
RUN apt-get install -y gitlab-ce

RUN apt update && apt install -y tzdata && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN mkdir -p /etc/gitlab/ssl && chmod 700 /etc/gitlab/ssl
RUN openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
	-subj "/C=FR/ST=Paris/L=Paris/O=my_org/CN=my_org.com" \
	-keyout /etc/gitlab/ssl/mykey.key -out /etc/gitlab/ssl/mycrt.crt

RUN echo "external_url \"https://192.168.99.100\"" >> /etc/gitlab/gitlab.rb
RUN	echo "nginx['redirect_http_to_https'] = true" >> /etc/gitlab/gitlab.rb
RUN	echo "nginx['ssl_certificate'] = \"/etc/gitlab/ssl/mycrt.crt\"" >> /etc/gitlab/gitlab.rb
RUN	echo "nginx['ssl_certificate_key'] = \"/etc/gitlab/ssl/mykey.key\"" >> /etc/gitlab/gitlab.rb
RUN echo "gitlab_rails['gitlab_shell_ssh_port'] = 777" >> /etc/gitlab/gitlab.rb 

EXPOSE 22 80 443

ENTRYPOINT service ssh restart && (/opt/gitlab/embedded/bin/runsvdir-start &) && \
			gitlab-ctl reconfigure && tail -f /dev/null


# create a new and optimized VM to build and run this Dockerfile
# docker-machine create -d virtualbox --virtualbox-memory "4096" --virtualbox-cpu-count "2" gitlabmachine
# eval $(docker-machine env gitlabmachine)

# docker build -t <name> .
# docker run -it -p 80:80 -p <ssh_port>:22 -p 443:443 --privileged <name>

# HTTPS Configuration

# GIT_SSL_NO_VERIFY=true before every command
# GIT_SSL_NO_VERIFY git clone <https_repo_link>

# SSH Configuration

# generate a keygen if needed
# copy it in the Gitlab settings
# ssh-agent $(ssh-add gitlab.key; git clone <ssh_repo_link>)
