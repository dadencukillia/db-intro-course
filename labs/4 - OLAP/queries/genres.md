```SQL
SELECT 
  genres.genre_type,
  COUNT(animes.anime_id) AS anime_count
FROM genres
LEFT JOIN animes ON genres.anime_id = animes.anime_id
GROUP BY genres.genre_type
ORDER BY anime_count DESC, genres.genre_type DESC;
```
```SQL

```