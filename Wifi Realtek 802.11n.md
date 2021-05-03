# Realtek 802.11n WiFi USB (mini)

El adaptador WiFi, listado en mi pc cómo

```bash
lsusb
Bus 003 Device 002: ID 0bda:f179 Realtek Semiconductor Corp
```

```bash
sudo dmesg # lista los eventos del kernel
usb 3-4: new high-speed USB device number 2 using xhci_hcd
usb 3-4: New USB device found, idVendor=0bda, idProduct=f179, bcdDevice= 0.00
usb 3-4: New USB device strings: Mfr=1, Product=2, SerialNumber=3
usb 3-4: Product: 802.11n
usb 3-4: Manufacturer: Realtek
usb 3-4: SerialNumber: 1CBFCE803E64
```

es muy pequeño y tiene el puerto USB en color rojo. Debian no trae un driver por defecto, pero podemos seguir las instrucciones [que se muestran acá](https://github.com/kelebek333/rtl8188fu).

También puede ayudarte [este tutorial](https://vivaelsoftwarelibre.com/usar-la-wifi-con-realtek-semiconductor-802-11n-en-linux-mint/).
