# ---- build stage ----
FROM ubuntu:24.04 AS build

WORKDIR /src

RUN apt-get update && apt-get install -y --no-install-recommends \
    g++ \
    libcpprest-dev \
    libboost-all-dev \
    libssl-dev \
    ca-certificates \
 && rm -rf /var/lib/apt/lists/*

COPY ok_api.cpp .
RUN g++ -O2 -o ok_api ok_api.cpp \
    -lcpprest -lboost_system -lboost_thread -lboost_chrono -lboost_random -lssl -lcrypto

# ---- runtime stage ----
FROM ubuntu:24.04

# Install only runtime deps needed by the compiled binary
RUN apt-get update && apt-get install -y --no-install-recommends \
    libcpprest2.10 \
    libboost-system1.83.0 \
    libboost-thread1.83.0 \
    libboost-chrono1.83.0 \
    libboost-random1.83.0 \
    libssl3 \
    ca-certificates \
 && rm -rf /var/lib/apt/lists/*

# Create an unprivileged user/group with a fixed UID/GID
RUN groupadd -g 10001 app && useradd -u 10001 -g 10001 -m -s /usr/sbin/nologin app

WORKDIR /app
COPY --from=build /src/ok_api /app/ok_api

RUN chown -R 10001:10001 /app
USER 10001:10001

EXPOSE 8080
CMD ["./ok_api"]
