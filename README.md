# Fetching Twitter Followers

This is a simple python script used to fetch a large list of followers from Twitter and write them to file.

### Getting Started

* Clone: `git clone https://github.com/ChunaraLab/Fetching-Twitter-Followers.git`
* Create config file (*see below*): `vi config.json`
* Launch script in the shell: `python fetch_followers.py`
* ... or to avoid binding the script to the current bash, use nohup and redirect output: `nohup python -u fetch_followers.py > log.out &`

### Links

* Create a new Twitter app: https://apps.twitter.com/app/new
* Generate the needed access tokens by using one of the methods described [here](https://github.com/bear/python-twitter#api) (either use the `get_access_token.py` or generate it via Twitter).
* `/followers/ids` API: https://dev.twitter.com/rest/reference/get/followers/ids

-----------------------

## Config file

You will need a `config.json` file in order to run the script.
> Here is a sample configuration:

```json
{
  "twitter": {
    "consumer_key": "...",
    "consumer_secret": "...",
    "access_token_key": "...",
    "access_token_secret": "..."
  },
  "accounts": ["someaccount", "anotherusername", "anotheryetagain", "etc"]
}

```

## python-twitter

This script uses a modified version of the twitter framework [bear/python-twitter](https://github.com/bear/python-twitter). It has been modified to fix the rate-limit issue being discussed [here](https://github.com/bear/python-twitter/issues/198) and [here](https://github.com/bear/python-twitter/issues/158).

## Converting to screen_name

Using the `/followers/ids` API allows for fetching 5,000 users every request, but in return it only gives us the User IDs and not the screen names. But we can then use the `/users/lookup` API to find out the screen names, since it will likely be on a smaller subset of users. See here: https://dev.twitter.com/rest/reference/get/users/lookup.