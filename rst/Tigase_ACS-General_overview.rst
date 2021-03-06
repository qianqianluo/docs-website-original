
ACS
===

**ACS** is our general purpose, commercial clustering strategy designed for more or less typical XMPP installations easily scaling to millions and beyond of online users without limit on cluster nodes. The load tests we have run over the code were included a user database with 100mln accounts and an average roster size of up to 150, but that’s not the limit.


Design
======

The clustering strategy is based on sharing information between cluster nodes about online users. Who is online and where the user is connected. Communication between cluster nodes is processed with the highest priority to ensure minimal delays with online user data population. An efficient synchronization mechanism allows for a minimal traffic between cluster nodes and distributing accurate data about connecting and disconnecting users.


Tigase ACS SM Installation
==========================

Tigase ACS SM component is by default provided with Tigase XMPP Server release (@-dist-max@ flavour of archive) so it’s enough to enable it in the configuration. It can be also obtained from ``tigase-acs`` distribution package.

After downloading the archive it’s simply matter of extracting it and copying contents of ``jars/`` directory of extracted archive to the ``jars/`` directory in ``tigase-server/`` installation directory, eg. under \*nix systems (assuming the archive was downloaded to main Tigase Server directory):

.. code:: bash

   tar -xf tigase-acs-${version}.tar.gz
   cp -R tigase-acs-${version}/jars/ tigase-server/jars/



Tigase ACS SM Configuration
===========================

In order to user Advanced Clustering Strategy, clustering mode first needs to be turned on:

.. code:: bash

   'cluster-mode' = true

and then an ACS strategy needs to be enabled:

.. code:: bash

   'sess-man' {
       strategy (class: tigase.server.cluster.strategy.OnlineUsersCachingStrategy) {}
   }
