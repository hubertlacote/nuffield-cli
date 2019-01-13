# nuffield-cli

**A set of command-line to make it easier to book Nuffield Health gym classes.**

## Why ([![start with why](https://img.shields.io/badge/start%20with-why%3F-brightgreen.svg?style=flat)](http://www.ted.com/talks/simon_sinek_how_great_leaders_inspire_action))

With Nuffield Health booking system (https://www.nuffieldhealth.com/account/homepage), you usually have to book 8 days in advance at 7 am to be sure to have space in your class.

It is not ideal since:

- you need to book several times a week if you attend several classes,
- if you forget to book at 7am, the class might be full.

With nuffield-cli:

- you can book all your classes for the next few weeks in one day,
- you will be the only one not to have the 8 days limitation, so you can be the first one to book all your classes.

## Configuration

You need to find your gym id, your member id and your Auth-Token (it will expire regularly, so you will have to repeat this procedure regularly):

- Login to Nuffield Health website in Google Chrome (https://www.nuffieldhealth.com/account/homepage),
- Open Network Activity panel in Google Chrome (Ctrl + Shift + I or F12), select XHR,
- Book a class and find the XHR request to 'checkout' using Network Activity Panel,
- Copy as cURL (see instructions on https://developers.google.com/web/updates/2015/05/replay-a-network-request-in-curl),
- You should have something like this in your clipboard containing everything you need:

```bash
# Check what you have in place of YOUR_GYM_ID_HERE / YOUR_MEMBER_ID / YOUR_AUTH_TOKEN_HERE:
curl 'https://nuffield.bookingbug.com/api/v1/YOUR_GYM_ID_HERE/basket/checkout' -H 'Origin: https://www.nuffieldhealth.com' -H 'App-Key: f0bc4f65f4fbfe7b4b3b7264b655f5eb' -H 'Accept-Language: en-GB,en;q=0.9,en-US;q=0.8,fr;q=0.7' -H 'App-Id: f6b16c23' -H 'Accept-Encoding: gzip, deflate, br' -H 'Connection: keep-alive' -H 'Pragma: no-cache' -H 'User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/65.0.3325.181 Safari/537.36' -H 'Content-Type: application/json' -H 'Auth-Token: YOUR_AUTH_TOKEN_HERE' -H 'Accept: application/hal+json,application/json' -H 'Cache-Control: no-cache' -H 'Referer: https://www.nuffieldhealth.com/gyms/city/timetable' -H 'DNT: 1' --data-binary '{"client":{"id":YOUR_MEMBER_ID}}' --compressed
```

## Requirements

```bash
# Install jq (Command-line JSON processor)
sudo apt install jq
```

## Usage

```bash
# List all the classes available to book on 01/01/2019
./list-classes -g 1234 -d "2019-01-01" -b

# Book the Yoga class at 06:35 on 01/01/2019
./list-classes -g 1234 -d "2019-01-01" -b | ./filter-classes -n "YOGA" -t "06:35" | ./book-class -a "AnUjfgrTyuihfTgjklMkdd" -g 1234 -m 123456

# Book any Yoga class on 01/01/2019
./list-classes -g 1234 -d "2019-01-01" -b | ./filter-classes -n "YOGA" | ./book-class -a "AnUjfgrTyuihfTgjklMkdd" -g 1234 -m 123456
```
