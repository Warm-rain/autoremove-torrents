Auto Remove Torrents
======================
|PyPI| |TravisCI| |Coverage| |Codacy| |MIT|

This program can help you to remove your torrents. Now you don't need to worry about your disk space - according to your strategies, the program will check each torrent if it satisfies the remove condition; If so, delete it automatically.

This program supports qBittorrent/Transmission/μTorrent. If you like, star it :sparkles: :)

Readme version in other languages: `简体中文`_.

.. _简体中文: https://github.com/jerrymakesjelly/autoremove-torrents/blob/master/README-cn.rst

.. |Codacy| image:: https://api.codacy.com/project/badge/Grade/6e5509ecb4714ed697c65f35d71cff65
    :target: https://www.codacy.com/app/jerrymakesjelly/autoremove-torrents?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=jerrymakesjelly/autoremove-torrents&amp;utm_campaign=Badge_Grade
.. |TravisCI| image:: https://www.travis-ci.org/jerrymakesjelly/autoremove-torrents.svg?branch=master
   :target: https://www.travis-ci.org/jerrymakesjelly/autoremove-torrents
.. |Coverage| image:: https://api.codacy.com/project/badge/Coverage/6e5509ecb4714ed697c65f35d71cff65    
   :target: https://www.codacy.com/app/jerrymakesjelly/autoremove-torrents?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=jerrymakesjelly/autoremove-torrents&amp;utm_campaign=Badge_Coverage
.. |MIT| image:: https://img.shields.io/badge/license-MIT-blue.svg
   :target: https://github.com/jerrymakesjelly/autoremove-torrents/blob/master/LICENSE
.. |PyPI| image:: https://badge.fury.io/py/autoremove-torrents.svg
    :target: https://badge.fury.io/py/autoremove-torrents

Requirements
-------------
* Python 3

That's all. It's a simple but smart program.


Quick Start
-------------
Installation
+++++++++++++++++++
Install from pip
^^^^^^^^^^^^^^^^^
::

    pip install autoremove-torrents

or

Install from GitHub
^^^^^^^^^^^^^^^^^^^^
::

    git clone https://github.com/jerrymakesjelly/autoremove-torrents.git
    cd autoremove-torrents
    python3 setup.py install


Write your configuration file
++++++++++++++++++++++++++++++
In order to satisfactory your needs, you have to learn how to write a configuration file. 

You can put the configuration file anywhere on your disk. The autoremove-torrents looks for ``config.yml`` in the Shell's current working directory::

    vim ./config.yml


The grammar is quite easy, for example::

    my_task:
      client: qbittorrent
      host: http://127.0.0.1
      username: admin
      password: adminadmin
      strategies:
        my_strategy:
          categories:
            - IPT
          seeding_time: 1209600
          ratio: 1
      delete_data: true


The program will delete those torrents whose categories are ``IPT``, seeding time is above 1209600 seconds **or** ratio is greater than 1. Visit `Wiki`_ to learn more.

.. _Wiki: https://github.com/jerrymakesjelly/autoremove-torrents/wiki

Run
++++
::

    autoremove-torrents

If you just want to see which torrents can be removed but don't want to really remove them, use ``--view`` command line argument.


Setting up scheduled tasks
-----------------------------
If you want to check whether there is any torrent can be removed every 15 minutes, the crontab can help you. Look at the example::

    crontab -e

And then, add a line at the end of the file (please confirm the path of the autoremove-torrents and your program)::

*/15 * * * * /usr/bin/autoremove-torrents --conf=/home/jerrymakesjelly/autoremove-torrents/config.yml --log=/home/jerrymakesjelly/autoremove-torrents/logs

The ``--conf`` indicates the path to the configuration file.
The ``--log`` argument specifies the path to store the log files (Must be existed).

Screenshot
-----------
|Screenshot|

.. |Screenshot| image:: https://user-images.githubusercontent.com/6760674/40576720-a78097fe-612d-11e8-9dda-8aac0c5011a2.png

Changelog
----------
**Wed, 17 Apr 2019**: Version 1.3.0.

* Fixed bug: Program gets stuck when there are a lot of torrents in qBittorrent client (`Issue #22 <https://github.com/jerrymakesjelly/autoremove-torrents/issues/22>`_).
* Fixed bug: Duplicated logging in status filter.
* Log system was updated:
    - Log path can be specified (Use ``--log`` argument, e.g. ``--log=/home/jerrymakesjelly/logs``) (`Issue #23 <https://github.com/jerrymakesjelly/autoremove-torrents/issues/23>`_).
    - Logs are stored in different files by day (Format: ``autoremove.%Y-%m-%d.log``).
* Changed the word ``seed`` to ``torrent`` (`Issue #25 <https://github.com/jerrymakesjelly/autoremove-torrents/issues/25>`_).
* Removed uncessary debug messages.

**Mon, 10 Jan 2019**: Version 1.2.5.

* Fixed bug: Incorrect number of torrents in multiple strategies (`Issue #10 <https://github.com/jerrymakesjelly/autoremove-torrents/issues/10>`_, thanks to @momokoo for the report and PR).
* Fixed bug: Incorrect number of torrents in qBittorrent (`Issue #13 <https://github.com/jerrymakesjelly/autoremove-torrents/issues/13>`_).

**Thu, 31 May 2018**: Version 1.2.4.

* Fixed startup failure.

**Wed, 30 May 2018**: Version 1.2.3. Added new features.

* Allowed to use environment variables to specify *host*, *username* and *password*.
* Allowed *username* and *password* to be empty (or one of them is empty) to log in a WebUI without username and/or password.
* Now the program won't quit directly when a task goes failed.

**Sun, 27 May 2018**: Version 1.2.2. Added new features :smile:

* Added new filter: Torrent Status
* Added new condition: Maximum number of torrents

**Sat, 26 May 2018**: Version 1.2.1. Fixed issue in *setup.py*.

**Sat, 26 May 2018**: Version 1.2.0. Refactoring was completed, and was published to PyPI.

* New features will be added soon.
* Now we can install it via *pip*.

**Mon, 14 May 2018**: Version 1.1.0. Created *setup.py*.

You can now use the *autoremove-torrents* command directly instead of *python3 main.py*.

**Wed, 28 Mar 2018**: (Correct document) The *delete_data* field shouldn't be indented.

**Thu, 22 Mar 2018**: First version :bowtie:

TODO List
-----------
Depend on users' feedback.

* Support Deluge and rtorrent in the future

* Add remove condition: Disk free space

* Add remove condition: Max/Min average UL/DL speed

If you have any problem, please submit `issues`_.

.. _issues: https://github.com/jerrymakesjelly/autoremove-torrents/issues

