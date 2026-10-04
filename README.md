# 🎵 Spotify ETL Pipeline & Star Schema Analytics

An end-to-end Data Engineering and Analytics project that transforms raw Spotify track data into an optimized **SQLite Star Schema**, enabling advanced analytical queries (Time Series Analysis, Window Functions, and Relational Aggregations).

---

## 📌 Architecture & Data Modeling

The pipeline processes raw, unnormalized data and transforms it into a production-ready **Star Schema** designed for OLAP querying.

```mermaid
erDiagram
    fact_track }|--|| dim_artist : "artist_id"
    fact_track }|--|| dim_album : "album_id"
    bridge_artist_genre }|--|| dim_artist : "artist_id"
    bridge_artist_genre }|--|| dim_genre : "genre_id"

    dim_artist {
        INTEGER artist_id PK
        TEXT artist_name
        REAL artist_popularity
        INTEGER artist_followers
    }

    dim_album {
        TEXT album_id PK
        TEXT album_name
        TEXT album_release_date
        REAL album_total_tracks
        TEXT album_type
    }

    dim_genre {
        INTEGER genre_id PK
        TEXT genre_name
    }

    bridge_artist_genre {
        INTEGER artist_id FK
        INTEGER genre_id FK
    }

    fact_track {
        TEXT track_id PK
        TEXT track_name
        INTEGER artist_id FK
        TEXT album_id FK
        REAL track_number
        REAL track_popularity
        REAL track_duration_min
        INTEGER explicit
        INTEGER release_year
        INTEGER release_decade
    }
