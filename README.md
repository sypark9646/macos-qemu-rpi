# macos-qemu-rpi

Bash scripts to run Raspbian (ARM architecture) on macOS Catalina using QEMU

# Note on Native Emulation Alternative

As of October 2020, consider leveraging QEMU's native emulation of the Raspi2/3 that became available instead of running the scripts in this repository.

See https://github.com/dhruvvyas90/qemu-rpi-kernel/tree/master/native-emuation for instructions on how to use QEMU's native emulation.

# Installation

Install [homebrew](https://brew.sh/), if you haven't already.
Next, run the following script:

```bash
./install.sh
```

# Running Raspbian in QEMU

```bash
./run.sh
```

This script doesn't require macOS, but the Raspbian image/kernel and QEMU are
required.

Note that this scripts forwards port TCP/5022 on the host (e.g., macOS) to port
TCP/22 on the Raspbian guest where Raspbian's SSH server is listening.
To run Raspbian in QEMU, no other application including Raspbian may listen on
port TCP/5022 on the host.

# Logging into Raspbian

Either log in via the QEMU window or use SSH:
```bash
ssh -F /dev/null -o "PreferredAuthentications password" -o "PasswordAuthentication yes" -p 5022 pi@127.0.0.1
```

If sshd failed to start, log in via the QEMU window and run `sudo service ssh restart`.

To get a root shell, run the following:
```bash
sudo bash
```

Note that no desktop manager is running, as the "Lite" image is used.
See https://www.raspberrypi.org/software/operating-systems/ for pointers to other images.

# Shutting Down Raspbian

Log into Raspbian, and then execute `sudo halt` in the Raspbian shell.

# Tutorials

Advanced configuration instructions under Raspbian are provided at
https://azeria-labs.com/emulate-raspberry-pi-with-qemu/

# Acknowledgements

Scripts in this repository are based on
https://gist.github.com/hfreire/5846b7aa4ac9209699ba#gistcomment-3075728 .
Credit goes to @janwillemCA, @tinjaw, and the other contributors to that GitHub
gist.

