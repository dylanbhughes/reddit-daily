# Reddit Daily

My implementation of [ferold/reddit-weekly](https://github.com/feroldi/reddit-weekly).

I'm using [prefect](https://github.com/PrefectHQ/prefect) to:

- elegantly handle task failures
- retry HTTP requests
- notify you of email failures
- run this on a schedule

## Setup

Firstly, go to [reddit apps](https://www.reddit.com/prefs/apps/) and
register a new app. You'll need the personal use script id,
and the secret. In case you aren't sure about the authentication
process, [read about it here](https://praw.readthedocs.io/en/latest/getting_started/authentication.html).
Next step is to create an email account. Currently, the script is
using Gmail to log in, but there are plans (#3) to provide
a way to plug-in a back-end that takes care of the emailing part.

Then, you need to generate your reddit's refresh token.
The easiest way is to run [this](https://praw.readthedocs.io/en/latest/tutorials/refresh_token.html#refresh-token)
script. This token is used for authentication to get a reddit account's subreddits.

1. Add the relevant secrets to `~/.prefect/config.toml`, see [the prefect docs](https://docs.prefect.io/guide/cloud_concepts/secrets.html) for more info

You'll need an app email password for your email address. Here's how to get one for [gmail](https://support.google.com/accounts/answer/185833?hl=en).

```toml
# config.toml
[cloud]
use_local_secrets = true

[context.secrets]
REDDIT_DAILY_EMAIL = "place email here"
REDDIT_DAILY_EMAIL_PASSWORD = "place email app password here"
REDDIT_DAILY_REFRESH_TOKEN = "place app refresh token here"
REDDIT_DAILY_APP_ID = "reddit app id goes here"
REDDIT_DAILY_APP_SECRET = "reddit app secret goes here"
```

## Running Locally

If you'd like to test this script locally, first install dependencies using [pip](https://pypi.org/project/pip/).

```bash
pip install -r requirements.txt
```

To run the flow, we can use an [ipython](https://ipython.org/) session.

```bash
ipython -i reddit_daily.py
```

Once the session is open:

```bash
In [1]: flow.run()
```

## What it looks like

Screenshot of newsletter from r/programming:

![reddit-weekly](http://i.imgur.com/QEyqKYs.png)

## License

This project is licensed under the MIT license. See LICENSE.
