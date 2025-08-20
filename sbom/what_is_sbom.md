##  **“Using the SBOM and sandboxing for improved 3rd party management”** combines two modern software security practices that organizations use to **manage risks from third-party software**. 
- Let’s break it down:

---

### 1. **SBOM (Software Bill of Materials)**

* Think of an SBOM like a **nutrition label for software**.
* It’s a formal, machine-readable list of all the components (open-source libraries, dependencies, frameworks, vendor software, etc.) inside an application.
* Helps answer:

  * *What third-party software are we using?*
  * *What version?*
  * *Does it have known vulnerabilities (CVEs)?*
  * *Are we compliant with licensing obligations?*

🔹 Example: If you use a vendor’s app and it ships with **OpenSSL v1.0.2**, your SBOM will flag that — then you’ll know it’s outdated and vulnerable.

---

### 2. **Sandboxing**

* Sandboxing means running third-party software in a **restricted environment** where it has **limited permissions and isolated resources**.
* Even if the third-party code is malicious or compromised, it can’t easily affect the rest of your system.
* Techniques:

  * Containers (Docker, Podman)
  * Virtual machines
  * OS-level sandboxing (AppArmor, SELinux, seccomp, Windows Sandbox)

🔹 Example: Running a PDF reader inside a sandbox prevents a malicious PDF from infecting your entire workstation.

---

### 3. **Improved 3rd Party Management**

When combined:

* **SBOM** gives **visibility** → You know *what’s inside* every vendor’s software.
* **Sandboxing** gives **control** → You contain untrusted or high-risk software, reducing blast radius if something goes wrong.

Together, they improve **third-party risk management** by:

* Identifying vulnerabilities in vendor-provided code (via SBOM).
* Reducing trust assumptions by running it in isolated environments (via sandboxing).
* Meeting compliance/regulatory requirements (e.g., U.S. Executive Order on SBOMs, EU Cyber Resilience Act).
* Limiting potential supply chain attacks.

---

✅ **In simple words:**
*"Using SBOM + sandboxing means: know exactly what’s in the third-party software you use, and run it in a safe, restricted environment so if it’s risky, it can’t harm the rest of your systems."*

---

