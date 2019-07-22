FROM kibana:6.5.2

RUN apt update && apt install -y netcat

COPY entrypoint.sh /tmp/entrypoint.sh
RUN chmod +x /tmp/entrypoint.sh

RUN kibana plugin --install elastic/sense

CMD ["/tmp/entrypoint.sh"]
