Changelog
=========

v0.1.1
------

*Released: 2015-06-02*

- Role is updated to use new features in ``debops.ifupdown``:

  Most of the "logic" behind how IP addresses were configured is now included
  in ``debops.ifupdown``. Instead of having separate variables for IPv4 and
  IPv6 addresses, you now shouldd use ``subnetwork_addresses`` list to specify
  IPv4/IPv6 subnets to configure, in the "host/prefix" format.

  Names of generated files in ``/etc/network/interfaces.d/`` have been changed
  to no longer contain duplicate ``_ipv4_ipv4`` or ``_ipv6_ipv6`` suffixes,
  since ``debops.ifupdown`` automatically adds the network suffix. You need to
  remove old configuration files from ``/etc/network/interfaces.config.d/`` to
  prevent any problems with duplicate interface configuration.

  ``subnetwork_ipv{4,6}_options`` variables have been renamed to
  ``subnetwork_options{6}``. By default, bridge will be configured with
  "forward delay" 0 to help with DHCP requests.

  ``subnetwork_ifupdown_prepend_interfaces`` list has been removed.

  ``subnetwork_ipv4_gateway`` variable has been renamed to
  ``subnetwork_ipv4_nat_snat_interface`` to better reflect its purpose as it
  specifies the interface from which firewall should take an IPv4 address to
  use in SNAT directive. [drybjed]

v0.1.0
------

*Released: 2015-05-12*

- Add Changelog. [drybjed]

- Disable automatically added ``allow-hotplug`` option in IPv6 bridge section.
  IPv6 is enabled automatically with IPv4 when bridge is brought up. [drybjed]

- Redefine ``subnetwork_ipv{4,6}_options`` variables.

  When you use multiple subnetwork interfaces, additional options provided in
  above variables for 1 interface would propagate into the rest of the
  interfaces. To change that, options variables are redefined as dicts with
  keys specifying the interface name and values being YAML text blocks with
  options.

  Note that dict keys must be specified explicity, not as Jinja variables. See
  ``defaults/main.yml`` file for examples. [drybjed]

