# Azure notes

**Azure Training Notes**

#### **Day 1: Active Directory (AD) Fundamentals**

**Forest in AD**

* A _Forest_ in Active Directory (AD) is a **security boundary** with a **trust relationship**.
* It is represented by a **triangle**.
* The **first domain** created is called the **Forest Root Domain** (all paths lead back to it).
* **Only one root domain** exists per forest.
* Key administrative groups include:
  * _Enterprise Admins_
  * _Schema Admins_

**Logical and Physical Components**

* Logical and physical components work together to define AD structure.

**Child Domains**

* Used to create multiple domains under the same forest.
* The **second domain** added to the forest is considered a child domain.
* Child domains inherit their parent’s name.
  * Example: `RSA.UHD.COM` and `EUR.UHD.COM`.
* Useful for **accommodating different legal and regulatory requirements** across geographic regions.

**Trust Relationships**

* Trust is a **software connection** that links two entities.
* Allows child domains to access resources across trust relationships.

**Schema**

* Controls how Active Directory objects are structured.
* **Classes** define object types (e.g., user objects).
* **Attributes** define properties (e.g., first name, last name).
* Stored in the **schema** and dynamically updatable.
* Updates can be performed by applications such as **Microsoft Exchange**.
* The schema acts as a **rulebook** for AD structure.

**Operations Master Roles (FSMO Roles)**

* There are **five** operations master roles:
  1. **Schema Master**
  2. **Domain Naming Master**
  3. **RID Master**
  4. **PDC Emulator**
  5. **Infrastructure Master**
* The first domain controller (DC) in a forest holds all five roles by default.
* If a role fails, certain AD functions may be impacted (e.g., inability to create user accounts).

**Global Catalog (GC)**

* A **search feature** that helps locate objects across the entire forest.

**Domain Partitions**

* Information is replicated within **domain partitions**.

**Sites in AD**

* Defined as **one or more domain controllers** within **well-connected subnets**.
* Helps **optimize authentication** and **replication traffic**.
* Example: Separate sites for Bournemouth and Poole.
* **IP addresses determine site membership**, and **DNS helps locate the correct subnet**.

**Server Configuration Best Practices**

* Always configure a **static IP address** for domain controllers.
* Carefully choose the **server role** before adding it.
* **Avoid modifying ADSI Edit** unless necessary.
* Key team member managing AD: _Lee Oliver_.

**Azure AD Connect (AAD Connect)**

* Synchronizes **on-premises AD with Azure AD**.
* Runs on a **server** and **syncs users, passwords, and attributes**.
* Provides **seamless sign-in experience** for hybrid environments.
* Once set up, **leave it running without changes**.

***

#### **Day 2: Advanced AD & DHCP**

**Domain Controller (Additional DC)**

* Must have a **static IP**.
* Use _Add Roles and Features_ to install necessary roles.
* Some roles require a **reboot**.
* After installation, use _Promote this server to a domain controller_.
* All domain controllers should:
  * Run **DNS**.
  * Be **Global Catalog servers**.

**DHCP (Dynamic Host Configuration Protocol)**

* **Assigns IP addresses** dynamically.
* Has remained mostly unchanged for 20+ years.
* Essential for network communication.
* Requires **Enterprise Admin** permissions to prevent unauthorized servers.

**DHCP Setup & Scopes**

* After installation, **configure a scope**:
  * Right-click _IPv4_ > _New Scope_.
  * Assign **subnet and exclusions**.
  * Configure **gateway** to allow communication beyond local subnet.
  * _Ignore WINS settings_ (legacy technology).
* One scope is usually enough.

**DHCP Reservations**

* Allows specific devices to get **fixed IP addresses**.
* Requires **MAC address** of the client (`arp -a`).
* To apply:
  1. Add MAC address and reserve the IP.
  2. On client machine, use `ipconfig /release` and `ipconfig /renew`.

**Common DHCP Commands**

* `ipconfig /release` – Releases current IP.
* `ipconfig /renew` – Requests new IP.
* `ipconfig /flushdns` – Clears DNS cache.

***

#### **Day 3: DNS & Azure Integration**

**DNS (Domain Name System)**

* **Critical** for network operations.
* Converts **hostnames to IP addresses** and vice versa.
* Used by **Active Directory**.
* **SRV Records** are needed for **AD functionality**.
* _Common troubleshooting step:_ If `ping domainname.com` works but `ping IP` fails, it’s likely a **DNS issue**.

**Reverse Lookup Zones**

* Used to resolve **IP addresses to hostnames**.
* Example: `nslookup 192.168.1.1`.
* Uses **PTR (Pointer) records**.

**External Domains & Root Hints**

* External queries use **Root Hints** if no local DNS record is found.
* Uses **iterative queries** to find the best possible match.

**Azure AD Connect (AAD Connect)**

* Syncs **on-prem AD with Azure AD**.
* Can be managed via **admin.microsoft.com**.

**Microsoft 365 Admin Center**

* **Central hub** for managing Microsoft services.
* **Default role:** User (no admin access).
* **Global Admin:** Full control over tenant.
* **MFA is mandatory** for all admin roles.

**Windows Autopilot**

* Automates device provisioning.
* **Requires a CSV file** uploaded to Endpoint Manager.
* Cannot be used on **Virtual Machines**.

**O365 Groups**

* Designed for **collaboration**.
* Each group gets **email, calendar, and storage**.
* Can be **private or public**.

**Azure AD Licensing (P1 vs. P2)**

* **P1:** Basic identity management.
* **P2:** Advanced features (e.g., _Privileged Identity Management_).

**Conditional Access Policies**

* Used to enforce security conditions.
* **Careful!** Misconfiguring a policy can lock everyone out.

**Password Reset Policies**

* Users can reset their own passwords if enabled.

***

#### **Key Networking & Troubleshooting Concepts**

**TCP/IP Fundamentals**

* The **core protocol** of the internet.
* Name resolution methods:
  * **NetBIOS** (legacy, broadcast-based)
  * **DNS** (modern, hierarchical)

**IP Addressing & Subnetting**

* **Static vs. Dynamic IPs**
* **Subnet masks** define network boundaries.
* **Default Gateway** allows inter-network communication.

**Common IP Commands**

* `ipconfig /all` – View all network settings.
* `ping 8.8.8.8` – Check internet connectivity.
* `tracert <IP>` – Trace route to a server.

***

This document provides a **comprehensive guide** to **Azure AD, DHCP, DNS, and networking concepts**, ensuring a solid foundation for managing **on-prem and cloud-based IT environments**.
