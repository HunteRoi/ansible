# Custom Glances role

## Mandatory variables

- glances_pkg : it contains the name of the package to install (whether it is `glances` or `glances[all]`) for example
- dependencies_pkg: it contains the list of package dependencies that are needed for glances to run properly
- username: it contains the username for the password protected web interface

## Optional variables
- glances_service_src_path : it contains the path to the glances service to run on the host. 
Can either be `files/services/glances.service` (by default) or `files/services/glances-debian.service`

