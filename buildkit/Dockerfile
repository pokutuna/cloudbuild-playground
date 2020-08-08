FROM alpine:latest

RUN mkdir /workdir
COPY command.ash /workdir
ENV PATH $PATH:/workdir

ENTRYPOINT ["command.ash"]
