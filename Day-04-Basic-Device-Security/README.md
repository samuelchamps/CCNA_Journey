# Day 04 - Basic Device Security

## CCNA 200-301 Journey

This lab is part of my **CCNA 200-301 study journey** using **Jeremy's IT Lab**.

Day 4 introduced me to the **Cisco IOS Command-Line Interface (CLI)** and how to perform basic security configuration on Cisco routers and switches.

---

## Lab Objective

The objective of this lab was to become familiar with the Cisco IOS CLI and configure basic device security on a router and switch.

The lab involved:

- Navigating different Cisco IOS CLI modes
- Configuring device hostnames
- Setting an enable password
- Viewing the running configuration
- Encrypting passwords
- Configuring an enable secret
- Testing authentication
- Saving the running configuration

---

## Tools Used

- Cisco Packet Tracer
- Cisco IOS CLI
- Jeremy's IT Lab
- Git
- GitHub

---

## Devices Configured

The lab contained:

- **R1** - Cisco Router
- **SW1** - Cisco Switch

Both devices were configured with basic security settings.

---

#  Cisco IOS CLI Modes

Cisco IOS provides different command modes depending on the level of access required.

## User EXEC Mode

User EXEC mode provides limited access to the device.

The prompt ends with:

```text
Router>
```

Example:

```text
Router>
```

---

## Privileged EXEC Mode

Privileged EXEC mode provides access to additional monitoring and administrative commands.

Enter privileged EXEC mode using:

```text
enable
```

Example:

```text
Router> enable
Router#
```

The `#` symbol indicates that the device is in privileged EXEC mode.

---

## Global Configuration Mode

Global configuration mode is used to make configuration changes to the device.

Enter global configuration mode using:

```text
configure terminal
```

Example:

```text
Router# configure terminal
Router(config)#
```

The command can also be shortened to:

```text
conf t
```

---

#  Lab Configuration

## 1. Configure Device Hostnames

The first task was to configure the correct hostname on each device.

### Router

```text
Router> enable
Router# configure terminal
Router(config)# hostname R1
R1(config)#
```

### Switch

```text
Switch> enable
Switch# configure terminal
Switch(config)# hostname SW1
SW1(config)#
```

Changing the hostname makes it easier to identify which network device is being configured.

---

#  2. Configure an Enable Password

An enable password was configured on both devices.

The password used in the lab was:

```text
CCNA
```

### R1

```text
R1(config)# enable password CCNA
```

### SW1

```text
SW1(config)# enable password CCNA
```

The `enable password` command protects access to privileged EXEC mode.

---

#  3. Test the Enable Password

I returned to User EXEC mode:

```text
R1(config)# exit
R1# exit
R1>
```

Then attempted to enter privileged EXEC mode again:

```text
R1> enable
Password:
```

After entering:

```text
CCNA
```

I was able to access privileged EXEC mode:

```text
R1#
```

---

#  4. View the Running Configuration

I used the following command to view the current device configuration:

```text
show running-config
```

Example:

```text
R1# show running-config
```

The configuration showed the enable password in plain text.

Example:

```text
enable password CCNA
```

This demonstrated why storing unencrypted passwords in the configuration is insecure.

---

#  5. Enable Password Encryption

To encrypt passwords stored in the configuration, I used:

```text
service password-encryption
```

Example:

```text
R1# configure terminal
R1(config)# service password-encryption
```

The same configuration was applied to SW1.

---

#  6. Verify Password Encryption

While still in global configuration mode, I used:

```text
do show running-config
```

Example:

```text
R1(config)# do show running-config
```

The previously visible password was now displayed in an encrypted format similar to:

```text
enable password 7 08026F6028
```

This showed that `service password-encryption` encrypted the password stored in the configuration.

---

#  7. Configure an Enable Secret

A more secure privileged EXEC password was then configured.

The password used was:

```text
Cisco
```

Configuration:

```text
R1(config)# enable secret Cisco
```

The same command was configured on SW1:

```text
SW1(config)# enable secret Cisco
```

Unlike `enable password`, the `enable secret` is stored as a hash rather than plain text.

---

#  8. Test the Enable Secret

I returned to User EXEC mode:

```text
R1(config)# exit
R1# exit
R1>
```

Then entered:

```text
R1> enable
Password:
```

The password required to enter privileged EXEC mode was now:

```text
Cisco
```

This demonstrated that when both `enable password` and `enable secret` are configured, the **enable secret takes precedence**.

---

#  9. Check the Passwords

I viewed the running configuration again:

```text
R1# show running-config
```

The configuration contained both the enable password and enable secret.

The encrypted enable password used:

```text
Type 7
```

The enable secret in this Packet Tracer lab used:

```text
Type 5
```

This showed the difference between the two password mechanisms.

---

#  10. Save the Configuration

Configurations made in the running configuration can be lost if the device restarts.

To save the configuration, I used:

```text
write memory
```

or the shortened version:

```text
write
```

From global configuration mode:

```text
R1(config)# do write
```

The configuration can also be saved using:

```text
copy running-config startup-config
```

---

## Verify the Startup Configuration

To confirm that the configuration was saved, I used:

```text
show startup-config
```

From global configuration mode:

```text
R1(config)# do show startup-config
```

This confirmed that the configuration would remain after the device was restarted.

---

# ⌨️ Important Commands Learned

| Command | Purpose |
|---|---|
| `enable` | Enter privileged EXEC mode |
| `configure terminal` | Enter global configuration mode |
| `hostname R1` | Change the device hostname |
| `enable password CCNA` | Configure an enable password |
| `show running-config` | Display the active configuration |
| `service password-encryption` | Encrypt plaintext passwords in the configuration |
| `enable secret Cisco` | Configure a more secure privileged EXEC password |
| `do show running-config` | Run an EXEC command from configuration mode |
| `write memory` | Save the running configuration |
| `copy running-config startup-config` | Save running configuration to startup configuration |
| `show startup-config` | Display the saved startup configuration |
| `exit` | Return to the previous CLI mode |

---

#  What I Learned

From this lab, I learned:

- How to navigate the Cisco IOS CLI.
- The difference between User EXEC, Privileged EXEC, and Global Configuration modes.
- How to change the hostname of Cisco devices.
- How to configure passwords for privileged EXEC access.
- Why plain-text passwords are a security risk.
- How `service password-encryption` protects passwords displayed in the configuration.
- The difference between `enable password` and `enable secret`.
- That `enable secret` takes precedence when both are configured.
- How to inspect the running configuration.
- How to save a configuration so it survives a device restart.

---

# Key Takeaway

Cisco IOS configuration is performed through different CLI modes, with each mode providing different levels of access.

One of the most important lessons from this lab was the difference between:

```text
enable password
```

and:

```text
enable secret
```

The `enable secret` provides more secure protection for privileged EXEC access and takes precedence when both are configured.

I also learned that making a configuration change is not enough — the running configuration must be saved to the startup configuration if I want it to remain after a reboot.

---

## 📁 Packet Tracer Lab

The completed Cisco Packet Tracer file for this lab is included in this repository:

```

The file can be opened using **Cisco Packet Tracer**.

---
