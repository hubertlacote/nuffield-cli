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

You need to log in to Nuffield Health in Google Chrome and extract your member id and Auth-Token:

- Open Network Activity panel in Google Chrome (Ctrl + Shift + I or F12), select XHR,
- Login to Nuffield Health website (https://www.nuffieldhealth.com/account/homepage) and possibly book a class,
- Follow the instructions on https://developers.google.com/web/updates/2015/05/replay-a-network-request-in-curl

The Auth-Token expires so you will have to repeat the procedure.

## Requirements

- Install jq (Command-line JSON processor)

```bash
sudo apt install jq
```

## Usage

```bash
# List all the classes available to book on 01/01/2019
./list-classes -d "2019-01-01" -b

# Book the Yoga class at 06:35 on 01/01/2019
./list-classes -d "2019-01-01" -b | ./filter-classes -n "YOGA" -t "06:35" | ./filter-classes -a "AnUjfgrTyuihfTgjklMkdd" -m 123456

# Book any Yoga class on 01/01/2019
./list-classes -d "2019-01-01" -b | ./filter-classes -n "YOGA" | ./filter-classes -a "AnUjfgrTyuihfTgjklMkdd" -m 123456
```
