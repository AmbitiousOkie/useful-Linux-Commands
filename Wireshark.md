## Wireshark Filters

## Display Filters 

`wlan.fc.type == 2`

`(wlan.fc.type == 2) && ~(wlan.fc.subtype == 0)`

## Capture Filters

`(wlan addr1 3A:30:F9:0F:E1:95) or (wlan addr2 3A:30:F9:0F:E1:95) or (wlan addr3 3A:30:F9:0F:E1:95) or (wlan addr4 3A:30:F9:0F:E1:95)`