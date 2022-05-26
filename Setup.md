
# Add BOS-Telegram Bot to startup on Umbrel  

Login via ssh: `ssh umbrel@umbrel.local`  
bos path should be `/home/umbrel/.npm-global/bin/bos` - run `which bos` to verify  
Create file with: `sudo nano /etc/systemd/system/bos-telegram.service`  
Copy/Paste code below - replace YOURCONNECTIONCODE with your bot code and /path/to/bos with your path:
```
    [Unit]
    Description=bos-telegram
    Wants=lnd.service
    After=lnd.service


    [Service] 
    ExecStart=/path/to/bos telegram --connect YOURCONNECTIONCODE
    User=umbrel
    Restart=always
    TimeoutSec=120
    RestartSec=30
    StandardOutput=null
    StandardError=journal

    [Install]
    WantedBy=multi-user.target
```
Save/Exit `ctrl + x` then `y enter`  
Enable: `sudo systemctl enable bos-telegram.service`  
Load: `sudo systemctl daemon-reload`  
Start: `sudo systemctl start bos-telegram.service`  
Check: `sudo systemctl status  bos-telegram.service` you should see 'Active: active (running)'
