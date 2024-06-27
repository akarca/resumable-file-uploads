# Resumable File Uploads with TUSD & Uppy

## Project Overview

This project provides a resilient and efficient solution for handling file uploads using [TUS](https://tus.io/) protocol implementation in **tusd** coupled with the client-side
library, **Uppy**. This guide will assist you through the setup process to get your server ready for accepting resumable file uploads.

I created this repository as an efficient solution to transfer files from my phone to computer easily and reliably. It can be used not only to handle photo transfers but also any other type of large or small files, thanks to its resumability feature. The project utilizes TUS protocol implementation through **tusd** server combined with the client-side library called **Uppy**.

## Downloading and Running tusd

Follow these steps below to download and run **tusd** on your machine:

1. Download the latest **tusd** binary from [here](https://github.com/tus/tusd/releases). If you're using Linux or mac use `wget`:

```bash
wget https://github.com/tus/tusd/releases/download/v2.4.0/tusd_darwin_arm64.zip
```

2. Open the zip file and move the executable to `/usr/local/bin/` or `/usr/bin/` directory:

```bash
unzip tusd_darwin_arm64.zip
chmod +x tusd_darwin_arm64/tusd
sudo mv tusd_darwin_arm64/tusd /usr/local/bin
```

3. Clone the repository

```bash
git clone https://github.com/akarca/resumable-file-uploads.git
cd resumable-file-uploads
```

4. Run **tusd** with the following command to set up your upload directory, host, port, and hooks directory:

```bash
tusd -upload-dir=./data -behind-proxy -host 0.0.0.0 -port 8080 -hooks-dir=./hooks/
```

## Setting up Nginx (linux)

1. Open nginx.conf and edit the path to the repository. Edit the line containing  `/Users/serdar/workspace/resumable-file-uploads/`.

2. Copy the `nginx.conf` file to your nginx configuration directory, typically located at `/etc/nginx/sites-enabled/` or `/etc/nginx/conf.d/`:

```bash
sudo cp nginx.conf /etc/nginx/conf.d/tusd.conf
```

3. Restart nginx:

```bash
sudo systemctl restart nginx
```

## Setting up Nginx (macOS)

1. If you're using Homebrew, install and set up nginx with the provided configuration file:

```bash
brew install nginx
cp nginx.conf /opt/homebrew/etc/nginx/servers/tusd.conf
brew services restart nginx
```

## Usage

1. Open your browser and go to `http://127.0.0.1:8000` or use a tool like Postman to send requests to http://127.0.0.1:8000/files/. If you want to upload photos from your phone, connect it to the
same WiFi as your computer and find your computers local IP address. Then you can open a browser on your phone and go to `http://<local ip e.g. 192.168.0.123>:8000`

2. The uploaded files will be stored in the "files/" directories, whereas tusd uses the "data/" folder for processing uploads. Feel free to delete the contents of this temporary directory after completion.

## Detailed Usage and Installation Guide

For more detailed instructions on how to use tusd with uppy and advanced configurations, please visit [TopSelfHosted.com](https://www.topselfhosted.com/blog/resumable-file-upload-server-using-tusd-and-uppy/).
