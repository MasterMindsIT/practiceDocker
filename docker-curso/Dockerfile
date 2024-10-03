FROM ubuntu
ENV DEBIAN_BACKEND=ADMIN
ENV version=1.0

ARG TEXT_EDITOR=nano
RUN apt-get update && apt-get install -y \
     python3 \
     curl \
     ${TEXT_EDITOR} \
     nginx

COPY . /app
WORKDIR /app
# RUN chmod -x entrypoint.sh
#ENTRYPOINT ./entryoint.sh
ENTRYPOINT ["nginx", "-g", "daemon off;"]