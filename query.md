Тут сразу приходит в голову два варианта:

1. Через `JOIN`
2. Через подзапрос и `EXISTS`

### Через `JOIN`

```sql
SELECT article.*
FROM article
LEFT JOIN comment ON article.id = comment.article_id
WHERE comment.id IS NULL;
```

Используем именно `LEFT JOIN`, потому что с `INNER JOIN` мы вообще не получим статьи без комментариев.

### Через подзапрос

```sql
SELECT *
FROM article
WHERE NOT EXISTS (
    SELECT 1
    FROM comment
    WHERE comment.article_id = article.id
);
```

`SELECT 1` в данном случае пишем, чтобы не доставать данные, т.к. они нам не нужны, нам нужно лишь наличие строк.
