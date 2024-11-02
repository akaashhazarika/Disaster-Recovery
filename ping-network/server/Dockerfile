# ./server/Dockerfile
FROM ubuntu:latest

RUN apt-get update && \
    apt-get install -y netcat-traditional dnsutils && \
    rm -rf /var/lib/apt/lists/*

RUN echo '#!/bin/bash\n\
echo "Server starting..."\n\
\n\
broadcast_to_replicas() {\n\
    local message="$1"\n\
    for replica in replica-1 replica-2; do\n\
        echo "Broadcasting to $replica..."\n\
        echo "$message" | nc -w 1 "$replica" 8080 || echo "Failed to reach $replica"\n\
    done\n\
}\n\
\n\
while true; do\n\
    echo "Waiting for client message..."\n\
    nc -l -p 8080 | while read message; do\n\
        echo "Received from client: $message"\n\
        broadcast_to_replicas "$message" &\n\
    done\n\
done' > /server.sh

RUN chmod +x /server.sh

EXPOSE 8080

CMD ["/server.sh"]

