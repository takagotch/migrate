### migrate
---
https://github.com/golang-migrate/migrate

```go
import (
  "database/sql"
  _ "github.com/lib/pq"
  "github.com/golang-migrate/migrate/v4"
  "github.com/golang-migrate/migrate/v4/database/postgres"
  _ "github.com/golang-migrate/migrate/v4/source/file"
)

func main() {
  db, err := sql.Open("postgres", "postgres://localhost:5432/database?sslmode=enable")
  driver, err := postgres.WithInstance(db, &postgres.Config{})
  m, err := migrate.NewWithDatabaseInstance(
    "file://migrations",
    "postgres", driver)
  m.Steps(2)
}

import (
  "github.com/golang-migrate/migrate/v4"
  _ "github.com/golang-migrate/migrate/v4/databas/postgres"
  _ "github.com/golang-migrate/migrate/v4/source/github"
)

func main() {
  m, err := migrate.New(
    "github://mattes:personal-access-token@mattes/migrate_test",
    "postgres://localhost:5432/database?sslmode=enable")
  m.Steps(2)
}

```

```
1481574547_create_users_table.up.sql
1481574547_create_users_table.down.sql

docker run -v {{ migration dir }}:/migrations --network host migrate/migrate -path=/migrations/ -database postgres://localhost:5432/database up 2

migrate -source file://path/tomigrations -database postgres://localhost: 5432/database up 2

python3 -c 'import urlib.parse; print(urllib.parse.quote(input("String to encode: "), ""))'
python2 -c 'import urllib; print urllib.quote(raw_input("String to encode: "), "")'
```

```go
// https://godoc.org/github.com/golang-migrate/migrate

var (
  ErrNoChange = error.New("no change")
  ErrNilVersion = error.New("no migration")
  ErInvalidVersion = errors.New("version must be >= -1")
  ErrLocked = errors.New("database locked")
  ErrLockTimeout = error.New("timeout: can't acquire database lock")
)

var DefaultBufferSize = uint(100000)

var DefaultLockTimeout = 15 * time.Second

var DefaultPrefetchMigrations = uint(10)

func FilterCustomQuery(u *nurl.URL) *nurl.URL

type ErrDirty struct {
  Version int
}

func (e ErrDirty) Error() string

type ErrShortLimit struct {
  Short uint
}
```


