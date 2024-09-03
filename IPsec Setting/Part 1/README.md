# IPsec Setting Part 1: Basic Lab Configuration

## 1. Changing Hostnames

### For R1:

```bash
config t
hostname R1
```

### For R2:

```bash
config t
hostname R2
```

### For R3:

```bash
config t
hostname R3
```

## 2. Configure Interfaces

### On R1:

```bash
interface fa0/0
ip address 1.1.1.1 255.255.255.0
no shutdown
exit

interface loopback 0
ip address 192.168.1.1 255.255.255.0
exit

interface tunnel 1
ip address 10.11.11.1 255.255.255.0
tunnel source 1.1.1.1
tunnel destination 2.2.2.3
exit
```

### On R2:

```bash
interface fa0/0
ip address 1.1.1.2 255.255.255.0
no shutdown
exit

interface fa0/1
ip address 2.2.2.2 255.255.255.0
no shutdown
exit
```

### On R3:

```bash
interface fa0/0
ip address 2.2.2.3 255.255.255.0
no shutdown
exit

interface loopback 0
ip address 172.16.3.3 255.255.255.0
exit

interface tunnel 1
ip address 10.11.11.3 255.255.255.0
tunnel source 2.2.2.3
tunnel destination 1.1.1.1
exit
```

## 3. Configure Static Route

### On R1:

```bash
ip route 0.0.0.0 0.0.0.0 1.1.1.2
```

### On R3:

```bash
ip route 0.0.0.0 0.0.0.0 2.2.2.2
```

## 4. Verify Connectivity

### On R1, R2, and R3:

```bash
show ip interface brief
```

### Ping Tests from R3:

```bash
ping 1.1.1.1  # Success
ping 10.11.11.1  # Success
ping 192.168.1.1 source loopback 0  # Expected failure

show ip route  # Should show no route for 192.168.1.1
```

## 5. Configure EIGRP Protocol

### On R3:

```bash
config t
router eigrp 10
network 172.16.3.0
network 10.11.11.0
no auto-summary
exit
```

### On R1:

```bash
config t
router eigrp 10
network 10.11.11.0
network 192.168.1.0
no auto-summary
exit
```

## 6. Verify Connectivity Between R1 and R3 Loopbacks

### On R1:

```bash
ping 172.16.3.3 source loopback 0  # Should succeed
```

### On R3:

```bash
ping 192.168.1.1 source loopback 0  # Should succeed
```

---

This format organizes the commands by task, removes any unnecessary lines, and corrects a couple of minor issues in the original commands.
