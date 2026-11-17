# EX01 Developing a Simple Webserver
## Date:3.11.2026
## REG NO: 26011976

## AIM:
To develop a simple webserver to serve html pages and display the list of protocols in TCP/IP Protocol Suite.

## DESIGN STEPS:
### Step 1: 
HTML content creation.

### Step 2:
Design of webserver workflow.

### Step 3:
Implementation using Python code.

### Step 4:
Import the necessary modules.

### Step 5:
Define a custom request handler.

### Step 6:
Start an HTTP server on a specific port.

### Step 7:
Run the Python script to serve web pages.

### Step 8:
Serve the HTML pages.

### Step 9:
Start the server script and check for errors.

### Step 10:
Open a browser and navigate to http://127.0.0.1:8000 (or the assigned port).

## PROGRAM:
~~~
from http.server import HTTPServer, BaseHTTPRequestHandler
content = """
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TCP/IP Protocol Suite Reference</title>
    <style>
        :root {
            --bg-color: #f4f7f6;
            --text-color: #2c3e50;
            --card-bg: #ffffff;
            --accent-blue: #2980b9;
            --accent-red: #c0392b;
            --border-color: #e2e8f0;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-color);
            line-height: 1.6;
            margin: 0;
            padding: 40px 20px;
}

        .container {
            max-width: 800px;
            margin: 0 auto;
        }

        header {
            margin-bottom: 30px;
            text-align: center;
        }

        h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
            color: var(--text-color);
        }

        .description {
            font-size: 1.1rem;
            color: #7f8c8d;
        }

        .layer-card {
            background: var(--card-bg);
            border: 1px solid var(--border-color);
            border-radius: 8px;
            padding: 25px;
            margin-bottom: 20px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
        }

        .layer-title {
            font-size: 1.4rem;
            color: var(--accent-blue);
            margin-top: 0;
            margin-bottom: 15px;
            border-bottom: 2px solid var(--border-color);
padding-bottom: 8px;
        }

        .protocol-list {
            list-style-type: none;
            padding-left: 0;
            margin: 0;
        }

        .protocol-item {
            margin-bottom: 15px;
            padding-bottom: 15px;
            border-bottom: 1px dashed var(--border-color);
        }

        .protocol-item:last-child {
            margin-bottom: 0;
            padding-bottom: 0;
            border-bottom: none;
        }

        .protocol-name {
            font-weight: bold;
            color: var(--accent-red);
            font-size: 1.1rem;
        }

        .protocol-desc {
            display: block;
            margin-top: 4px;
            color: #34495e;
        }

        code {
            background-color: #f8f9fa;
padding: 2px 6px;
            border-radius: 4px;
            font-family: monospace;
            font-size: 0.9em;
            border: 1px solid #e1e8ed;
        }
    </style>
</head>
<body>

    <div class="container">
        <header>
            <h1>TCP/IP Protocol Suite</h1>
            <p class="description">A structured overview of the core protocols running the modern internet, mapped by conceptual network layers.</p>
        </header>

        <main>
            <!-- Transport Layer -->
            <section class="layer-card">
                <h2 class="layer-title">1. Transport Layer Protocols</h2>
                <ul class="protocol-list">
                    <li class="protocol-item">
                        <span class="protocol-name">TCP (Transmission Control Protocol)</span>
                        <span class="protocol-desc">A connection-oriented protocol that guarantees reliable, ordered, and error-checked delivery of data packets between applications using a three-way handshake.</span>
                    </li>
                    <li class="protocol-item">
                        <span class="protocol-name">UDP (User Datagram Protocol)</span>
                        <span class="protocol-desc">A connectionless, lightweight alternative to TCP. It prioritizes speed over reliability, making it ideal for live streaming, gaming, and DNS services.</span>
                    </li>
                </ul>
            </section>
<!-- Internet Layer -->
            <section class="layer-card">
                <h2 class="layer-title">2. Internet / Network Layer Protocols</h2>
                <ul class="protocol-list">
                    <li class="protocol-item">
                        <span class="protocol-name">IP (Internet Protocol)</span>
                        <span class="protocol-desc">The primary network layer mechanism (supporting both IPv4 and IPv6 addresses) responsible for routing data packets across distinct networks from source to destination.</span>
                    </li>
                    <li class="protocol-item">
                        <span class="protocol-name">ICMP (Internet Control Message Protocol)</span>
                        <span class="protocol-desc">Used by network devices to send error messages and operational data. Utilities like <code>ping</code> and <code>traceroute</code> rely on ICMP.</span>
                    </li>
                    <li class="protocol-item">
                        <span class="protocol-name">ARP (Address Resolution Protocol)</span>
                        <span class="protocol-desc">Resolves dynamic network layer addresses (IP addresses) into physical local link layer addresses (MAC addresses).</span>
                    </li>
                </ul>
            </section>

            <!-- Application Layer -->
            <section class="layer-card">
                <h2 class="layer-title">3. Application Layer Protocols</h2>
                <ul class="protocol-list">
                    <li class="protocol-item">
                        <span class="protocol-name">HTTP / HTTPS (Hypertext Transfer Protocol / Secure)</span>
                        <span class="protocol-desc">The foundational protocols used to transfer webpage data across the World Wide Web, with HTTPS wrapping the data in TLS encryption.</span>
                    </li>
                    <li class="protocol-item">
                        <span class="protocol-name">DNS (Domain Name System)</span>
                        <span class="protocol-desc">The directory system of the internet that translates human-readable domain names (like example.com) into numerical IP addresses.</span>
                    </li>
                    <li class="protocol-item">
                        <span class="protocol-name">DHCP (Dynamic Host Configuration Protocol)</span>
                        <span class="protocol-desc">Automatically assigns IP addresses, subnet masks, and gateway configurations to client devices entering a network.</span>
                    </li>
                </ul>
            </section>
</main>
    </div>

</body>
</html>

"""
class myhandler(BaseHTTPRequestHandler):
    def do_GET(self):
        print("request received")
        self.send_response(200)
        self.send_header('content-type', 'text/html; charset=utf-8')
        self.end_headers()
        self.wfile.write(content.encode())
server_address = ('',880)
httpd = HTTPServer(server_address,myhandler)
print("my webserver is running...")
httpd.serve_forever()
~~~
## OUTPUT:

![alt text](<Screenshot 2026-11-03 142416.png>)


## RESULT:
The program for implementing simple webserver is executed successfully.

