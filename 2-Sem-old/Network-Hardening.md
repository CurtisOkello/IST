# Basic Cisco Router Hardening Guide

This reference guide outlines the baseline security configurations required to protect a Cisco IOS router from unauthorized access, minimize its attack surface, and encrypt administrative credentials.

---

## 🛡️ 1. Device Identity & Global Security
Modify the default hostname, enforce a minimum complexity rule for passwords, and ensure all passwords stored in the configuration file are encrypted.

```ethernet
Router(config)# hostname Edge-Router
Edge-Router(config)# security passwords min-length 10
Edge-Router(config)# service password-encryption
```

---

## 🔑 2. Securing Privileged Exec Mode
Protect access to global configuration mode. Always use `enable secret` which utilizes a modern hashing algorithm, rather than the legacy cleartext `enable password`.

```ethernet
Edge-Router(config)# enable secret SuperSecureP@ss123!
```

---

## 💻 3. Securing Physical Console Access
Prevent unauthorized physical access via a console cable by enforcing a password and setting an automatic inactivity log-out timer.

```ethernet
Edge-Router(config)# line console 0
Edge-Router(config-line)# password ConsoleP@ss567!
Edge-Router(config-line)# login
Edge-Router(config-line)# exec-timeout 5 0   ! Logs out after 5 minutes of idle time
Edge-Router(config-line)# exit
```

---

## 🔒 4. Enforcing SSH & Disabling Telnet
Telnet transmits credentials in plain text. Force the router to use SSH by establishing a cryptographic domain, generating encryption keys, and binding VTY lines to local secure authentication.

```ethernet
! Define domain and generate cryptographic RSA keys
Edge-Router(config)# ip domain-name company.local
Edge-Router(config)# crypto key generate rsa
! (When prompted, type 2048 for the key modulus size)

! Create a local administrator account
Edge-Router(config)# username netadmin secret AdminP@ss890!

! Configure virtual terminal lines to allow SSH ONLY
Edge-Router(config)# line vty 0 4
Edge-Router(config-line)# login local
Edge-Router(config-line)# transport input ssh
Edge-Router(config-line)# exec-timeout 10 0  ! Logs out remote sessions after 10 minutes
Edge-Router(config-line)# exit
```

---

## 🛑 5. Disabling Unnecessary Services
Minimize the device's attack surface by turning off legacy, unencrypted, or unneeded network discovery and management services.

```ethernet
Edge-Router(config)# no ip http server         ! Disable unencrypted web interface
Edge-Router(config)# no ip http secure-server  ! Disable HTTPS web management
Edge-Router(config)# no ip dns server          ! Disable DNS server functionality
Edge-Router(config)# no ip source-route        ! Disable source routing exploits
```

---

## 🛠️ Verification Commands

Execute these commands from Privileged Exec mode (`#`) to verify the hardening implementation:

* `show running-config`: Confirm all listed credentials appear as encrypted strings and `transport input ssh` is applied to VTY lines.
* `show ip ssh`: Verify that SSH status is operational (Version 2 is recommended).
