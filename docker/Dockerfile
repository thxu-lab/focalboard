## Final image
FROM debian:buster-slim@sha256:5b0b1a9a54651bbe9d4d3ee96bbda2b2a1da3d2fa198ddebbced46dfdca7f216

# Create directories and set permissions
RUN mkdir -p /opt/focalboard/data/files && \
    chown -R nobody:nogroup /opt/focalboard

WORKDIR /opt/focalboard

# Copy binaries and webapp (remove `server_config.json`)
COPY --from=nodebuild --chown=nobody:nogroup /webapp/pack pack/
COPY --from=gobuild --chown=nobody:nogroup /go/src/focalboard/bin/docker/focalboard-server bin/
COPY --from=gobuild --chown=nobody:nogroup /go/src/focalboard/LICENSE.txt LICENSE.txt

# Use environment variables instead of `config.json`
USER nobody

EXPOSE 8000/tcp 9092/tcp

VOLUME /opt/focalboard/data

CMD ["/opt/focalboard/bin/focalboard-server"]
