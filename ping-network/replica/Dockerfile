# ./replica/Dockerfile
FROM ubuntu:latest

ARG REPLICA_ID
ENV REPLICA_ID=$REPLICA_ID

RUN apt-get update && \
    apt-get install -y netcat-traditional && \
    rm -rf /var/lib/apt/lists/*

RUN echo '#!/bin/bash\n\
echo "Starting $REPLICA_ID..."\n\
while true; do\n\
    nc -l -p 8080 | while read line; do\n\
        echo "Received on $REPLICA_ID: $line"\n\
        echo "Pong from $REPLICA_ID at $(date)!"\n\
    done\n\
done' > /replica.sh

RUN chmod +x /replica.sh

EXPOSE 8080

CMD ["/replica.sh"]
