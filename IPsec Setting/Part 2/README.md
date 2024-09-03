# IPsec Setting Part 2: ISAKMP & IPsec Configuration

In this section, we'll configure ISAKMP and IPsec settings on routers R1 and R3 to secure the communication between them. Follow the steps below to complete the setup.

## 1. Define ISAKMP Policy on Router R1 & R3

On **Router R1**:

```bash
R1(config)# crypto isakmp policy 10
R1(config-isakmp)# hash md5
R1(config-isakmp)# authentication pre-share
R1(config-isakmp)# group 2
R1(config-isakmp)# encryption 3des
R1(config-isakmp)# exit
```

On **Router R3**:

```bash
R3(config)# crypto isakmp policy 10
R3(config-isakmp)# hash md5
R3(config-isakmp)# authentication pre-share
R3(config-isakmp)# group 2
R3(config-isakmp)# encryption 3des
R3(config-isakmp)# exit
```

## 2. Define Pre-shared Key on a Per Peer Basis on Router R1 & R3

On **Router R1**:

```bash
R1(config)# crypto isakmp key 0 cisco123 address 2.2.2.3
```

On **Router R3**:

```bash
R3(config)# crypto isakmp key 0 cisco123 address 1.1.1.1
```

## 3. Configure Transform Sets on Router R1 & R3

On **Router R1**:

```bash
R1(config)# crypto ipsec transform-set TSET esp-3des esp-md5-hmac
R1(config)# exit
```

On **Router R3**:

```bash
R3(config)# crypto ipsec transform-set TSET esp-3des esp-md5-hmac
R3(config)# exit
```

## 4. Create IPsec Profile on Router R1 & R3

On **Router R1**:

```bash
R1(config)# crypto ipsec profile GRE-PROFILE
R1(ipsec-profile)# set transform-set TSET
R1(ipsec-profile)# exit
```

On **Router R3**:

```bash
R3(config)# crypto ipsec profile GRE-PROFILE
R3(ipsec-profile)# set transform-set TSET
R3(ipsec-profile)# exit
```

## 5. Assign IPsec Profile on Tunnel Interfaces

On **Router R1**:

```bash
R1(config)# interface tunnel 1
R1(config-if)# tunnel protection ipsec profile GRE-PROFILE
R1(config-if)# exit
```

On **Router R3**:

```bash
R3(config)# interface tunnel 1
R3(config-if)# tunnel protection ipsec profile GRE-PROFILE
R3(config-if)# exit
```

## Verification

1. **Start Packet Capture**:

   - On **Router R3**, right-click on the `fa0/0` interface and select "Start Capture". This will open Wireshark or a similar tool to monitor the traffic on this interface.

     ![alt text](image.png)

2. **Initiate Traffic**:

   - On **Router R1**, run the following command to send a ping from R1's loopback interface to R3:
     ```bash
     R1# ping 172.16.3.3 source loopback 0
     ```

3. **Analyze the Packet Capture**:

   - In Wireshark, filter the captured traffic using the IP address of either Router R1 or Router R3. You can apply the filter like this:
     ```
     ip.addr == 1.1.1.1 || ip.addr == 2.2.2.3
     ```
   - Look at the **Protocol** column in Wireshark:
     - You should see packets labeled as **ESP (Encapsulating Security Payload)**, which indicates that the traffic is encrypted.
     - The **Info** column should show "ESP" instead of the higher-level protocols like ICMP, indicating that the ping request and response are being encrypted.

   ![alt text](image-1.png)

4. **Detailed View**:

   - Click on any of the ESP packets and expand the **Internet Protocol Security** section in Wireshark.
   - You won't be able to see the inner contents of the packet (like the ICMP echo request and reply) because they are encrypted. This lack of visibility confirms that the traffic is encrypted.

   ![alt text](image-2.png)

## What to Observe

- **Encrypted Packets**: If IPsec is correctly configured, all packets between the routers that should be secured will appear as ESP packets in the capture, indicating that the data is encrypted.
- **No Cleartext Data**: The ping responses and requests will not be visible as regular ICMP packets, confirming that the communication is being encrypted by IPsec.

---
