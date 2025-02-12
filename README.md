# Youtube Music Scrobbler

The YTMusic Last.fm Scrobbler is a Python script that allows you to fetch
your YouTube Music listening history from the last 24 hours and scrobble
it to Last.fm.

## Setup

I recommend using [uv](https://docs.astral.sh/uv/) for this project.

1. Clone or download the repository to your local machine.

2. Create a set of credentials through Google Cloud Console as described
[here](https://ytmusicapi.readthedocs.io/en/stable/setup/oauth.html).

3. Create an API key and secret for Last.fm
[here](https://www.last.fm/api/account/create).

4. Create a `.env` file in the project's root directory with the following
information:

```sh
LAST_FM_API=...
LAST_FM_API_SECRET=...
GOOGLE_CLIENT_ID=...
GOOGLE_CLIENT_SECRET=...
```

5. Use `ytmusicapi` to authenticate with Youtube Music by running

```sh
uv run ytmusicapi oauth
```

6. Now you can start the script with

```sh
uv run start.py
```

### Using SQLite for tracking scrobbled songs

The YTMusic Last.fm Scrobbler uses a SQLite database to keep track of the
songs that have already been scrobbled to Last.fm. This prevents the same
songs from being repeatedly sent as scrobbles in subsequent runs of the
script.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE)
file for more information.

