# Overview

This charm provides Tiny-Tiny RSS (http://tt-rss.org/redmine/projects/tt-rss/wiki). Taken from the main project site:

Tiny Tiny RSS is an open source web-based news feed (RSS/Atom) reader and aggregator, designed to allow you to read news from any location, while feeling as close to a real desktop application as possible.

# Usage

To deploy the charm, you will need a bootstrapped Juju environment with capacity for two additional machines. You could, however, use the deploy-to feature of jitsu to deploy these charms to a single machine.

First deploy mysql then deploy tt-rss in your bootstrapped environment:

  juju deploy mysql
  juju deploy tt-rss

Next configure tt-rss to use the mysql backend by adding a relation between the two:

  juju add-relation tt-rss mysql

Finally, expose the tt-rss service:

  juju expose tt-rss

You can then browse to http://ip-address/tt-rss to configure the service. The default username and password are "admin/password". 

# Configuration

Currently, there are three configuration variables avialable to be set via Juju: fqdn, update-tasks, and update-interval.

## FQDN

This setting will update the TT-RSS config.php variable 'SELF_URL_PATH'. To update it simply issue the following:

  juju set tt-rss fqdn=mysite.example.com

Below is the yaml configuration found in the charm:

  fqdn:
    type: string
    default: localhost
    description: FQDN of the server

## Update Tasks

Update tasks are the number of spawned tasks used when calling the feed update function. For a installation with a high number of feeds, you may consider increasing the number of update tasks from the default value of '2'.

  juju set tt-rss update-tasks=4

Below is the yaml configuration found in the charm:

  update-tasks:
    type: int
    default: 2
    description: number of feed update tasks to spawn

## Update Interval

This configuration setting is used to set the frequency at which feeds are updated (in seconds). The current default setting is to update the installation feeds every 5 minutes. You can configure this by issuing the following:

  juju set tt-rss update-interval=600

Below is the yaml configuration found in the charm:

  update-interval:
    type: int
    default: 300
    description: frequency to check for feed updates

# Updating

To update your TT-RSS installation, it is recommended to use the updater plugin included in TT-RSS. This allows you to view and update your installation via the web interface. A helpful guide can be found on the TT-RSS site (http://tt-rss.org/redmine/projects/tt-rss/wiki/InstallationNotes#In-place-upgrading).

# Author and Charm Details

Author: NextRevision (notarobot@nextrevision.net)
Report bugs at: http://bugs.launchpad.net/charms/+source/tt-rss
Location: http://jujucharms.com/charms/precise/tt-rss

