# Youtube Music Scrobbler

The YTMusic Last.fm Scrobbler is a Python script that allows you to fetch
your YouTube Music listening history from the last 24 hours and scrobble
it to Last.fm. With the added automation, you can now run the script automatically using GitHub Actions. This means your listening history will be fetched and scrobbled to Last.fm on a schedule, without needing to run the script manually on your local machine.

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

## Automation

1. Fork this repository (or clone if you want it private)

2. Run the script once locally to retrieve your Last.fm session key:

```sh
uv run start.py
```

This will generate oauth.json and output your Last.fm session key, which you’ll need for automation.

3. Add the following secrets under "Settings > Secrets and Variables > Actions > Repository Secrets" in your GitHub repository:

```sh
LAST_FM_API=...
LAST_FM_API_SECRET=...
GOOGLE_CLIENT_ID=...
GOOGLE_CLIENT_SECRET=...
LASTFM_SESSION=...
OAUTH_JSON=...  (Paste the entire contents of oauth.json as a single secret)
```

4. Enable GitHub Actions in your repository settings. Once set up, GitHub Actions will run the script daily at 1:00 AM UTC or manually via the “Run workflow” button.

Note: running this workflow on GitHub’s servers counts toward your GitHub Actions usage limits. If you fork this repository or enable the workflow on your own repo, be aware that excessive runs may consume your free GitHub Actions minutes or lead to rate limits.

### Using SQLite for tracking scrobbled songs

The YTMusic Last.fm Scrobbler uses a SQLite database to keep track of the
songs that have already been scrobbled to Last.fm. This prevents the same
songs from being repeatedly sent as scrobbles in subsequent runs of the
script.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE)
file for more information.

