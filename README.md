pyslack
==========

A Python wrapper for Slack's API

https://api.slack.com

## Installation

    pip install git+git://github.com/aneisch/pyslack.git

## Usage

Post a message into your Slack integration's `#play` channel

    >>> from pyslack import SlackClient
    >>> from pyslack import SlackClient
    >>> client.chat_post_message('#play', "testing, testing...", username='slackbot')
    {u'ok': 1, u'timestamp': u'1392000237000006'}
    
Post an 'attachment' message into your Slack integration's `#play` channel. (Follow guidlines at https://api.slack.com/docs/attachments)

    from pyslack import SlackClient
    def post_attachment(recipient, message):
        client = SlackClient('YOUR-TOKEN-HERE')
        client.chat_post_attachment(recipient, message, username='BOT', icon_emoji=":cop:")
    message = '''[
        {
            "fallback": "Required plain-text summary of the attachment.",

            "color": "#36a64f",

            "pretext": "Optional text that appears above the attachment block",

            "author_name": "Bobby Tables",
            "author_link": "http://flickr.com/bobby/",
            "author_icon": "http://flickr.com/icons/bobby.jpg",

            "title": "Slack API Documentation",
            "title_link": "https://api.slack.com/",

            "text": "Optional text that appears within the attachment",

            "fields": [
                {
                    "title": "Priority",
                    "value": "High",
                    "short": false
                }
            ],

            "image_url": "http://my-website.com/path/to/image.jpg"
        }
    ]'''
    post_attachment('#play',message)


Integrate a SlackHandler into your logging!

    >>> import logging
    >>> from pyslack import SlackHandler
    
    >>> logger = logging.getLogger('test')
    >>> logger.setLevel(logging.DEBUG)
    
    >>> handler = SlackHandler('YOUR-TOKEN-HERE', '#channel_name', username='botname')
    >>> handler.setLevel(logging.WARNING)
    >>> formatter = logging.Formatter('%(asctime)s [%(levelname)s] %(name)s (%(process)d): %(message)s')
    >>> handler.setFormatter(formatter)
    >>> logger.addHandler(handler)
    
    >>> logger.error("Oh noh!") # Will post the formatted message to channel #channel_name from user botname

## Testing

Before running the test suite, you'll need to add the required libraries to your environment. These aren't included in the main requirements.txt because they are not needed for normal operation of pyslack.

    pip install -r tests/requirements.txt
    
The tests can be run as follows:

    $ python setup.py test
