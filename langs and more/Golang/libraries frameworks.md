- [[#libraries|libraries]]
	- [[#libraries#логирование:|логирование:]]
	- [[#libraries#БД|БД]]
	- [[#libraries#конфигурирование|конфигурирование]]
- [[#frameworks|frameworks]]
	- [[#frameworks#web|web]]
- [[#db drivers|db drivers]]
	- [[#db drivers#postgresql|postgresql]]


## 1_libraries
### логирование:

- [logrus](github.com/sirupsen/logrus)

- slog (стандартная библиотека Go с 1.21)

- zerolog

- zap

### БД

- [sqlx](github.com/jmoiron/sqlx)
sqlx — это библиотека, которая предоставляет набор расширений для стандартной `database/sql`библиотеки go

### конфигурирование

- [viper](github.com/spf13/viper)

глобал переменные:

- [godotenv](github.com/joho/godotenv)

### токены

- [jwt](github.com/dgrijalva/jwt-go)

## 2_frameworks

### web

- [Gin](github.com/gin-gonic/gin)

## 3_db drivers

### postgresql

- [pq](github.com/lib/pq)
pq - Чистый драйвер postgres для database/sql пакета Go.

