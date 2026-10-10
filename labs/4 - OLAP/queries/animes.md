```SQL
CREATE TYPE public.anime_format_enum AS ENUM('tv', 'ova', 'ona', 'movie', 'special', 'music', 'other');
CREATE TYPE public.anime_status_enum AS ENUM('upcoming', 'ongoing', 'cancelled', 'finished');
CREATE TYPE public.mpaa_rating_enum AS ENUM('g', 'pg', 'pg13', 'r', 'nc17');

CREATE TABLE IF NOT EXISTS public.animes(
  anime_id UUID PRIMARY KEY DEFAULT uuidv7(),
  slug TEXT NOT NULL UNIQUE,
  title_ua TEXT NOT NULL DEFAULT '',
  title_en TEXT NOT NULL DEFAULT '',
  title_original TEXT NOT NULL DEFAULT '',
  anime_description TEXT NOT NULL DEFAULT '',
  cover_url TEXT NOT NULL DEFAULT '',
  production_studio TEXT NOT NULL DEFAULT '',
  mal_id BIGINT,
  anilist_id BIGINT,
  hikka_id TEXT,
  imdb_id TEXT,
  year_released SMALLINT CHECK(year_released >= 1900),
  avg_episode_duration SMALLINT NOT NULL DEFAULT 0 CHECK(avg_episode_duration >= 0),
  episodes_count SMALLINT NOT NULL DEFAULT 0 CHECK(episodes_count >= 0),
  age_restriction mpaa_rating_enum,
  anime_status anime_status_enum,
  anime_format anime_format_enum NOT NULL DEFAULT 'tv',
  available BOOLEAN NOT NULL DEFAULT TRUE
);

CREATE INDEX IF NOT EXISTS idx_anime_available ON public.animes(available);
```

```SQL
SELECT 
    anime_status,
    count(*) AS total_count_animes
FROM public.animes
WHERE 
    available = TRUE
    AND anime_status IS NOT NULL
GROUP BY anime_status;
```

```SQL
SELECT episode_count,
    count(*) AS total_count_episodes
FROM public.animes, episodes
WHERE 
    available = TRUE
    AND episodes.anime_id = animes.anime_id
GROUP BY episode_count;
```

SELECT 
  production_studio,
  DISTINCT COUNT(anime_id) AS total_animes,
  SUM(episodes_count) AS total_episodes,
  ROUND(AVG(avg_episode_duration), 1) AS avg_duration
FROM animes
WHERE production_studio IS NOT NULL
GROUP BY production_studio
ORDER BY total_episodes DESC;
