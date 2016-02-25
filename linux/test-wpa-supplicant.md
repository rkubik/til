# Test wpa_supplicant for Errors

    wpa_supplicant -Dwext -iwlan0 -c/etc/wpa_supplicant/wpa_supplicant.conf
    dhclient <interface>
    wpa_passphrase <ssid> <passphrase>
