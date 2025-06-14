FROM python:3.12-alpine3.20 AS builder

WORKDIR /app
COPY requirements.txt .
RUN apk update && \
    apk upgrade --no-cache && \
    apk add --no-cache build-base && \
    pip install --upgrade pip && \
    pip install --prefix=/install -r requirements.txt --no-cache-dir

FROM python:3.12-alpine3.20

WORKDIR /app
COPY --from=builder /install /usr/local
COPY . .

RUN apk update && \
    apk upgrade --no-cache && \
    apk add --no-cache rsync git nodejs npm && \
    rm -rf /var/cache/apk/* /root/.cache

USER nonroot

ENTRYPOINT ["mkdocs"]
CMD ["serve", "--dev-addr", "0.0.0.0:8000"]
