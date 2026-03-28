# 🖧 Day 4 | Subnetting (Understanding Network Boundaries)

## 🎯 Objective
Understand why subnet masks exist, how networks are divided, and how to recognize network ranges without guessing.

---

## 🧠 Core Idea
A network is not just devices connected.

It is devices grouped within a boundary.

Subnetting defines that boundary.

---

## 🌐 What Subnetting Means
Subnetting is the process of dividing a network into smaller network segments.

A subnet mask tells you which part of an IP address represents the network and which part represents the host.

![Subnetting Concept](https://github.com/Pelumi-Johnson/Day-4-Subnetting-Understanding-Network-Boundaries-/blob/main/Screenshot%202026-03-28%20020959.png)

---

## 🧠 Basic Example

Subnet mask:
255.255.255.0

This means:
- first 3 octets identify the network
- last octet identifies the hosts

Network:
192.168.1.0

Usable host range:
192.168.1.1 to 192.168.1.254

Broadcast:
192.168.1.255

![Subnet Mask Example](https://github.com/Pelumi-Johnson/Day-4-Subnetting-Understanding-Network-Boundaries-/blob/main/Screenshot%202026-03-28%20022018.png)

---

## 🧠 Rule to Remember
If two devices do not share the same network portion, they cannot communicate directly.

---

## 🧪 Lab Setup
Rebuilt the network from memory using:
- 1 Router
- 1 Switch
- 2 PCs

### 📸 Insert Screenshot Here
![Rebuilt Topology](topology.png)

---

## ⚙️ Boundary Test

### PC0
192.168.1.10
255.255.255.0

### PC1
192.168.1.200
255.255.255.0

This communication should work because both devices belong to the same network:
192.168.1.0

### 📸 Insert Screenshot Here
![Same Network Test](same-network-test.png)

---

## 💥 Boundary Break Test

Changed PC1 to:
192.168.2.10
255.255.255.0

This communication should fail because the devices are now in different networks:
- PC0 → 192.168.1.0
- PC1 → 192.168.2.0

### 📸 Insert Screenshot Here
![Different Network Test](different-network-test.png)

---

## Thinking Like an Engineer
Instead of memorizing addresses, I asked myself:

What network is this device in?

Example:
IP Address: 192.168.5.23
Mask: 255.255.255.0

Network:
192.168.5.0

When the mask is 255.255.255.0:
- same first 3 octets = same network
- different first 3 octets = different network

---

## Additional Understanding from Practice

### What a Subnet Mask Really Means
A subnet mask tells you which part of the IP address is the network portion and which part is the host portion.

Example:
IP Address: 192.168.1.152
Subnet Mask: 255.255.255.0

This means:
- 192.168.1 = network portion
- 152 = host portion

A home network using 255.255.255.0 is still a subnet, but it is usually one large subnet that has not been further divided into smaller ones.

---

## Bit Understanding and Prefix Logic

Subnet masks come from the prefix length.

Example:
- /24 means 24 network bits
- /28 means 28 network bits
- /22 means 22 network bits

The mask is built by turning bits on from left to right.

Example:
/28

11111111.11111111.11111111.11110000

This becomes:

255.255.255.240

The value 240 is simply the decimal translation of 11110000.

---

## Important Clarification
The mask is not built from host counts or subnet counts.

The mask comes only from the prefix.

Example:
/28 = 28 ones followed by zeros

That gives:
255.255.255.240

Counts such as:
- 2^4 = 16 subnets
- 2^4 = 16 total addresses

help describe capacity, but they do not build the mask itself.

---

## Why 256 Is Used
When calculating block size in an octet, use 256, not 255.

Reason:
- 0 through 255 gives 256 total values

Example:
256 - 4 = 252

So for /22:
255.255.252.0 is correct

Do not subtract 1 when building the subnet mask.

The minus 1 rule belongs to broadcast calculations, not mask creation.

---

## Valid Subnet Mask Values
Subnet mask octets must follow continuous binary 1s and then 0s.

Valid values:
0, 128, 192, 224, 240, 248, 252, 254, 255

Example:
- 252 = valid
- 251 = invalid

This is why 255.255.252.0 is valid and 255.255.251.0 is not.

---

## /24 vs /28 vs /22

### /24
11111111.11111111.11111111.00000000
= 255.255.255.0

This is often the original full network before subdivision.

### /28
11111111.11111111.11111111.11110000
= 255.255.255.240

This means the network has been divided into smaller subnets.

### /22
11111111.11111111.11111100.00000000
= 255.255.252.0

This groups addresses in blocks of 4 in the third octet.

---

## Block Size Understanding
For 255.255.252.0:

Block size in the third octet is:
256 - 252 = 4

This creates subnet starting points like:
0, 4, 8, 12, 16 ... 252

These are not one continuous range from 0 to 252.

They are stepping points for subnet boundaries.

---

## 📝 Key Concepts Learned
- Subnetting defines the boundary of a network
- A subnet mask separates network bits from host bits
- Devices must share the same network portion to communicate directly
- The subnet mask is built from the prefix length
- 256 is used for block size calculations because an octet contains 256 values
- Subnet mask octets must follow valid continuous binary patterns
- Different networks require routing to communicate

---

## 🔁 Practical Reinforcement
- Rebuilt the topology from memory
- Tested communication within the same subnet
- Broke communication by placing devices in different networks
- Strengthened understanding of masks, prefixes, and boundaries
- Clarified the difference between mask creation, host counts, subnet counts, and block size

---

## ✅ Outcome
Developed a stronger understanding of subnet masks, network boundaries, and how IP ranges determine direct communication.

This lab helped shift subnetting from memorization to structured understanding.
