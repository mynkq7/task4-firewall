Task 4 – Firewall Configuration with UFW
Objective:
Configure and test basic firewall rules to allow or block traffic.

Tools:

Windows Firewall (not used in this demo)

UFW (Uncomplicated Firewall) on Linux (Kali)

Deliverables:

Screenshot/configuration file showing firewall rules applied

What is UFW?
The Uncomplicated Firewall (UFW) is a user-friendly front-end for managing the Netfilter firewall (iptables) on Linux.
It simplifies setting up a host-based firewall by providing an easy-to-use command-line interface, allowing users to manage network traffic rules without deep iptables knowledge.

Installing UFW

bash
Copy
Edit
sudo apt update
sudo apt -y install ufw
Enabling UFW

bash
Copy
Edit
sudo ufw enable
Output:

bash
Copy
Edit
Firewall is active and enabled on system startup
Checking Current Rules

bash
Copy
Edit
sudo ufw status numbered
Initially shows no custom rules.

Blocking Telnet (Port 23)

bash
Copy
Edit
sudo ufw deny 23
Output:

bash
Copy
Edit
Rule added
Rule added (v6)
Allowing SSH (Port 22)

bash
Copy
Edit
sudo ufw allow 22
Output:

bash
Copy
Edit
Rule added
Rule added (v6)
Viewing Updated Rules

bash
Copy
Edit
sudo ufw status numbered
Example output:

bash
Copy
Edit
[ 1] 23                         DENY IN     Anywhere
[ 2] 22                         ALLOW IN    Anywhere
[ 3] 23 (v6)                    DENY IN     Anywhere (v6)
[ 4] 22 (v6)                    ALLOW IN    Anywhere (v6)
Testing the Rules
Using nc (Netcat) to check connectivity:

bash
Copy
Edit
nc -vz localhost 22
nc -vz localhost 23
Output:

bash
Copy
Edit
localhost [127.0.0.1] 22 (ssh) : Connection refused
localhost [127.0.0.1] 23 (telnet) : Connection refused
Note: Localhost tests may still show “open” or “connection refused” because UFW allows loopback traffic by default. External connections to port 23 would be blocked.

Removing the Test Block Rule

bash
Copy
Edit
sudo ufw delete deny 23
sudo ufw delete deny 23 (v6)
Or by number:

bash
Copy
Edit
sudo ufw delete 1
sudo ufw delete 3
Final check:

bash
Copy
Edit
sudo ufw status numbered
Summary – How a Firewall Filters Traffic
A firewall is essentially a traffic filter. It checks incoming and outgoing packets against a set of predefined rules:

If the traffic matches an allow rule, it is permitted.

If it matches a deny rule, it is blocked.

If there is no matching rule, the firewall applies its default policy (usually deny for inbound).

Firewalls help secure systems by limiting unnecessary or dangerous network access.

