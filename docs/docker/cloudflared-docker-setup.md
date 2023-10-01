# Cloudflared Docker

This is a short guide for setting up a cloudflare tunnel with a docker container.

## Docker Setup

All information needed for installing the docker itself.

??? info "Create App Folder"
    ### Create App Folder

    First we need to make sure we have the app folder ready with the correct permissions. you can use the following command in the terminal to create the folder and set the correct permissions:

    ```
    mkdir -p /mnt/user/appdata/cloudflared/ && chmod -R 777 /mnt/user/appdata/cloudflared/
    ```

??? warning "Authorise Cloudflared"
    ### Authorise Cloudflared

    Run the following command to authorize Cloudflared with the Cloudflare site you want to set up with a tunnel.

    ```
    docker run -it --rm -v /mnt/user/appdata/cloudflared:/home/nonroot/.cloudflared/ cloudflare/cloudflared:latest tunnel login
    ```

    It will print out a link to Cloudflare. Put this link in your web browser, and select which domain you want to use. Then, the daemon will automatically pull the certificate.

??? tip "Create a tunnel"
    ### Create a tunnel

    Now we need to create a tunnel. To do this, we will run another command from the terminal:

    ```
    docker run -it --rm -v /mnt/user/appdata/cloudflared:/home/nonroot/.cloudflared/ cloudflare/cloudflared:latest tunnel create TUNNELNAME
    ```

    This will create your tunnel's UUID.json file, which contains a secret used to authenticate your tunnelled connection with Cloudflare. The JSON file is only needed for running the tunnel, but any tunnel modifications require the cert.pem. More information about what requires what can be found [here](https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/create-tunnel).

    Make sure you copy your UUID, as this will be used in later steps. It can always be found later by the name of the JSON file.

??? example "Create the config.yaml"
    ### Create the config.yaml

    Now we need to create a config.yaml to configure the tunnel

    ```
    nano /mnt/user/appdata/cloudflared/config.yml
    ```

    Now paste in the following and amend your reverse proxy IP:PORT, tunnel UUID and domain name if applicable

    * if you have an ssl certificate on your reverse proxy, you need to pass in your domain name that the SSL cert is under
    * if you want to proxy to an http server, use the commended ingress rule
    * if you want to disable ssl verification, add noTLSVerify under originRequest

    ```
    tunnel: UUID
    credentials-file: /home/nonroot/.cloudflared/UUID.json

    # NOTE: You should only have one ingress tag, so if you uncomment one block comment the others

    # forward all traffic to Reverse Proxy w/ SSL
    ingress:
      - service: https://REVERSEPROXYIP:PORT
        originRequest:
          originServerName: yourdomain.com

    #forward all traffic to Reverse Proxy w/ SSL and no TLS Verify
    #ingress:
    #  - service: https://REVERSEPROXYIP:PORT
    #    originRequest:
    #      noTLSVerify: true

    # forward all traffic to reverse proxy over http
    #ingress:
    #  - service: http://REVERSEPROXYIP:PORT
    ```

??? success "Start the cloudflared docker"

    ### Start the cloudflared docker

    Start the cloudflare docker container with the following command:

    ```
    docker run -it -d -v /mnt/user/appdata/cloudflared:/home/nonroot/.cloudflared/ cloudflare/cloudflared:latest tunnel run -- UUID
    ```