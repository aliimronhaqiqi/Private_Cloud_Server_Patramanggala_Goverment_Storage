# Native Web Application Firewall

## Overview

Patramanggala Cloud implements a lightweight Native Web Application Firewall (WAF) using HAProxy Access Control Lists (ACL).

Unlike ModSecurity, this implementation relies on native HAProxy features to filter malicious requests before they reach the Nextcloud application.

The primary objectives are to reduce unnecessary resource consumption while maintaining essential protection against common web attacks.

---

# Architecture

```
Client

↓

HTTPS

↓

HAProxy Reverse Proxy

↓

Native WAF (ACL)

↓

Nextcloud Cluster

↓

MariaDB / Redis
```

---

# Protection Features

The implemented protections include:

- HTTP Method Filtering
- Hidden File Protection
- Sensitive Directory Protection
- Scanner Detection
- Request Rate Limiting
- Security Response Headers

---

# Advantages

- Lightweight
- No additional WAF container
- Integrated directly into HAProxy
- Easy to maintain
- Low memory usage
- Fast request processing

---

# Repository Structure

```
waf/

├── README.md

├── acl/

└── tests/
```

---

# Related Documentation

- docs/Security.md
- docs/Architecture.md
- docs/Troubleshooting.md

---

# Future Improvements

Planned enhancements include:

- OWASP Core Rule Set integration
- GeoIP filtering
- IP reputation blocking
- Advanced bot detection
- Centralized logging
