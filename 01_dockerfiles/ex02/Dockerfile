FROM ruby

RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y nodejs

ONBUILD COPY myapp /opt/app
ONBUILD WORKDIR /opt/app

ONBUILD EXPOSE 3000

ONBUILD RUN bundle install
ONBUILD RUN rake db:migrate

# To launch the server, execute the following commands in the ex02/ folder

# build the image from the child dockerfile
# the name ("ft-rails:on-build") matches the parent 'FROM'
# docker build -t ft-rails:on-build -f <Dockerfile_source> .

# build the image from the parent dockerfile
# copy the content of the Dockerfile in the subject in a file
# docker build -t <name> -f <Dockerfile_source> .

# finally, run the image created with appropriate flags
# docker run -it --rm -p 3000:3000 <name>
