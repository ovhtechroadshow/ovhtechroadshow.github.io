# CloudDB PostgreSQL

## 1. Podłączenie do bazy danych

Instalujemy klienta postgresql:

```code
sudo apt-get install postgresql-14
```

Sprawdzamy zainstalowaną wersję:

```code
psql --version
```

Podłączamy się do bazy danych:

```code
psql "postgres://username:password@hostname:port/defaultdb?sslmode=require"
```

## Obsługa bazy danych

### Przykładowe polecenia

Lista tabel
```code
\dt
```

Tworzenie tabeli
```code
CREATE TABLE tabela (first TEXT, last TEXT);
```

Listowanie zawartości tabeli
```
SELECT * FROM tabela;
```

Kasowanie tabeli
```
DROP TABLE tabela;
```