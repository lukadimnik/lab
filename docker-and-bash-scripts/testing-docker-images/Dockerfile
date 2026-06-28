FROM ubuntu:24.04

RUN apt-get update && apt-get install

WORKDIR /app

COPY juhu .

RUN chmod +x juhu

CMD ["./juhu"]

