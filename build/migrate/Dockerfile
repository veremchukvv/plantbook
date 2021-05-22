FROM migrate/migrate:v4.14.1
ADD . /database/migrations_schema/
ENTRYPOINT ["migrate"]
CMD ["-database postgres://localhost:5432/database"]
LABEL org.opencontainers.image.source https://github.com/veremchukvv/plantbook