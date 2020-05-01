# DNF plugin for detecting local mirrors



## Installation

1. Set up a local mirror of dnf repositories as desired, for example under http://mirror.local/fedora/ and http://mirror.local/fedora/, mirroring the 'fedora' and 'fedora-updates' repositories
2. Clone this git repository
3. Copy the file src/local-mirror-detection.py into the appropriate directory, e.g. /usr/lib/python3.7/site-packages/dnf-plugins/local-mirror-detection.py for Fedora 31

4. Create a file 'repos.json' containing a description of your locally mirrored repository:
   ```
   {"fedora": {"url": "http://mirror.local/fedora/$releasever/Everything/$basearch/os/"},
    "updates": {"url": "http://mirror.local/updates/$releasever/Everything/$basearch/"}}
   ```
5. Serve the file 'repos.json' under 'http://mirror.local/repos.json'
6. Create a configuration file /etc/dnf/plugins/local-mirror-detection.conf with the following content:
   ```
   [main]
   local_mirror_url=http://mirror.local/repos.json
   ```
7. Run dnf and you should that your local mirror is detected and used when it is available:
   ```
   Local mirror url: http://mirror.local/repos.json
   Local mirror available
   Last metadata expiration check: 0:02:34 ago on Fr 01. Mee 2020 16:59:13.
   Dependencies resolved.
   ===================================================================================================================================================================================================================================================
   Package                                                            Architecture                                     Version                                                               Repository                                         Size
   ===================================================================================================================================================================================================================================================
   Upgrading:
    cldr-emoji-annotation                                              noarch                                           36.12.120200305_0-1.fc31                                              updates                                           4.7 M
    cups                                                               x86_64                                           1:2.2.12-8.fc31                                                       updates                                           1.4 M

   Transaction Summary
   ===================================================================================================================================================================================================================================================
   Upgrade  2 Packages

   Total size: 6.1 M
   Total download size: 6.1 M
   Is this ok [y/N]: 
   ```