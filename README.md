[![Build Status](https://img.shields.io/travis/GeekChimp/ansible-role-ntp.svg)](https://travis-ci.org/GeekChimp/ansible-role-ntp) [![Ansible Galaxy](https://img.shields.io/badge/ansible--galaxy-ntp-green.svg)](https://galaxy.ansible.com/list#/roles/3006)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](https://github.com/geekchimp/ansible-role-ntp/blob/master/README.md#license) [![Bountysource](https://www.bountysource.com/badge/tracker?tracker_id=13000391)](https://www.bountysource.com/trackers/13000391-geekchimp-ansible-omnibus?utm_source=13000391&utm_medium=shield&utm_campaign=TRACKER_BADGE)

[![Gratipay](https://img.shields.io/gratipay/Frenck.svg)](https://gratipay.com/Frenck) [![PayPal](https://img.shields.io/badge/paypal-donate-red.svg)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=UZDP6DYW6W9BU)
[![Facebook](https://img.shields.io/badge/facebook-follow-blue.svg)](https://www.facebook.com/geekchimp) [![Twitter](https://img.shields.io/badge/twitter-follow-blue.svg)](https://twitter.com/gchimp) [![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/GeekChimp/ansible-omnibus?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)

# Ansible NTP Role

Installs and configures the NTP daemon

## Supported Platforms

Debian (and Debian based e.g. Ubuntu)

## Requirements

None.

## Variables & Defaults

```yaml
# Ensure the NTP daemon is running and the service is enabled.
ntp_enabled: yes

# Ensure the NTP configuration created by the DHCP client is removed.
ntp_remove_dhcp_configuration: yes

# Location of the NTP drift file.
ntp_driftfile: "/var/lib/ntp/ntp.drift"

# Enable this if you want statistics to be logged.
ntp_stats_enabled: no

# Location of where the statistics should be logged.
ntp_statsdir: "/var/log/ntpstats/"

# List of NTP servers to synchronize with.
# pool.ntp.org maps to about 1000 low-stratum NTP servers.
ntp_servers:
  - "0.pool.ntp.org"
  - "1.pool.ntp.org"
  - "2.pool.ntp.org"
  - "3.pool.ntp.org"

# The restrict option can be used to provide better control and security over what NTP can do, and who can effect it.
#
# Access control configuration; see /usr/share/doc/ntp-doc/html/accopt.html for
# details.  The web page <http://support.ntp.org/bin/view/Support/AccessRestrictions>
# might also be helpful.
#
# Note that "restrict" applies to both servers and clients, so a configuration
# that might be intended to block requests from certain clients could also end
# up blocking replies from your own upstream servers.
ntp_restrict:
  - "restrict -4 default kod notrap nomodify nopeer noquery"
  - "restrict -6 default kod notrap nomodify nopeer noquery"
  - "restrict 127.0.0.1"
  - "restrict ::1"

# If you want to provide time to your local subnet, change the next lines.
ntp_broadcast_enabled: no
ntp_broadcast_address: 192.168.123.255

# If you want to listen to time broadcasts on your local subnet?
# Please do this only if you trust everybody on the network!
ntp_broadcast_client_enabled: no
```

## Dependencies

Does not depend on other roles and/or plugins

## Installation

Using `ansible-galaxy`:

```
$ ansible-galaxy install geekchimp.ntp
```

Using `arm` ([Ansible Role Manager](https://github.com/mirskytech/ansible-role-manager/)):

```
$ arm install geekchimp.ntp
```

Using `git`:

```
$ git clone https://github.com/GeekChimp/ansible-role-ntp.git
```

Or get the whole GeekChimp Ansible Omnibus collection using `git`:

```
$ git clone https://github.com/GeekChimp/ansible-omnibus.git
```

## Example Playbook

```yaml
----
- name: Install and configure the NTP daemon
  hosts: servers
  vars:
    ntp_servers:
      - "0.pool.ntp.org"
      - "1.pool.ntp.org"
      - "2.pool.ntp.org"
      - "3.pool.ntp.org"
  roles:
    - { role: geekchimp.ntp }

```

## Design philosophy & code styling

Read more about this here: https://github.com/GeekChimp/ansible-omnibus#design-philosophy--code-styling

## Contributing

Ansible Omnibus is an open source project. Feel free to submit a pull request.
Please ensure you submit pull requests and bugs reports to the main repository located at:

https://github.com/geekchimp/ansible-omnibus

## Author

The Ansible Omnibus project was created in 2015 by Franck Nijhof (aka Frenck).

Contact the author via frenck at geekchimp dot com

## Contributors

See https://github.com/geekchimp/ansible-omnibus/contributors

## License

The MIT License (MIT)

Copyright (c) 2015 Franck Nijhof, GeekChimp.com

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.

THIS SOFTWARE IS NOT DESIGNED OR INTENDED FOR USE OR RESALE AS ON-LINE
CONTROL EQUIPMENT IN HAZARDOUS ENVIRONMENTS REQUIRING FAIL-SAFE
PERFORMANCE, SUCH AS IN THE OPERATION OF NUCLEAR FACILITIES, AIRCRAFT
NAVIGATION OR COMMUNICATION SYSTEMS, AIR TRAFFIC CONTROL, DIRECT LIFE
SUPPORT MACHINES, OR WEAPONS SYSTEMS, IN WHICH THE FAILURE OF THE
SOFTWARE COULD LEAD DIRECTLY TO DEATH, PERSONAL INJURY, OR SEVERE
PHYSICAL OR ENVIRONMENTAL DAMAGE ("HIGH RISK ACTIVITIES"). GEEKCHIMP
SPECIFICALLY DISCLAIMS ANY EXPRESS OR IMPLIED WARRANTY OF FITNESS
FOR HIGH RISK ACTIVITIES.
