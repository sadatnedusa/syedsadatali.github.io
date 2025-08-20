## Walk through a **practical workflow example** of
**“Using SBOM and sandboxing for improved 3rd party management.”**

---

## 🔹 Example Scenario: A company receives a 3rd-party analytics tool

### **Step 1. Vendor provides software**

* Vendor ships `analytics_tool_v1.2.tar.gz`
* You don’t know what’s inside (libraries, versions, etc.)

---

### **Step 2. Generate SBOM**

* Use tools like **Syft, SPDX, CycloneDX** to generate an SBOM.

```bash
syft packages analytics_tool_v1.2.tar.gz -o cyclonedx-json > sbom.json
```

👉 Output:

* Lists all components, e.g.:

  * Python 3.9.7
  * Flask 2.0.1
  * OpenSSL 1.0.2

---

### **Step 3. Check vulnerabilities**

* Feed the SBOM into a vulnerability scanner (e.g. **Grype, Anchore, Dependency-Track**).

```bash
grype sbom:sbom.json
```

👉 Output:

* ⚠️ OpenSSL 1.0.2 → known CVE (CVE-2016-2107, critical)
* Flask 2.0.1 → medium risk CVE

---

### **Step 4. Decide risk strategy**

* You **can’t upgrade** vendor’s software directly.
* But you now **know the risks**.
* Action: run it in a **restricted environment** (sandbox).

---

### **Step 5. Sandbox the application**

* Use Docker (or Podman) to run it with **minimal privileges**:

```bash
docker run --rm -it \
  --security-opt no-new-privileges \
  --cap-drop ALL \
  --read-only \
  -v /data:/data:ro \
  analytics_tool:v1.2
```

🔒 Restrictions applied:

* No root privileges.
* No filesystem writes except `/data`.
* No extra Linux capabilities.
* Read-only filesystem.

---

### **Step 6. Monitoring and auditing**

* Monitor container with **Falco** or audit logs.
* Track SBOM over time — if new CVEs appear, get alerts.
* Decide if vendor must upgrade before production rollout.

---

## ✅ Benefits

* **SBOM**: Full visibility → you know exactly what’s inside.
* **Sandboxing**: Containment → even if vulnerable, it can’t escape easily.
* **Together**: Stronger 3rd party risk management than trust alone.

---

👉 In real organizations, this workflow fits into a **CI/CD pipeline**:

1. Vendor software received → auto-generate SBOM
2. Scan for CVEs → block if critical
3. Deploy in sandbox/container with least privilege
4. Monitor and track SBOM updates

---

