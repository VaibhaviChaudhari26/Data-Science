# Steps to install KVM

---

1. Check if virtualization is enabled.

```shell
cat /proc/cpuinfo | grep -Ec '(vmx|svm)'
```

In this command, we are printing the contents of `/proc/cpuinfo`, then using grep for pattern matching. `vmx` is the name for Intel's virtualization and `svm` is AMD's. If the output is 0, virtualization is disabled in BIOS, otherwise it's on.

2. Install required packages

```shell
sudo apt install -y qemu-kvm virt-manager libvirt-daemon-system virtinst libvirt-clients
```

- qemu-kvm  – An opensource emulator and virtualization package that provides hardware emulation.
- virt-manager – A Qt-based graphical interface for managing virtual machines via the libvirt daemon.
- libvirt-daemon-system – A package that provides configuration files required to run the libvirt daemon.
- virtinst – A  set of command-line utilities for provisioning and modifying virtual machines.
- libvirt-clients – A set of client-side libraries and APIs for managing and controlling virtual machines & hypervisors from the command line.

3. Start and enable virtualization daemon

```shell
sudo systemctl enable libvirtd
sudo systemctl start libvirtd
sudo systemctl status libvirtd
```

> [!TIP]
> After viewing status of the `libvirtd` service, press `q` to exit out of the view.

4. Add user to KVM and libvirt group

```shell
sudo usermod -aG kvm $USER
sudo usermod -aG libvirt $USER
```

5. Launch KVM Virtual Machine Manager from App Launcher.

6. `QEMU/KVM` should show _connecting_ followed by _connected_ in the app. Now, you can launch as many virtual machines as you want!

---
