# Postgres

```yaml
version: '3.1'
services:
  db:
    image: postgres
    volumes:
      - pgdata:/var/lib/postgresql/data/
    ports:
      - 5432:5432
    restart: always
    environment:
      POSTGRES_PASSWORD: example

volumes:
  pgdata:
```
