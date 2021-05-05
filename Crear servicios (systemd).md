# How to create services
Place this script at /etc/systemd/system/myServiceNameHere.service; replacing the name and path with ones of your choise.

[Unit]

Description=Overclock tweak

[Service]

ExecStart=/home/ethereum/eth-mining/overclock.sh

[Install]

WantedBy=multi-user.target

# Enable the service
sudo systemctl enable myServiceNameHere

# Start the service
sudo systemctl start myServiceNameHere
