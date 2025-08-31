# 🔒 Linux Firewall Configuration with `iptables`

## 📝 Lab Summary
Configured firewall rules on Linux using `iptables` to secure a two-tier application environment.  
Enforced least privilege access, restricted network exposure, and validated rules as **audit evidence**.  

---

## ✅ Lessons Learned
- Restricted access to network services through firewall guardrails.  
- Installed and configured `iptables` on relevant servers.  
- Allowed specific inbound traffic (**SSH & HTTP**) while denying all others.  
- Controlled outbound connections to database and repository servers.  
- Verified rules via CLI for traceable compliance evidence.  

---

## 📑 Compliance Mapping

**ISO/IEC 27001:2022 Annex A**  
- **A.5.15** – Access control  
- **A.5.18** – Preventing unauthorized access  
- **A.8.20** – Network security controls  
- **A.8.21** – Secure system configuration  

**NIST Cybersecurity Framework / SP 800-53**  
- **PR.AC-4** – Access to assets restricted  
- **AC-03** – Access enforcement  
- **AC-03(11)** – Control of remote access  
- **AC-24** – Access control decisions  

---

## 🛡️ Risk Mitigation Mapping

| Scenario / Risk                                   | Control Applied | Mitigation Outcome |
|--------------------------------------------------|----------------|--------------------|
| Unrestricted SSH access could allow brute-force attacks | PR.AC-4 / A.5.15 | Limited SSH to a known source IP only |
| Open HTTP port exposed to all networks            | AC-03 / A.8.20 | Restricted web access to trusted source IPs |
| Outbound connections to unauthorized destinations | AC-24 / A.5.18 | Dropped all outbound traffic except approved DB and Repo servers |
| Default “allow all” inbound traffic               | AC-03(11) / A.8.21 | Enforced DROP as baseline policy, reducing attack surface |
| Lack of audit evidence for firewall enforcement   | PR.AC-4 / A.5.15 | Captured rules with `iptables -L -v --line-numbers` for audits |

---

## 🔑 Key Takeaways
- Firewall configuration is **system hardening** — adds a protective layer.  
- Directly enforced **least privilege access** at OS level.  
- Reduced attack surface by allowing only necessary inbound/outbound traffic.  
- Created **traceable compliance guardrails** mapped to ISO 27001 & NIST controls.  
- Demonstrated ability to provide **evidence for audits** in real-world scenarios.  

---
