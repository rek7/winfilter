# WinFilter
Winlogon and LSA Notification Password Filters 

## Reference
The primary code for each of the filters were pulled from:
- https://github.com/gtworek/PSBits/tree/master/PasswordStealing
- https://github.com/3gstudent/PasswordFilter

## Usage

### Building
Mingw is used to compile each dll. Install on your system before compiling, and then use `make` to build each dll. Binaries will exist in `bin/`.

### Filters
1) Modify the IP (`$ipa`) and Port (`$pt`) that the filters will call back to in the `kindtime_key.ps1` script. 

2) Modify the name of the dll (`$dllname`) at the top of each filters' powershell installer scripts (`lsainstall.ps1` and `wlinstall.ps1`). Run the installers.

3) Move each filter dll into `C:\windows\system32`.

### Credentials Receiver
To receive creds and set up the server, run:

```sh
python3 winfilter.py
```

By default, the IP will be '0.0.0.0' and the port will be '80'. You can give a specific ip or port using `--ip <ip_addr>` or `--port <port_num>`.

Screenshot Example:
```python3 winfilter.py --port 6006```

![photo](photos/photo.png)

Credentials will also be written to a file in the `creds` directory. Use the `--clean` option to clear out the directory.

### Sharing Creds

Creds are shipped to pwnboard via the `updatePwnboard` function. Make sure the url is correct at the top of the script.

### Other Methods
Credentials are written to the `creds` directory. Start a Python HTTP server in this directory, and have other use the command below.

```sh
curl <red_ip>:8000/<blue_ip>
```

Discord Webhook functionality is also available. Uncomment the `discordWH` function call in the `winfilter.py` file and modify the url variable.



