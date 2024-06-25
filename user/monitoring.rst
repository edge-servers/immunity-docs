Monitoring
==========

.. image:: https://github.com/edge-servers/immunity-monitoring/raw/docs/docs/monitoring-demo.gif
   :target: https://github.com/edge-servers/immunity-monitoring/tree/docs/docs/monitoring-demo.gif
   :alt: Feature Highlights

`Immunity Monitoring
<https://github.com/edge-servers/immunity-monitoring/tree/1.0>`_
has been introduced in Immunity 22.05 and focuses
on allowing users to know the status of their devices at any given time.

.. contents:: **Table of Contents**:
   :backlinks: none
   :depth: 3

Deploy instructions
-------------------

The monitoring module is enabled by default in the
`Immunity 22.05 ansible role
<https://github.com/edge-servers/ansible-immunity2/tree/22.05>`_.

It's also available in
`docker-immunity <https://github.com/edge-servers/docker-immunity>`_
although its usage is not recommended for production usage yet, unless
the reader is willing to invest effort in adapting the docker images
and configurations to overcome any roadblocks encountered.

Quickstart Guide
----------------

This guide assumes you have the
`Immunity Monitoring
<https://github.com/edge-servers/immunity-monitoring/tree/1.0>`_ module enabled
in your Immunity server application and you have already followed
the steps to :doc:`install immunity-config on your OpenWRT
devices <./configure-device>`.

Install monitoring packages on the device
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

`Install the openwrt-immunity-monitoring packages
<https://github.com/edge-servers/openwrt-immunity-monitoring/tree/0.1.0#install-pre-compiled-packages>`_
on your device.

These packages collect and send the
monitoring data from the device to Immunity Monitoring and
are required to collect `metrics
<https://github.com/edge-servers/immunity-monitoring/tree/1.0#immunity_monitoring_metrics>`_
like interface traffic, WiFi clients, CPU load, memory usage, etc.

.. _immunity_reach_devices:

Make sure Immunity can reach your devices
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In order to perform `active checks <https://github.com/edge-servers/immunity-monitoring/tree/1.0#available-checks>`_
and other actions like
`triggering the push of configuration changes
<https://github.com/edge-servers/immunity-controller/tree/1.0#how-to-configure-push-updates>`_,
`executing shell commands
<https://github.com/edge-servers/immunity-controller/tree/1.0#sending-commands-to-devices>`_ or
`performing firmware upgrades
<https://github.com/edge-servers/immunity-firmware-upgrader/tree/1.0#perform-a-firmware-upgrade-to-a-specific-device>`_,
**the Immunity server needs to be able to reach the network devices**.

There are mainly two deployment scenarios for Immunity:

1. the Immunity server is deployed on the public internet and the
   devices are geographically distributed across different locations:
   **in this case a management tunnel is needed**
2. the Immunity server is deployed on a computer/server which is
   located in the same Layer 2 network (that is, in the same LAN)
   where the devices are located.
   **in this case a management tunnel is NOT needed**

1. Public internet deployment
#############################

This is the most common scenario:

- the Immunity server is deployed to the public internet, hence the
  server has a public IPv4 (and IPv6) address and usually a valid
  SSL certificate provided by Mozilla Letsencrypt or another SSL provider
- the network devices are geographically distributed across different
  locations (different cities, different regions, different countries)

In this scenario, the Immunity application will not be able to reach the
devices **unless a management tunnel** is used, for that reason having
a management VPN like OpenVPN, Wireguard, ZeroTier or any other tunneling
solution is paramount, not only to allow Immunity to work properly, but
also to be able to perform debugging and troubleshooting when needed.

In this scenario, the following requirements are needed:

- a VPN server must be installed in a way that the Immunity
  server can reach the VPN peers, for more information on how to do this
  via Immunity please refer to the following sections:

  - `OpenVPN tunnel automation
    <https://immunity.io/docs/user/vpn.html>`_
  - `Wireguard tunnel automation
    <https://github.com/edge-servers/immunity-controller/tree/1.0#how-to-setup-wireguard-tunnels>`_

  If you prefer to use other tunneling solutions (L2TP, Softether, etc.)
  and know how to configure those solutions on your own,
  that's totally fine as well.

  If the Immunity server is connected to a network infrastructure
  which allows it to reach the devices via pre-existing tunneling or
  Intranet solutions (eg: MPLS, SD-WAN), then setting up a VPN server
  is not needed, as long as there's a dedicated interface on OpenWrt
  which gets an IP address assigned to it and which is reachable from
  the Immunity server.

- The devices must be configured to join the management
  tunnel automatically, either via a pre-existing configuration in
  the firmware or via an
  `Immunity Template <https://immunity.io/docs/user/templates.html>`_.

- The `immunity-config <https://github.com/edge-servers/immunity-config>`_
  agent on the devices must be configured to specify
  the ``management_interface`` option, the agent will communicate the
  IP of the management interface to the Immunity Server and Immunity will
  use the management IP for reaching the device.

  For example, if the *management interface* is named ``tun0``,
  the immunity-config configuration should look like the following
  example:

.. code-block:: text

    # In /etc/config/immunity on the device

    config controller 'http'
        # ... other configuration directives ...
        option management_interface 'tun0'

2. LAN deployment
#################

When the Immunity server and the network devices are deployed in the same
L2 network (eg: an office LAN) and the Immunity server is reachable
on the LAN address, Immunity can then use the **Last IP** field of the
devices to reach them.

In this scenario it's necessary to set the
`"IMMUNITY
_MONITORING_MANAGEMENT_IP_ONLY"
<https://github.com/edge-servers/immunity-monitoring/tree/1.0#immunity-monitoring-management-ip-only>`_
setting to ``False``.

Find out more about Immunity Monitoring
---------------------------------------

For more information about the features offered by Immunity Monitoring
and the related OpenWrt packages we refer to the following sections
of their respective READMEs.

Immunity Monitoring Python/Django module
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- `List of the available features
  <https://github.com/edge-servers/immunity-monitoring/tree/1.0#available-features>`_
- `Passive vs Active Metric Collection
  <https://github.com/edge-servers/immunity-monitoring/tree/1.0#passive-vs-active-metric-collection>`_
- `Device Health Status
  <https://github.com/edge-servers/immunity-monitoring/tree/1.0#device-health-status>`_
- `Default Metrics
  <https://github.com/edge-servers/immunity-monitoring/tree/1.0#default-metrics>`_
- `Available Checks
  <https://github.com/edge-servers/immunity-monitoring/tree/1.0#available-checks>`_
- `Rest API
  <https://github.com/edge-servers/immunity-monitoring/tree/1.0#rest-api>`_
- `Django Settings
  <https://github.com/edge-servers/immunity-monitoring/tree/1.0#settings>`_

Immunity Monitoring OpenWrt packages
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- `Configuration options
  <https://github.com/edge-servers/openwrt-immunity-monitoring/tree/0.1.0#configuration-options>`_
- `Collecting vs Sending
  <https://github.com/edge-servers/openwrt-immunity-monitoring/tree/0.1.0#collecting-vs-sending>`_
- `Compiling immunity-monitoring
  <https://github.com/edge-servers/openwrt-immunity-monitoring/tree/0.1.0#compiling-immunity-monitoring>`_
- `Debugging
  <https://github.com/edge-servers/openwrt-immunity-monitoring/tree/0.1.0#debugging>`_
