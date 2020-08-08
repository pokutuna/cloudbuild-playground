FROM alpine:20200626

RUN mkdir /workdir
COPY command.ash /workdir
ENV PATH $PATH:/workdir

ENTRYPOINT ["command.ash"]
