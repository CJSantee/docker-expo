# docker-expo
Dockerized Expo application. 

Tested on Mac. For Windows option see [kerbe/docker-expo](https://github.com/kerbe/docker-expo).

# Usage
Pull container from [DockerHub](https://hub.docker.com/r/cjsantee/expo) or project from [GitHub](https://github.com/CJSantee/docker-expo)

If using project from GitHub, build with: 
``` 
docker build -t cjsantee/expo:1.0 .
```

Run container with the following:
``` 
docker run -it --rm -p 19000:19000 -p 19001:19001 -p 19002:19002 -v "$PWD:/usr/app" \
-e REACT_NATIVE_PACKAGER_HOSTNAME=<<HOST LOCAL IP>> \
-e EXPO_DEVTOOLS_LISTEN_ADDRESS=0.0.0.0 \
--name=expo cjsantee/docker-expo:1.0
```

**Port 19000** is for accessing the actual application, which needs to be opened from your mobile device on ExpoGo. 

**Port 19001** is the default Metro Bundler port. 

**Port 19002** is for Expo DevTools, accessible by browser. Open at ```<<HOST LOCAL IP>>:19002```

Set REACT_NATIVE_PACKAGER_HOSTNAME to be your local IP address. If that is not set, Expo will bind to Docker container local IP. That IP isn't accessible for your mobile phone, even if it is in same WLAN.

Set EXPO_DEVTOOLS_LISTEN_ADDRESS to 0.0.0.0. Current version of expo-cli listens only 127.0.0.1, which doesn't work for Docker environment. Those forwarded ports need to be listened by containers internal ip, so we listen all addresses inside container with 0.0.0.0.

# Running with Docker Compose
Update build directory and volume location in docker-compose.yml and environment variables in .env

Run with: 
``` 
docker-compose up --build
```

# What is \<\<HOST LOCAL IP>> ??
On a Mac locate your local IP in system preferences under "Network"

"Your Wi-Fi is connected to *Wifi* and has the IP address \<\<HOST LOCAL IP>>"