FROM alpine:3.12.0

RUN mkdir /workdir
COPY command.ash /workdir
ENV PATH $PATH:/workdir

ENTRYPOINT ["command.ash"]
