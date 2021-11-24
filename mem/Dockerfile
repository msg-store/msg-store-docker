FROM rust:latest as builder
RUN git clone https://github.com/msg-store/msg-store-server.git
WORKDIR /msg-store-server
RUN cargo update -p libc
RUN cargo install --path .

# FROM debian:buster-slim
# RUN apt-get update
# RUN apt-get install -y git rustc && rm -rf /var/lib/apt/lists/*
# RUN git clone https://github.com/msg-store/msg-store-server.git
# WORKDIR /msg-store-server
# RUN cargo install --path .
# COPY --from=builder /usr/local/cargo/bin/msg-store /usr/local/bin/msg-store
# CMD ["msg-store"]

FROM debian:buster-slim
RUN apt-get update
RUN mkdir /etc/msg-store-server
# RUN apt-get install -y extra-runtime-dependencies && rm -rf /var/lib/apt/lists/*
COPY --from=builder /usr/local/cargo/bin/msg-store-server /usr/local/bin/msg-store-server
# EXPOSE 8080
COPY ./config.json /etc/msg-store-server/
# VOLUME [ "/etc/msg-store-server/" ]
CMD ["msg-store-server", "--config", "/etc/msg-store-server/config.json"]
