FROM alpine/git AS git
WORKDIR /app
# RUN git clone https://gitlab.com/v1996-96/kms-backend.git .
RUN git clone git@gitlab.com:v1996-96/kms-publish.git .

FROM postgres:latest
RUN mkdir -p "$PGDATA" && chmod 700 "$PGDATA"
COPY dump.sh /docker-entrypoint-initdb.d/dump.sh
COPY --from=git /app/dump.sql /app/dump.sql
EXPOSE 5432