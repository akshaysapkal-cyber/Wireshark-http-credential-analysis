# HTTP Credential Capture using Wireshark

## Introduction

In this project, I created a lab using Kali Linux and a Windows machine to observe how login data is transmitted over HTTP. By capturing network traffic with Wireshark, I analyzed POST requests and found how credentials can be seen in plaintext when encryption is not used.

## Lab Setup

- Attacker Machine: Kali Linux (Wireshark)
- Target Machine: Windows
- Website Used: Metasploitable 2
- Network: Same local network
- Protocol Used: HTTP

## Tools Used

- Wireshark
- Kali Linux
- Metasploitable 2 web browser
- Windows OS

## Objective

To capture and analyze HTTP POST requests and observe how sensitive data like login credentials can be transmitted in plaintext.

## Steps Performed

### Step 1: Start Wireshark

- Open Wireshark on Kali Linux
- Select the active network interface (eth0 / wlan0)
- Start packet capture

![Step1](https://github.com/akshaysapkal-cyber/Wireshark-http-credential-analysis/blob/main/Screenshots/step%201%20wireshark.png?raw=true) 

### Step 2: Perform Login

- Open browser on Windows machine
- Visit: http://metasploitable-ip.com
- Click on DVWA (This is login form)
- Enter dummy credentials used for this lab:
<pre>
Username: admin
Password: password
</pre>

![Step2](https://github.com/akshaysapkal-cyber/Wireshark-http-credential-analysis/blob/main/Screenshots/step%202%20login.png?raw=true) 

![step2 2](https://github.com/akshaysapkal-cyber/Wireshark-http-credential-analysis/blob/main/Screenshots/step%202%202nd.png?raw=true)

### Step 3: Apply Filter

Use the following filter in Wireshark:

``` http.request.method == POST ```

![step3](https://github.com/akshaysapkal-cyber/Wireshark-http-credential-analysis/blob/main/Screenshots/step%203.png?raw=true)

### Step 4: Find Credentials Using Packet Search

- In Wireshark, go to: **Edit → Find Packet**

- In the search window:
  - Set **Find By** → String  
  - Enter → `password`  
  - Search in → Packet Details  

- Click **Find / Next** to locate packets containing password fields  

![step4](https://github.com/akshaysapkal-cyber/Wireshark-http-credential-analysis/blob/main/Screenshots/step%204.png?raw=true) 

The credentials were successfully located within the packet details using the search functionality. To further validate the findings, the TCP stream was analyzed to confirm the transmitted data.

### Step 5: Follow TCP Stream

- Right click on packet → Follow → TCP Stream
- View full request including transmitted data

After capturing the login request, the credentials were visible in plaintext within the HTTP POST request.
To further verify the activity, the TCP stream was analyzed to view the complete communication between client and server. This provided a clearer view of how the credentials were transmitted.

![step5](https://github.com/akshaysapkal-cyber/Wireshark-http-credential-analysis/blob/main/Screenshots/Step%205.jpeg?raw=true)

![step5 2nd](https://github.com/akshaysapkal-cyber/Wireshark-http-credential-analysis/blob/main/Screenshots/step%205%202nd.png?raw=true)

## Key Observation

The login credentials were visible in plaintext within the HTTP request, showing that data transmitted over HTTP is not secure.

## What I Learned

- How to capture network traffic using Wireshark
- How HTTP POST requests work
- How to inspect packet details and payload
- How credentials can be exposed over insecure protocols

## Disclaimer

This project was performed in a controlled lab environment using test data for learning purposes only.
