# DrumPadMachine-Kotlin


### How to determine download the wav files hosted on original app

1) Open CMD, and type 
    > ipconfig
2) Copy the Wi-Fi IPv4 address, for example `192.168.100.15`

3) Open iOS Wi-Fi settings, and add proxy for the current network:
   - ip: `192.168.100.15` (copied IPv4 address)
   - port: `8888` (default Charles port)

4) Download and install Charles
https://www.charlesproxy.com/

5) Porxy -> SSL Proxy Settings... -> Enable SSL Proxy

6) Right click on url `https://cloudflare-content-dpm.easybrain.com` and select Enable SSL Proxy

7) Download SSL Certificates by typing following url in Safari browser(from iOS device):
  - `https://chls.pro/ssl`

8) Search on iOS settinsg: VPN & Device Managmend -> Click on cerificate -> Enable it

9) General -> About -> (scroll down) -> Certificate Trust Settings -> Enable certificate

10) Open original DrumPadMachine app load some new pack (that is not download yet)

11) Open Charles -> (check now the revealed urls)

12) As of no 11/20/2023, the url for wav audio files is:
```
https://cloudflare-content-dpm.easybrain.com/shared/files/dpm/presets/id/2.zip
```

13) Run following script in PowerShell to download all files:

```
# This script will open all audio *zip archive links in Firefox browser, which will download them in Download folder
$firefoxPath = "C:\Program Files\Mozilla Firefox\firefox.exe"

for ($i = 0; $i -le 500; $i++) {
    $url = "https://cloudflare-content-dpm.easybrain.com/shared/files/dpm/presets/id/$i.zip"

    try {
        # Attempt to open URL in Firefox
        Start-Process $firefoxPath -ArgumentList $url -ErrorAction Stop
        Write-Host "Opened in Firefox: $url"
    } catch {
        Write-Host "File not found or error opening URL: $url"
    }
}
```