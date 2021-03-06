# Request Info - Sample Backend Service
Sample backend service which returns request details to the caller.

## 1. Test Sample Service

- Set `NAME` environment variable to set the name of the service, which will out as a response
- Set `-read-envs` argument if it is required to out environment variables set in container
- set `-pretty` argument if it is required to out prettified JSON

Resource Usage
```yaml
resources:
  limits:
    cpu: "5m"
    memory: "10Mi"
  requests:
    cpu: "2m"
    memory: "5Mi"
```

### 1.1. Basic

Running backend service.
```sh
docker run -d -p 8080:8080 -e "NAME=Service A" --name service-A cakebakery/request-info:v1
```

Sending request to backend service.
```
curl http://localhost:8080/hello/world
```

```json
{"Name":"Service A","Request":{"Method":"GET","Header":{"Accept":["*/*"],"User-Agent":["curl/7.54.0"]},"URL":{"Scheme":"","Opaque":"","User":null,"Host":"","Path":"/hello/world","RawPath":"","ForceQuery":false,"RawQuery":"","Fragment":"","RawFragment":""},"ContentLength":0,"TransferEncoding":null,"Host":"localhost:8080","Form":null,"PostForm":null,"MultipartForm":null,"Trailer":null,"RemoteAddr":"172.17.0.1:55922","RequestURI":"/hello/world","TLS":null}}
```

Remove running service
```
docker rm -f service-A
```

### 1.2. Print ENV Variables

Running backend service.
```sh
docker run -d -p 8080:8080 -e "NAME=Service A" --name service-A cakebakery/request-info:v1 -read-envs
```

Sending request to backend service.
```
curl http://localhost:8080/hello/world
```

```json
{"Name":"Service A","Env":["PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin","NAME=Service A","HOME=/root"],"Request":{"Method":"GET","Header":{"Accept":["*/*"],"User-Agent":["curl/7.54.0"]},"URL":{"Scheme":"","Opaque":"","User":null,"Host":"","Path":"/hello/world","RawPath":"","ForceQuery":false,"RawQuery":"","Fragment":"","RawFragment":""},"ContentLength":0,"TransferEncoding":null,"Host":"localhost:8080","Form":null,"PostForm":null,"MultipartForm":null,"Trailer":null,"RemoteAddr":"172.17.0.1:35306","RequestURI":"/hello/world","TLS":null}}
```

Remove running service
```
docker rm -f service-A
```

### 1.3. Pretty JSON Output

Running backend service.
```sh
docker run -d -p 8080:8080 -e "NAME=Service A" --name service-A cakebakery/request-info:v1 -pretty
```

Sending request to backend service.
```
curl http://localhost:8080/hello/world
```

```json
{
    "Name": "Service A",
    "Request": {
        "Method": "GET",
        "Header": {
            "Accept": [
                "*/*"
            ],
            "User-Agent": [
                "curl/7.54.0"
            ]
        },
        "URL": {
            "Scheme": "",
            "Opaque": "",
            "User": null,
            "Host": "",
            "Path": "/hello/world",
            "RawPath": "",
            "ForceQuery": false,
            "RawQuery": "",
            "Fragment": "",
            "RawFragment": ""
        },
        "ContentLength": 0,
        "TransferEncoding": null,
        "Host": "localhost:8080",
        "Form": null,
        "PostForm": null,
        "MultipartForm": null,
        "Trailer": null,
        "RemoteAddr": "172.17.0.1:44222",
        "RequestURI": "/hello/world",
        "TLS": null
    }
}
```

Remove running service
```
docker rm -f service-A
```

## 2. Build From Source
run `./build-docker.sh`
