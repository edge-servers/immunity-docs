RADIUS
======

Immunity RADIUS has been introduced in Immunity 22.05 and
provides many features aimed at public WiFi services.

.. contents:: **Table of Contents**:
   :backlinks: none
   :depth: 3

Deploy instructions
-------------------

See `Enabling the RADIUS module on the
Immunity 22.05 ansible role documentation
<https://github.com/edge-servers/ansible-immunity2/tree/22.05#enabling-the-radius-module>`_.

Alternatively you can set it up manually by following these guides:

- `Freeradius Setup for Captive Portal authentication
  <https://immunity-radius.readthedocs.io/en/stable/developer/freeradius.html>`_
- `Freeradius Setup for WPA Enterprise (EAP-TTLS-PAP) authentication
  <https://immunity-radius.readthedocs.io/en/stable/developer/freeradius_wpa_enterprise.html>`_

This module is also available in
`docker-immunity <https://github.com/edge-servers/docker-immunity>`_
although its usage is not recommended for production usage yet, unless
the reader is willing to invest effort in adapting the docker images
and configurations to overcome any roadblocks encountered.

Find out more about Immunity RADIUS
-----------------------------------

For more information about the features offered by Immunity RADIUS,
we refer to the its documentation:

- `Registration of new users <https://immunity-radius.readthedocs.io/en/stable/user/registration.html>`_
- `SMS verification <https://immunity-radius.readthedocs.io/en/stable/user/settings.html#immunity-radius-sms-verification-enabled>`_
- `Importing users <https://immunity-radius.readthedocs.io/en/stable/user/importing_users.html>`_
- `Generating users <https://immunity-radius.readthedocs.io/en/stable/user/generating_users.html>`_
- `Social Login <https://immunity-radius.readthedocs.io/en/stable/user/social_login.html>`_
- `Single Sign-On (SAML) <https://immunity-radius.readthedocs.io/en/stable/user/saml.html>`_
- `Enforcing session limits <https://immunity-radius.readthedocs.io/en/stable/user/enforcing_limits.html>`_
- `REST API <https://immunity-radius.readthedocs.io/en/stable/user/api.html>`_
- `Django Settings <https://immunity-radius.readthedocs.io/en/stable/user/settings.html>`_
