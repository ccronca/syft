FROM alpine:3.20.2@sha256:eddacbc7e24bf8799a4ed3cdcfa50d4b88a323695ad80f317b6629883b2c2a78 as tools
FROM scratch
COPY --from=tools /bin /bin
COPY --from=tools /lib /lib
ADD . .
RUN rm -rf file-1.txt /bin /lib
