# Lib16 RSS Builder for PHP 7
A library for creating RSS feeds written in PHP 7.


## Installation with Composer
This package is available on [packagist](https://packagist.org/packages/lib16/rss), so you can use [Composer](https://getcomposer.org) to install it.If applicable add the following to your project's `composer.json` file:

```json
{
    "minimum-stability": "dev",
    "prefer-stable" : true
}
```
Run the following command in your shell:

```
composer require lib16/rss:dev-master
```

## Basic Usage
Example markup is taken from [en.wikipedia.org/wiki/Rss](https://en.wikipedia.org/wiki/Rss)

```php
<?php

require_once 'vendor/autoload.php';

use Lib16\Calendar\DateTime;
use Lib16\RSS\Channel;
use Lib16\RSS\RssMarkup;

$channel = Channel::create('RSS Title',
        'This is an example of an RSS feed',
        'http://www.example.com/main.html');
$channel
        ->pubDate(DateTime::create('2010-09-06 00:01 +0'))
        ->lastBuildDate(DateTime::create('2009-09-06 16:20 +0'))
        ->ttl(1800);

$channel
        ->item('Example entry',
                'Here is some text containing an interesting description.',
                'http://www.example.com/blog/post/1')
        ->guid('7bd204c6-1655-4c27-aeee-53f933c5395f', true)
        ->pubDate(DateTime::create('2009-09-06 16:20 +0'));

RssMarkup::headerfields();
print $channel;
```
… generates the following output:

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<rss version="2.0">
    <channel>
        <title>RSS Title</title>
        <description>This is an example of an RSS feed</description>
        <link>http://www.example.com/main.html</link>
        <pubDate>Mon, 06 Sep 2010 00:01:00 +0000</pubDate>
        <lastBuildDate>Sun, 06 Sep 2009 16:20:00 +0000</lastBuildDate>
        <ttl>1800</ttl>
        <item>
            <title>Example entry</title>
            <description>Here is some text containing an interesting description.</description>
            <link>http://www.example.com/blog/post/1</link>
            <guid isPermaLink="true">7bd204c6-1655-4c27-aeee-53f933c5395f</guid>
            <pubDate>Sun, 06 Sep 2009 16:20:00 +0000</pubDate>
        </item>
    </channel>
</rss>
```