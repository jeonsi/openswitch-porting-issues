https://tree.taiga.io/project/openswitch/issues?q=676

# When I save the configuration as below, it hangs.

```
copy running-config startup-config
[prompt never shows up]
```

- Just after installation, when I save the configuration at first time, it works normally.
- But from the second initiation of the above command, CLI prompt does not show up for quite long time, for example, more than 10 minutes.
- During that period, if I ssh to the switch on another terminal, I can access the switch normally.
- If rebooted, all configuration is removed. Furthermore, no configuration can be done.

# Analysis
- The configuration is saved in the file: /var/local/openvswitch/config.db
- This file grows abnormally large.
- Because it is too large, it make problem reading or writing the file.

# Workaround
- Delete the file: /var/local/openvswitch/config.db, and reboot.
- Reconfigure
- Don't save the configuration
