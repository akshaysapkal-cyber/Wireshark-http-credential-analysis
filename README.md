# HTTP Credential Capture using Wireshark

## Introduction

In this project, I created a lab using Kali Linux and a Windows machine to observe how login data is transmitted over HTTP. By capturing network traffic with Wireshark, I analyzed POST requests and found how credentials can be seen in plaintext when encryption is not used.

## Lab Setup

- Attacker Machine: Kali Linux (Wireshark)
- Target Machine: Windows
- Network: Same local network
- Protocol Used: HTTP

## Tools Used

- Wireshark
- Kali Linux
- Windows OS
- Web Browser

## Objective

To capture and analyze HTTP POST requests and observe how sensitive data like login credentials can be transmitted in plaintext.

## Steps Performed

### Step 1: Start Wireshark

- Open Wireshark on Kali Linux
- Select the active network interface (eth0 / wlan0)
- Start packet capture

Screenshot: step1_capture.png

### Step 2: Perform Login

- Open browser on Windows machine
- Visit: http://moviescope.com
- Enter test credentials

Screenshot: step2_login.png

### Step 3: Apply Filter

Use the following filter in Wireshark:

<pre> ```bash http.request.method == "POST" ``` </pre>

 Screenshot: step3_filter.png

### Step 4: Identify Request

- Locate the POST request packet
- Verify source (Windows machine) and destination (server)

 Screenshot: step4_packet.png

### Step 5: Inspect Packet

- Go to: Packet Details → Hypertext Transfer Protocol
- Expand form data section

📸 Screenshot: step5_details.png

### Step 6: Follow TCP Stream

- Right click on packet → Follow → TCP Stream
- View full request including transmitted data

📸 Screenshot: step6_tcpstream.png

## Key Observation

The login credentials were visible in plaintext within the HTTP request, showing that data transmitted over HTTP is not secure.

## What I Learned

- How to capture network traffic using Wireshark
- How HTTP POST requests work
- How to inspect packet details and payload
- How credentials can be exposed over insecure protocols

## Disclaimer

This project was performed in a controlled lab environment using test data for learning purposes only.
