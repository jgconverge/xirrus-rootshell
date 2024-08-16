# Xirrus Access Point Backdoor Automation Script

## Overview

This repository contains an Expect script that automates the process of logging into a Xirrus access point and executing a series of commands to access the underlying Linux system. This script is useful for penetration testers who need to quickly bypass the front-end CLI and get root access to the Linux shell.

**Credit:** The vulnerability and initial discovery were detailed by "WatTheFuckIsSecurity" on Reddit. You can read the full post [here](https://www.reddit.com/r/networking/comments/65yx3i/a_certain_network_vendor_has_a_front_door_in/).

## Background

A certain network vendor has a front door in their ArrayOS (AOS) that allows access to the underlying Linux system. The security surrounding this access is minimal, as it involves a hard-coded password (`pazzword`) that grants root access.

### How It Works

- **Step 1:** SSH into the Xirrus access point using the default credentials (`admin:admin`) if they haven't been changed.
- **Step 2:** Enter global configuration mode.
- **Step 3:** Modify the boot environment to include `CLIOPTS=b` in the boot arguments.
- **Step 4:** Save the configuration and execute the command to "open the door".
- **Step 5:** Enter the hard-coded password (`pazzword`) to access the Linux shell as root.

### Why Is This a Problem?

- The password `pazzword` is extremely easy to brute-force or guess.
- It grants root access to the underlying system, allowing full control over the device.
- The boot arguments and commands are not logged, making detection difficult.
- This access method works on both network equipment and enterprise management server software from the vendor.

### Default Credentials

By default, the Xirrus access points use the credentials `admin:admin`. It is strongly recommended to change these credentials to something more secure to prevent unauthorized access.

## Script Usage

### Prerequisites

- **Expect**: Ensure that Expect is installed on your system.

### Script Execution

```bash
./xirrus_rootshell.exp <host> <username> <password>
```

Replace `<host>`, `<username>`, and `<password>` with the appropriate values for your target device.

### Example

```bash
./xirrus_rootshell.exp 10.34.162.101 admin your_password_here
```

### What the Script Does

1. Logs into the Xirrus access point using SSH.
2. Enters the global configuration mode.
3. Modifies the boot arguments to include `CLIOPTS=b`.
4. Saves the configuration.
5. Opens the door by executing the command `o`.
6. Provides root access to the Linux shell.

## Potential Risks

- **Unauthorized Access:** If used maliciously, this script could allow unauthorized users to gain root access to network devices.
- **Device Stability:** Modifying boot arguments and accessing the Linux shell could potentially destabilize the device or cause unintended behavior. My testing hasn't revealed any stability issues thus far.

## Disclaimer

This script is provided for educational and penetration testing purposes only. The author is not responsible for any misuse or damage caused by using this script. Always obtain proper authorization before accessing or testing network devices.

## References

- Original Reddit Post: [WatTheFuckIsSecurity on Reddit](https://www.reddit.com/r/networking/comments/65yx3i/a_certain_network_vendor_has_a_front_door_in/)
