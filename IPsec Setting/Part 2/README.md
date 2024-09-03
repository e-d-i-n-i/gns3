Here’s how you can organize the ISAKMP & IPsec configuration steps into your GitHub README file for Part 2:

---

## Part 2: ISAKMP & IPsec Configuration

In this section, we'll configure ISAKMP and IPsec settings on routers R1 and R3 to secure the communication between them. Follow the steps below to complete the setup.

### 1. Define ISAKMP Policy on Router R1 & R3

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

### 2. Define Pre-shared Key on a Per Peer Basis on Router R1 & R3

On **Router R1**:

```bash
R1(config)# crypto isakmp key 0 cisco123 address 2.2.2.3
```

On **Router R3**:

```bash
R3(config)# crypto isakmp key 0 cisco123 address 1.1.1.1
```

### 3. Configure Transform Sets on Router R1 & R3

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

### 4. Create IPsec Profile on Router R1 & R3

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

### 5. Assign IPsec Profile on Tunnel Interfaces

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

### Verification

1. **Start Packet Capture**:

   - On **Router R3**: Right-click on the `fa0/0` interface and select "Start Capture".

2. **Test Connectivity**:
   - On **Router R1**:
     ```bash
     R1# ping 172.16.3.3 source loopback 0
     ```

### What to Observe

- The packet capture on **Router R3** should show encrypted traffic when the ping command is executed from **Router R1**. This indicates that IPsec is successfully encrypting the data between R1 and R3.
- If the ping is successful, it means the tunnel is properly configured, and the routers are securely communicating using IPsec.

---
