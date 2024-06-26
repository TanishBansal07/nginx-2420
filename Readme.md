### Step 1: Install Necessary Software

Install Vim and Nginx.

```bash
sudo pacman -S vim nginx
```

- Installs Vim (a text editor) and Nginx (a web server).
- Vim is used for editing configuration files and other text files.
- Nginx is the web server software that will serve the website.

**Note:** You could check whether nginx was installed using the `sudo nginx -version` command.

### Step 2: Configure Nginx

1. Navigate to the Nginx configuration directory.

```bash
cd /etc/nginx/
```

2. Create the following new directory to store your server blocks.

```bash
sudo mkdir sites-available sites-enabled
```

3. Edit the main Nginx configuration file.

```bash
sudo vim nginx.conf
```

- Opens the main Nginx configuration file in Vim for editing.

4. Add the following line inside the `http` block to include server blocks:

```nginx
include /etc/nginx/sites-enabled/*;
```

This is what your `http` block should look like:

```nginx
http {
    include mime.types
    include  /etc/nginx/sites-enabled/*
    ...
}
```


Save and exit the file.
To do so, Press `esc` and then type `:wq` to exit the file.



1. Create a new server block for your project.

```bash
sudo vim sites-available/nginx-2420.conf
```


The server block configuration file must be located in the sites-available directory within the Nginx configuration directory `/etc/nginx/sites-available`. However, the user can choose the name of the file within this directory.


**Step 2:**: Add the following to your configuration file:

```nginx
server {
    listen 80;
    server_name your_server_ip;

    root /web/html/nginx-2420;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

**Note**: Replace `your_server_ip` with your server's actual IP address.The provided server block configuration uses the file name nginx-2420 for the server block, but the user can choose a different name if desired.


5. Create a symbolic link to enable the server block.

```bash
sudo ln -s /etc/nginx/sites-available/nginx-2420 /etc/nginx/sites-enabled/
```


The symbolic link to enable the server block must be located in the sites-enabled directory within the Nginx configuration directory (/etc/nginx/sites-enabled).

6. Test Nginx configuration and restart the service.

```bash
sudo nginx -t
```

- Tests the Nginx configuration for syntax errors.

```bash
sudo systemctl restart nginx
```

- Restarts the Nginx service to apply the new configuration.

### Step 3: Set Up systemd Components

Create a directory for your website documents.

```bash
sudo mkdir -p /web/html/nginx-2420
```

Note: Remember to `nginx-2420` to your directory name if changed in earlier steps.

### Step 4: Serve the Demo Document

1. Create and edit the demo document.

```bash
sudo vim /web/html/nginx-2420/index.html
```

- Opens a new file in Vim for editing.

**Note**: The index.html file for the demo document is located within the project root directory `/web/html/nginx-2420`. The file name must be index.html for Nginx to serve it as the default document.

2. Paste the provided HTML document into the file or you can also add custom html of your own.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2420</title>
    <style>
        * {
            color: #db4b4b;
            background: #16161e;
        }
        body {
            display: flex;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
        }
        h1 {
            text-align: center;
            font-family: sans-serif;
        }
    </style>
</head>
<body>
    <h1>All your base are belong to us</h1>
</body>
</html>

```

- The provided HTML document is pasted into this file to serve as the demo page.

3. Open your browser and navigate to your server's IP address. You should see the demo page served by Nginx.

### Conclusion

You've now successfully set up a Arch Linux Server, installed necessary software like Vim and Nginx, configured Nginx with a separate server block, set up systemd components, served the provided demo document.
