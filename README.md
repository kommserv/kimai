This Ansible galaxy role can be used to install and upgrade [Kimai](https://www.kimai.org/), see the [defaults/main.yml](defaults/main.yml) file for the required variables.

This role doesn't install or configure a webserver or database server but it assumes MySQL / MariaDB will be used.

Note that [version 1.7 upwards](https://github.com/kevinpapst/kimai2/blob/master/UPGRADING.md) requires the `mysql` database to contain timzone data, this can be [imported when changed using Ansible](https://git.coop/webarch/mariadb/blob/master/tasks/tz.yml).
