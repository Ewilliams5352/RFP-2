# The Million Playlist Dataset

(Documentation updated Aug 5, 2020)

The Million Playlist Dataset contains 1,000,000 playlists created by
users on the Spotify platform. It can be used by researchers interested
in exploring how to improve the music listening experience.

## What's in the Million Playlist Dataset (MPD)

The MPD contains a million user-generated playlists. These playlists
were created during the period of January 2010 through October 2017.
Each playlist in the MPD contains a playlist title, the track list
(including track metadata) editing information (last edit time,
number of playlist edits) and other miscellaneous information
about the playlist. See the **Detailed
Description** section for more details.

## License

Usage of the Million Playlist Dataset is subject to these
[license terms](https://www.aicrowd.com/challenges/spotify-million-playlist-dataset-challenge/challenge_rules)

## Citing the Million Playlist Dataset

To use this dataset, please cite the following [paper](https://dl.acm.org/doi/abs/10.1145/3240323.3240342):

_Ching-Wei Chen, Paul Lamere, Markus Schedl, and Hamed Zamani. Recsys Challenge 2018: Automatic Music Playlist Continuation. In Proceedings of the 12th ACM Conference on Recommender Systems (RecSys ’18), 2018._

## Getting the dataset

The dataset is available at [https://www.aicrowd.com/challenges/spotify-million-playlist-dataset-challenge](https://www.aicrowd.com/challenges/spotify-million-playlist-dataset-challenge)

## Verifying your dataset

You can validate the dataset by checking the md5 hashes of the data. From the top level directory of the MPD:

    % md5sum -c md5sums

This should print out OK for each of the 1,000 slice files in the dataset.

You can also compute a number of statistics for the dataset as follows:

    % python src/stats.py data

The output of this program should match what is in 'stats.txt'. Depending on how
fast your computer is, stats.py can take 30 minutes or more to run.

## Detailed description

The Million Playlist Dataset consists of 1,000 slice files. These files have the naming convention of:

mpd.slice._STARTING_PLAYLIST_ID\_-_ENDING_PLAYLIST_ID_.json

For example, the first 1,000 playlists in the MPD are in a file called
`mpd.slice.0-999.json` and the last 1,000 playlists are in a file called
`mpd.slice.999000-999999.json`.

Each slice file is a JSON dictionary with two fields:
_info_ and _playlists_.

### `info` Field

The info field is a dictionary that contains general information about the particular slice:

- **slice** - the range of slices that in in this particular file - such as 0-999
- **_version_** - - the current version of the MPD (which should be v1)
- **_description_** - a description of the MPD
- **_license_** - licensing info for the MPD
- **_generated_on_** - a timestamp indicating when the slice was generated.

### `playlists` field

This is an array that typically contains 1,000 playlists. Each playlist is a dictionary that contains the following fields:

- **_pid_** - integer - playlist id - the MPD ID of this playlist. This is an integer between 0 and 999,999.
- **_name_** - string - the name of the playlist
- **_description_** - optional string - if present, the description given to the playlist. Note that user-provided playlist descrptions are a relatively new feature of Spotify, so most playlists do not have descriptions.
- **_modified_at_** - seconds - timestamp (in seconds since the epoch) when this playlist was last updated. Times are rounded to midnight GMT of the date when the playlist was last updated.
- **_num_artists_** - the total number of unique artists for the tracks in the playlist.
- **_num_albums_** - the number of unique albums for the tracks in the playlist
- **_num_tracks_** - the number of tracks in the playlist
- **_num_followers_** - the number of followers this playlist had at the time the MPD was created. (Note that the follower count does not including the playlist creator)
- **_num_edits_** - the number of separate editing sessions. Tracks added in a two hour window are considered to be added in a single editing session.
- **_duration_ms_** - the total duration of all the tracks in the playlist (in milliseconds)
- **_collaborative_** - boolean - if true, the playlist is a collaborative playlist. Multiple users may contribute tracks to a collaborative playlist.
- **_tracks_** - an array of information about each track in the playlist. Each element in the array is a dictionary with the following fields:
  - **_track_name_** - the name of the track
  - **_track_uri_** - the Spotify URI of the track
  - **_album_name_** - the name of the track's album
  - **_album_uri_** - the Spotify URI of the album
  - **_artist_name_** - the name of the track's primary artist
  - **_artist_uri_** - the Spotify URI of track's primary artist
  - **_duration_ms_** - the duration of the track in milliseconds
  - **_pos_** - the position of the track in the playlist (zero-based)

Here's an example of a typical playlist entry:

        {
            "name": "musical",
            "collaborative": "false",
            "pid": 5,
            "modified_at": 1493424000,
            "num_albums": 7,
            "num_tracks": 12,
            "num_followers": 1,
            "num_edits": 2,
            "duration_ms": 2657366,
            "num_artists": 6,
            "tracks": [
                {
                    "pos": 0,
                    "artist_name": "Degiheugi",
                    "track_uri": "spotify:track:7vqa3sDmtEaVJ2gcvxtRID",
                    "artist_uri": "spotify:artist:3V2paBXEoZIAhfZRJmo2jL",
                    "track_name": "Finalement",
                    "album_uri": "spotify:album:2KrRMJ9z7Xjoz1Az4O6UML",
                    "duration_ms": 166264,
                    "album_name": "Dancing Chords and Fireflies"
                },
                {
                    "pos": 1,
                    "artist_name": "Degiheugi",
                    "track_uri": "spotify:track:23EOmJivOZ88WJPUbIPjh6",
                    "artist_uri": "spotify:artist:3V2paBXEoZIAhfZRJmo2jL",
                    "track_name": "Betty",
                    "album_uri": "spotify:album:3lUSlvjUoHNA8IkNTqURqd",
                    "duration_ms": 235534,
                    "album_name": "Endless Smile"
                },
                {
                    "pos": 2,
                    "artist_name": "Degiheugi",
                    "track_uri": "spotify:track:1vaffTCJxkyqeJY7zF9a55",
                    "artist_uri": "spotify:artist:3V2paBXEoZIAhfZRJmo2jL",
                    "track_name": "Some Beat in My Head",
                    "album_uri": "spotify:album:2KrRMJ9z7Xjoz1Az4O6UML",
                    "duration_ms": 268050,
                    "album_name": "Dancing Chords and Fireflies"
                },
                // 8 tracks omitted
                {
                    "pos": 11,
                    "artist_name": "Mo' Horizons",
                    "track_uri": "spotify:track:7iwx00eBzeSSSy6xfESyWN",
                    "artist_uri": "spotify:artist:3tuX54dqgS8LsGUvNzgrpP",
                    "track_name": "Fever 99\u00b0",
                    "album_uri": "spotify:album:2Fg1t2tyOSGWkVYHlFfXVf",
                    "duration_ms": 364320,
                    "album_name": "Come Touch The Sun"
                }
            ],

        }

## Tools

There are some tools in the src/ directory that you can use with the dataset:

- check.py - checks to se that the MPD is correct
- deeper_stats.py - shows deep stats for the MPD
- descriptions.py - surfaces the most common descriptions in the MPD
- print.py - prints the full MPD
- show.py - shows playlists by id or id range in the MPD
- stats.py - iterates over the million playlist dataset and outputs info about what is in there.

## How was the dataset built

The Million Playist Dataset is created by sampling playlists from the billions of playlists that Spotify users have created over the years. Playlists that meet the following criteria are selected at random:

- Created by a user that resides in the United States and is at least 13 years old
- Was a public playlist at the time the MPD was generated
- Contains at least 5 tracks
- Contains no more than 250 tracks
- Contains at least 3 unique artists
- Contains at least 2 unique albums
- Has no local tracks (local tracks are non-Spotify tracks that a user has on their local device)
- Has at least one follower (not including the creator)
- Was created after January 1, 2010 and before December 1, 2017
- Does not have an offensive title
- Does not have an adult-oriented title if the playlist was created by a user under 18 years of age

Additionally, some playlists have been modified as follows:

- Potentially offensive playlist descriptions are removed
- Tracks added on or after November 1, 2017 are removed

Playlists are sampled randomly, for the most part, but with some dithering to disguise the true distribution of playlists within Spotify. [Paper tracks](https://en.wikipedia.org/wiki/Fictitious_entry) may be added to some playlists to help us identify improper/unlicensed use of the dataset.

## Overall demographics of users contributing to the MPD

### Gender

- Male: 45%
- Female: 54%
- Unspecified: 0.5%
- Nonbinary: 0.5%

### Age

- 13-17: 10%
- 18-24: 43%
- 25-34: 31%
- 35-44: 9%
- 45-54: 4%
- 55+: 3%

### Country

- US: 100%

## Who built the dataset

The million playlist dataset was built by the following researchers @ Spotify:

- Cedric De Boom
- Paul Lamere
- Ching-Wei Chen
- Ben Carterette
- Christophe Charbuillet
- Jean Garcia-Gathright
- James Kirk
- James McInerney
- Vidhya Murali
- Hugh Rawlinson
- Sravana Reddy
- Marc Romejin
- Romain Yon
- Yu Zhao
