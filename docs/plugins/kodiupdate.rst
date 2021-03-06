KodiUpdate Plugin
=================

The ``kodiupdate`` plugin lets you automatically update `Kodi`_'s music
library whenever you change your beets library or, alternatively, every
time a new album is imported.

To use ``kodiupdate`` plugin, enable it in your configuration
(see :ref:`using-plugins`).
Then, you'll want to configure the specifics of your Kodi host.
You can do that using a ``kodi:`` section in your ``config.yaml``,
which looks like this::

    kodi:
        host: localhost
        port: 8080
        user: kodi
        pwd: kodi

With the basic configuration settings above, the ``kodiupdate`` plugin
will notify Kodi to scan your entire music library after any changes to
the beets database. For importing albums into large music libraries you
may prefer to have Kodi only scan the directory where each album was
imported. To enable this behavior, add a `kodi_dir` setting, which reflects
the Kodi `Music` directory found in Kodi's sources.xml file, and a `library`
setting, which indicates exactly how much of the beets library album
path should be removed before appending the remaining portion to
the `kodi_dir`:

    kodi:
        host: localhost
        port: 8080
        user: kodi
        pwd: kodi
        kodi_dir: nfs://myserver.local/music/library/
        library: /home/music/library/

`kodi_dir` should be the Kodi Music path found in .kodi/userdata/sources.xml.
`library` should be the path to your beets library.

With this configuration, after every album import, the `library` path is stripped
from the imported album's path and the remaining part is added to the `kodi_dir`.
Kodi is then asked to scan the resulting directory.

To use the ``kodiupdate`` plugin you need to install the `requests`_ library with::

    pip install requests

You'll also need to enable JSON-RPC in Kodi in order the use the plugin.
In Kodi's interface, navigate to System/Settings/Network/Services and choose "Allow control of Kodi via HTTP."

With that all in place, you'll see beets send the "update" command to your Kodi
host every time you change your beets library.

.. _Kodi: http://kodi.tv/
.. _requests: http://docs.python-requests.org/en/latest/

Configuration
-------------

The available options under the ``kodi:`` section are:

- **host**: The Kodi host name.
  Default: ``localhost``
- **port**: The Kodi host port.
  Default: 8080
- **user**: The Kodi host user.
  Default: ``kodi``
- **pwd**: The Kodi host password.
  Default: ``kodi``
- **kodi_dir**: The Kodi Music path.
  Default: none
- **library**: The beets library directory.
  Default: none
