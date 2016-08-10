## Ansible Role: Atlassian
Configure Atlassian software on RedHat/CentOS 7 servers

## JIRA Server
The JIRA binary installer requires input, so we can download it but you'll have to SSH in and run the installation manually. However JIRA Software & Service Desk are 1-click no-downtime upgrades inside the JIRA interface since v7.0, so we only need to manually update JIRA Core.

* Download any version of JIRA Core installer by setting `atlassian_jira_current_version` variable (latest version number found [here](https://www.atlassian.com/software/jira/core/update))
* Set JVM min/max memory (can make a huge difference on even smallish installs)
* Configure server.xml so you can add things such as custom domains and HTTPS support

## Bamboo Server
Bamboo Server has a lot of config files and extra drivers that are lost on every upgrade. For some unknown reason these user settings reside in the install_dir, instead of the home_dir, where the rest of your install specific persistent data resides (builds etc). Well, it makes upgrading a perfect use case for Ansible:

* Update to any specific release by setting `atlassian_bamboo_current_version` variable (latest version number found [here](https://www.atlassian.com/software/bamboo/download))
* Install database driver (ex: mysql connector)
* Set JVM min/max memory (can make a huge difference on even smallish installs)
* Configure server.xml so you can add things such as custom domains and HTTPS support
* Update other misc required configs (bamboo-init.properties)

## Bamboo Remote Agent

* Install remote agent jar
* Configure wrapper.conf
* Configure systemd service unit: `systemctl restart bamboo-agent`

## License
2-clause BSD
