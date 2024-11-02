# ./client/Dockerfile
FROM ubuntu:latest

RUN apt-get update && \
    apt-get install -y netcat-traditional && \
    rm -rf /var/lib/apt/lists/*

RUN echo '#!/bin/bash\n\
echo "Client starting..."\n\
while true; do\n\
    message="Message from client: $(date)"\n\
    echo "Sending: $message"\n\
    echo "$message" | nc -w 1 server 8080\n\
    sleep 3\n\
done' > /client.sh

RUN chmod +x /client.sh

CMD ["/client.sh"]
