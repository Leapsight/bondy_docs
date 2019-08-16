# OS Settings

## Configuring Open File Limits

Bondy can accumulate a large number of open file handles during operation. The creation of numerous data files is normal, and the storage backend performs periodic merges of data file collections to avoid accumulating file handles.

To accommodate this you should increase the open files limit on your system. We recommend setting a soft limit of 65536 and a hard limit of 200000.

### Changing Limit For Current Session

Most operating systems can check and change the open-files limit for the current shell session using the `ulimit`command.

Start by checking the current open file limit values with:

```bash
ulimit -Hn # Hard limit
ulimit -Sn # Soft limit
```

Set the limit by using:

```bash
ulimit -n 200000
```

This configuration persists only for the duration of your shell session. To change the limit on a system-wide, permanent basis read the following sections.

### Linux

On most Linux distributions, the total limit for open files is controlled by `sysctl`.

If you installed Bondy from a binary package, you will need to the add the following settings to the `/etc/security/limits.conf` file for the `bondy` user:

{% code-tabs %}
{% code-tabs-item title="/etc/security/limits.conf" %}
```bash
bondy soft nofile 65536
bondy hard nofile 200000
```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### Enable PAM-Based Limits for Debian & Ubuntu

You can enable PAM-based user limits so that non-root users, such as the `bondy` user, may specify a higher value for maximum open files.

Edit `/etc/pam.d/common-session` and add the following line:

{% code-tabs %}
{% code-tabs-item title="/etc/pam.d/common-session" %}
```bash
session required pam_limits.so 
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Save and close the file.   
If `/etc/pam.d/common-session-noninteractive` exists, append the same line as above.

Then, edit `/etc/security/limits.conf` and append the following lines to the file:

{% code-tabs %}
{% code-tabs-item title="/etc/security/limits.conf" %}
```bash
soft nofile 65536
hard nofile 200000
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Save and close the file.

\(Optional\) If you will be accessing the Bondy nodes via secure shell \(SSH\), you should also edit `/etc/ssh/sshd_config` and set the following line:

{% code-tabs %}
{% code-tabs-item title="/etc/ssh/sshd\_config" %}
```bash
UseLogin yes
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Restart the machine so the limits take effect and verify that the new limits are set with the following command:

```bash
ulimit -a
```

## UseLogin no

And set its value to yes as shown here:

/ETC/SSH/SSHD\_CONFIG UseLogin yes 6. Restart the machine so the limits take effect and verify that the new limits are set with the following command:

SHELL ulimit -a

#### CentOS & Redhat

### macOS

### Solaris

To increase the open file limit on Solaris, add the following line to the `/etc/system file`:

{% code-tabs %}
{% code-tabs-item title="/etc/system" %}
```bash
set rlim_fd_max=200000
```
{% endcode-tabs-item %}
{% endcode-tabs %}

