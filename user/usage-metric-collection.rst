Collection of Usage Metrics
===========================

The ``immunity-utils`` module includes an optional sub-app
``immunity_utils.metric_collection``, which allows us to collect of the
following information from Immunity instances:

- Immunity Version
- List of enabled Immunity modules and their version
- Operating System identifier, e.g.: Linux version, Kernel version, target
  platform (e.g. x86)
- Installation method, if available, e.g. `ansible-immunity2
  <https://github.com/edge-servers/ansible-immunity2>`_ or `docker-immunity
  <https://github.com/edge-servers/docker-immunity>`_

The data above is collected during the following events:

- **Install**: when Immunity is installed the first time
- **Upgrade**: when any Immunity module is upgraded
- **Heartbeat**: once every 24 hours

We collect data on Immunity usage to gauge user engagement,
satisfaction, and upgrade patterns. This informs our development
decisions, ensuring continuous improvement aligned with user needs.

To enhance our understanding and management of this data, we have
integrated `Clean Insights <https://cleaninsights.org/>`_, a
privacy-preserving analytics tool. Clean Insights allows us to
responsibly gather and analyze usage metrics without compromising
user privacy. It provides us with the means to make data-driven
decisions while respecting our users' rights and trust.

We have taken great care to ensure no sensitive or personal data is
being tracked.

Opting out from metric collection
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You can opt-out from sharing this data any time from the "System Info"
page. Alternatively, you can also remove the
``immunity_utils.metric_collection`` app from ``INSTALLED_APPS`` in one
of the following ways:

- If you are using the `ansible-immunity2
  <https://github.com/edge-servers/ansible-immunity2>`_ role, you can set
  the variable ``immunity2_usage_metric_collection`` to ``false`` in
  your playbook.

- If you are using `docker-immunity
  <https://github.com/edge-servers/docker-immunity>`_, you can set the
  environment variable ``METRIC_COLLECTION`` to ``False`` in the
  ``.env`` file.

However, it would be very helpful to the project if you keep the
collection of these metrics enabled, because the feedback we get from
this data is useful to guide the project in the right direction.
