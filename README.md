[![Build Status](https://travis-ci.org/clem16/Sonarr-MakeLinks.svg?branch=master)](https://travis-ci.org/clem16/Sonarr-MakeLinks)
[![GitHub version](https://badge.fury.io/gh/clem16%2FSonarr-MakeLinks.svg)](https://badge.fury.io/gh/clem16%2FSonarr-MakeLinks)

Sonarr-MakeLinks

Sonarr::MakeLinks is used to automate the creation of hard linked directories using data from Sonarr for use in Plex Media Player.

The Senario is this:

- Collection of Television shows tracked by Sonarr.
- All shows are on one filesystem. (Script doesn't support multiple filesystems yet.)
- When Sonarr::MakeLinks is run it querys Sonarr through an api call and does the following things.
-- Retrieves a list of every show in the Sonarr database.
-- Checks the status of the show. ex. Continuing or Ended.
-- Checks to see if all episodes of the show are available.
-- Based on the above information it sorts the shows into three categories. Continuing, Ended, Incomplete.

- Continuing - These are shows that are currently on air.
- Ended - These shows are ended, and all episodes are available on disk.
- Incomplete - These shows are ended, the local disk is missing episodes.

- There are several bits of information this module needs to be provided with.

SONARR_API_KEY: Can be found in the web interface of sonarr.
IP: The ip address of the server running sonarr.
PORT: The port number of sonarr.
DIR: This is the directory that all the hard links will be created in.
- You will have to create the sub folders in this directory.
- The folders need to be called: continuing ended incomplete

-- The direcotry stucture should look like this.

-- plex-links
	continuing
	ended
	incomplete

-- NOTE: Due to the nature of hard links, this folder needs to be on the same filesystem as the origional media.

There are several reasons why this script is useful.
1. When browsing Plex shows are kept in neat categories, old shows that are off air are easilly found in Ended yet they are kept out of the way of new.
2. Because of the hard links, if media files are deleted in Plex only the hard links are deleted. Not the archived files. 
-- This can be useful in a number of situations. 
-- -- For example, if anyone decides they dislike a show in plex and clicks delete...
-- -- Depending on CRON settings, the show will automatically pop back up in plex again.

The operating system this module is developed and used on is FreeBSD, anything else is untested.


EXAMPLE:

#!/usr/bin/env perl
use Sonarr::MakeLinks
Sonarr::MakeLinks::run_api_call("SONARR_API_KEY", "127.0.0.1", "8989", "/tv/plex-links");

ONE LINER EXAMPLE:
perl -MSonarr::MakeLinks -e "Sonarr::MakeLinks::run_api_call('API_KEY', '127.0.0.1', '8989', '/tv/plex-links');"

INSTALLATION

To install this module, run the following commands:

	perl Makefile.PL
	make
	make test
	make install

SUPPORT AND DOCUMENTATION

After installing, you can find documentation for this module with the
perldoc command.

    perldoc Sonarr::MakeLinks

You can also look for information at:

    RT, CPAN's request tracker (report bugs here)
        https://rt.cpan.org/NoAuth/Bugs.html?Dist=Sonarr-MakeLinks

    AnnoCPAN, Annotated CPAN documentation
        http://annocpan.org/dist/Sonarr-MakeLinks

    CPAN Ratings
        https://cpanratings.perl.org/d/Sonarr-MakeLinks

    Search CPAN
        https://metacpan.org/release/Sonarr-MakeLinks


LICENSE AND COPYRIGHT

The MIT License (MIT)

This software is Copyright (c) 2019 by Clem Morton.

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
