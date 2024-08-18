To run the Python script at startup and ensure it runs in the background on Ubuntu, you can create a systemd service. Here's how you can do it:

Create the Python script: Save the provided Python script to a file, for example, clone_repo.py.

Make the Python script executable:

```sh

chmod +x /path/to/main.py
```
Create a systemd service file:
Create a new service file for your script, e.g., clone_repo.service. You can do this by creating a new file in /etc/systemd/system/.

```sh

sudo nano /etc/systemd/system/clone_repo.service
```
Add the following content to the service file:

```ini
[Unit]
Description=Clone Git Repository Service
After=network-online.target

[Service]
ExecStart=/usr/bin/python3 /path/to/clone_repo.py
WorkingDirectory=/path/to
StandardOutput=inherit
StandardError=inherit
Restart=always
User=your-username

[Install]
WantedBy=multi-user.target
```
Replace /path/to/clone_repo.py with the actual path to your Python script. Also, replace your-username with your actual username.

Reload systemd to recognize the new service:

```sh
sudo systemctl daemon-reload
```
Enable the service to run at startup:

```sh

sudo systemctl enable clone_repo.service
```
Start the service immediately:

```sh
sudo systemctl start clone_repo.service
```
Check the status of the service:

```sh
sudo systemctl status clone_repo.service
```
This setup will ensure that your Python script runs in the background at startup, checking for an internet connection and cloning the repository if the connection is available.
