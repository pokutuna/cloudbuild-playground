FROM alpine:3.11

RUN mkdir /workdir
COPY command.ash /workdir
ENV PATH $PATH:/workdir

ENTRYPOINT ["command.ash"]
