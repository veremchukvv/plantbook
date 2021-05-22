FROM migrate/migrate:v4.14.1
ADD ../../database/migrations_schema /database/migrations_schema
WORKDIR /database
ENTRYPOINT ["migrate -database postgres://plantbook_admin:mypassword@plantbook-testdb:5432/plantbook_admin?sslmode=disable -path ./migrations_schema up"]
LABEL org.opencontainers.image.source https://github.com/veremchukvv/plantbook