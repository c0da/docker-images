FROM alpine:3.16

ENV REMOTE_PORT=80
ENV LOCAL_PORT=80

EXPOSE 80

RUN echo "Installing base packages" \
         && apk add --update --no-cache \
	         socat \
         && echo "Removing apk cache" \
	 && rm -rf /var/cache/apk/

CMD socat tcp-listen:$LOCAL_PORT,reuseaddr,fork tcp:$REMOTE_HOST:$REMOTE_PORT & pid=$! && trap "kill $pid" SIGINT && \
    echo "Socat started listening on $LOCAL_PORT: Redirecting traffic to $REMOTE_HOST:$REMOTE_PORT ($pid)" && wait $pid
