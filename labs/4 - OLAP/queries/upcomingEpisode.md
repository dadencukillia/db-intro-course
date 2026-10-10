```SQL
CREATE TABLE IF NOT EXISTS public.upcoming_episodes(
  anime_id UUID NOT NULL REFERENCES public.animes(anime_id) ON DELETE CASCADE,
  episode_name TEXT NOT NULL CHECK(length(trim(episode_name)) > 0),
  episode_date TIMESTAMPTZ NOT NULL DEFAULT now(),

  PRIMARY KEY(anime_id, episode_name)
);

CREATE INDEX IF NOT EXISTS idx_upcoming_episode_date ON public.upcoming_episodes(episode_date ASC);
```

```SQL
SELECT 
  animes.title_ua,
  animes.title_en,
  count(upcoming_episodes.episode_name) AS upcoming_episodes_count
FROM animes, upcoming_episodes
WHERE 
  animes.anime_id = upcoming_episodes.anime_id AND
  animes.available = TRUE AND 
  upcoming_episodes.episode_date::date = now()::date
GROUP BY animes.title_ua, animes.title_en;
```
```SQL
SELECT 
    anime_id,
    count(episode_name) AS upcoming_episodes_count
FROM public.upcoming_episodes
GROUP BY anime_id;
```
```SQL
SELECT 
    anime_id,
    count(episode_name) AS episodes_in_schedule
FROM public.upcoming_episodes
GROUP BY anime_id
HAVING count(episode_name) > 1;
```