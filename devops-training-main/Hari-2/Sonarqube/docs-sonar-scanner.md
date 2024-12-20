# Sonar Scanner 

## Create Project
You can create project with sonarqube dashboard

## Install Scanner
Download and extract sonar-scanner package
```
wget https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.8.0.2856-linux.zip
unzip sonar-scanner-cli-4.8.0.2856-linux.zip
```

Move sonar-scanner package and change ownership
```
mv -v /tmp/sonar-scanner-4.8.0.2856-linux/ /opt/sonar-scanner/
chown -R sonar:sonar /opt/sonar-scanner 
```

Create link sonar-scanner
```
ln -s /opt/sonar-scanner/bin/sonar-scanner /usr/bin/
```

## Running
### Scanning
Config project
```
vim sonar-project.properties
```

Edit
```
# must be unique in a given SonarQube instance
sonar.projectKey=Simple-Apps

# --- optional properties ---

# defaults to project key
sonar.projectName=Simple Apps
# defaults to 'not provided'
sonar.projectVersion=1.0
 
# Path is relative to the sonar-project.properties file. Defaults to .
sonar.sources=.
 
# Encoding of the source code. Default is default system encoding
sonar.sourceEncoding=UTF-8
```

Running Scanner
```
sonar-scanner \
  -Dsonar.projectKey=Simple-Apps \
  -Dsonar.sources=. \
  -Dsonar.host.url=http://10.23.0.11:9000 \
  -Dsonar.login=sqp_1405bc476b26d2b88fd512d79d8f3383f08e8dff
```
### Scanning with exclusions
Config project
```
vim sonar-project.properties
```

Edit
```
sonar.exclusions=coverage/**, node_modules/**, testing/**
```

Running Scanner
```
sonar-scanner \
  -Dsonar.projectKey=Simple-Apps \
  -Dsonar.sources=. \
  -Dsonar.host.url=http://10.23.0.11:9000 \
  -Dsonar.login=sqp_1405bc476b26d2b88fd512d79d8f3383f08e8dff
```

### Scanning with testing
Config project
```
vim sonar-project.properties
```

Edit
```
sonar.test=testing/
```

Running Scanner
```
sonar-scanner \
  -Dsonar.projectKey=Simple-Apps \
  -Dsonar.sources=. \
  -Dsonar.host.url=http://10.23.0.11:9000 \
  -Dsonar.login=sqp_1405bc476b26d2b88fd512d79d8f3383f08e8dff
```

### Scanning with coverage
Config project
```
vim sonar-project.properties
```

Edit
```
sonar.javascript.lcov.reportPaths=coverage/lcov.info
```

Running Scanner
```
sonar-scanner \
  -Dsonar.projectKey=Simple-Apps \
  -Dsonar.sources=. \
  -Dsonar.host.url=http://10.23.0.11:9000 \
  -Dsonar.login=sqp_1405bc476b26d2b88fd512d79d8f3383f08e8dff
```