# Grafana

## Install Grafana
```
sudo apt-get install -y adduser libfontconfig1
wget https://dl.grafana.com/oss/release/grafana_9.5.2_amd64.deb
sudo dpkg -i grafana_9.5.2_amd64.deb

systemctl enable grafana-server --now
```

Access grafana dashboard
```
http://localhost:3000
```

Login 
```
username: admin
password: admin
```