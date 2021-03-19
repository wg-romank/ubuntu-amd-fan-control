# ubuntu-amd-fan-control

1. clone `amdgpu-tweakd` (https://github.com/amezin/amdgpu-tweakd) then `sudo python setup.py install` it
2. create a configuration file (if you have Sapphire Pulse RX 570 you could use one in this repo) then store it somewhere (e.g. `/etc/amdgpu-tweakd`)
3. create a `.service` file to make sure script is running (see `amdgpu-tweakd.service` for reference) then store it in ` /etc/systemd/system/amdgpu-tweakd.service`

Enjoy a peaceful evening ☕

# how to get `pci_id` and `vbios_version`

## `pci_id`

1. run `lspci` then look for your video device (may include `VGA` etc.)
2. run `grep PCI_ID /sys/bus/pci/devices/*/uevent` and look for value you saw in first column of `lspci` output maching your video device

if you put all in single command you should get something like this

```bash
grep PCI_ID /sys/bus/pci/devices/*/uevent | grep $(lspci | grep VGA | awk '{ print $1 }')
```

this would output on my system

```bash
/sys/bus/pci/devices/0000:1f:00.0/uevent:PCI_ID=1002:67DF
```

## `vbios_version`

Simply run `amdgpu-tweakd` with any config, along output lines you should see `vbios_version`

```bash
INFO: Identification data for Device('/sys/devices/pci0000:00/0000:00:03.1/0000:1f:00.0'): {'pci_id': '1002:67DF', 'pci_slot_name': '0000:1f:00.0', 'pci_subsys_id': '1DA2:E343', 'device': b'0x67df', 'vbios_version': b'113-D00034-L01'}
```
