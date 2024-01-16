# Custom Glances web service role

## Mandatory variables

- apache_pkg : it contains the name of the web service package
- apache_service : it contains the name of the web service
- apache_glances_conf_path : it contains the path to the web service package's configuration file for glances.
It should thus end with `/glances.conf`.

## Optional variables
- apache_conf_path : it contains the path to the web service's configuration file for inline updates (on Arch-like distros)
