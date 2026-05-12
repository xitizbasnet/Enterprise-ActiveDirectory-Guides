# DNS Management Basics

## 📘 Overview

**Objective:** Create and manage DNS records for domain services
**Estimated Time:** 25 minutes

---

# 🖧 DNS Management Procedures

## 1. Open DNS Manager

Open the DNS management console from the domain controller.

### Steps

1. Open **Server Manager**
2. Navigate to:

```text
Tools → DNS
```

### Purpose

This console is used to manage DNS zones, records, and name resolution services within the domain environment.

---

## 2. Expand Forward Lookup Zones

Navigate to the appropriate domain zone.

### Steps

1. In the DNS Manager console, expand:

```text
Forward Lookup Zones
```

2. Select your domain zone.

### Purpose

Forward Lookup Zones are used to resolve hostnames to IP addresses.

---

## 3. Create an A Record

Create a Host (A) record to map a hostname to an IPv4 address.

### Steps

1. Right-click inside the selected DNS zone.
2. Select:

```text
New Host (A or AAAA)
```

3. Enter:

   * **Hostname**
   * **IP Address**

4. Click **Add Host**.

### Example

```text
Hostname: webserver
IP Address: 192.168.1.10
```

### Purpose

A records allow devices and services to locate systems using hostnames instead of IP addresses.

---

## 4. Create a CNAME Record

Create an alias record for a service or hostname.

### Steps

1. Right-click inside the DNS zone.
2. Select:

```text
New Alias (CNAME)
```

3. Create an alias for the target service or host.

### Example

```text
Alias Name: ftp
Fully Qualified Domain Name (FQDN): server01.yourdomain.com
```

### Purpose

CNAME records provide alternate names for existing host records.

---

## 5. Create an MX Record

Create a Mail Exchanger (MX) record for email routing.

### Steps

1. Right-click inside the DNS zone.
2. Select:

```text
Other New Records
```

3. Choose:

```text
Mail Exchanger (MX)
```

4. Add the mail server details.

### Example

```text
Mail Server: mail.yourdomain.com
Priority: 10
```

### Purpose

MX records direct email traffic to designated mail servers.

---

## 6. Create an SRV Record

Create a Service Location (SRV) record for service discovery.

### Steps

1. Right-click inside the DNS zone.
2. Select:

```text
Other New Records
```

3. Choose:

```text
Service Location (SRV)
```

4. Define:

   * Service
   * Protocol
   * Port Number
   * Target Host

### Example

```text
Service: _sip
Protocol: _tcp
Port: 5060
Target: voipserver.yourdomain.com
```

### Purpose

SRV records help clients locate network services automatically.

---

# 🧪 DNS Testing & Validation

## 7. Test DNS Resolution

Verify hostname resolution using the `nslookup` command.

### Command

```bash
nslookup hostname.yourdomain.com
```

### Purpose

Confirms that DNS records resolve correctly to the expected IP address.

---

## 8. Test Reverse Lookup

Verify reverse DNS (PTR) resolution.

### Command

```bash
nslookup -type=PTR 192.168.1.x
```

### Purpose

Confirms that IP addresses resolve back to hostnames correctly.

---

## 9. Check DNS Event Logs

Review DNS-related logs for warnings or errors.

### Steps

1. Open **Event Viewer**
2. Navigate to:

```text
Applications and Services Logs → DNS Server
```

3. Review logs for:

   * Query failures
   * Replication issues
   * Configuration errors

### Purpose

Helps identify DNS-related operational issues and troubleshooting information.

---

# ✅ Best Practices

## 🔹 DNS Management Best Practices

* Maintain consistent naming conventions.
* Use lowercase for DNS records.
* Test all records after creation.
* Document DNS changes for auditing purposes.
* Regularly review DNS event logs.
* Remove stale or unused records periodically.

---

# 📌 Summary

This guide covered the essential DNS management tasks required for maintaining domain name services within a Windows Server environment, including:

* Creating A, CNAME, MX, and SRV records
* Performing DNS resolution tests
* Verifying reverse lookups
* Reviewing DNS event logs
* Applying DNS administration best practices
