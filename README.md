# Vulnerability Management Program Implementation

In this project, we implementated a comprehensive vulnerability management program, from inception to completion.

_**Inception State:**_ the organization has no existing policy or vulnerability management practices in place.

_**Completion State:**_ a formal policy is enacted, stakeholder buy-in is secured, and a full cycle of organization-wide vulnerability remediation is successfully completed. <br>

---

<img align="center" width="800" alt="image" src="https://github.com/user-attachments/assets/cfc5dbcf-3fcb-4a71-9c13-2a49f8bab3e6">

# Technology Utilized
- Tenable (enterprise vulnerability management platform)
- Azure Virtual Machines (Nessus scan engine + scan targets)
- PowerShell & BASH (remediation scripts)  <br>

---


# Table of Contents

- [Vulnerability Management Policy Draft Creation](#vulnerability-management-policy-draft-creation)
- [Meeting: Policy Buy-In (Stakeholders)](#step-2-meeting-policy-buy-in-stakeholders)
- [Policy Finalization and Senior Leadership Sign-Off](#step-3-policy-finalization-and-senior-leadership-sign-off)
- [Meeting: Initial Scan Permission (Server Team)](#step-4-meeting-initial-scan-permission-server-team)
- [Initial Scan of Server Team Assets](#step-5-initial-scan-of-server-team-assets)
- [Vulnerability Assessment and Prioritization](#step-6-vulnerability-assessment-and-prioritization)
- [Distributing Remediations to Remediation Teams](#step-7-distributing-remediations-to-remediation-teams)
- [Meeting: Post-Initial Discovery Scan (Server Team)](#step-8-meeting-post-initial-discovery-scan-server-team)
- [CAB Meeting: Implementing Remediations](#step-9-cab-meeting-implementing-remediations)
- [Remediation Round 1: Outdated Wireshark Removal](#remediation-round-1-outdated-wireshark-removal)
- [Remediation Round 2: Insecure Protocols & Ciphers](#remediation-round-2-insecure-protocols--ciphers)
- [Remediation Round 3: Guest Account Group Membership](#remediation-round-3-guest-account-group-membership)
- [Remediation Round 4: Windows OS Updates](#remediation-round-4-windows-os-updates)
- [First Cycle Remediation Effort Summary](#first-cycle-remediation-effort-summary)  <br> <br>
---

### Vulnerability Management Policy Draft Creation

This phase focuses on drafting a Vulnerability Management Policy as a starting point for stakeholder engagement. The initial draft outlines scope, responsibilities, and remediation timelines, and may be adjusted based on feedback from relevant departments to ensure practical implementation before final approval by upper management.  <br><br>
[Draft Policy](https://docs.google.com/document/d/1CLSWm1_9JL1oUqgyNNwtPXW6FzXJ7ddVnSAUQTyqC8I/edit?usp=drive_link)  <br> <br>

---

### Step 2) Meeting: Policy Buy-In (Stakeholders)

In this phase, a meeting with the server team introduces the draft Vulnerability Management Policy and assesses their capability to meet remediation timelines. Feedback leads to adjustments, like extending the critical remediation window from 48 hours to one week, ensuring collaborative implementation.


<details>
<summary><strong>Click to expand meeting example transcript </strong></summary>
<br>

**Marco:**  
Good morning, Logan. How have things been? I know the past few weeks have been especially busy.

**Logan:**  
Good morning, Marco. It’s been a bit hectic, but we’re managing. I reviewed the policy draft, and overall it looks good. However, with our current staffing, we won’t be able to meet the aggressive remediation timelines—particularly the 48-hour window for critical vulnerabilities.

**Marco:**  
I understand. The timeline *is* aggressive. Maybe we extend the critical window to one week and reserve 48 hours for severe zero-days.

**Logan:**  
That sounds reasonable. We appreciate the flexibility. Could we also have some leeway during the initial rollout?

**Marco:**  
Absolutely. Once finalized, we’ll start the program but allow six months for departments to adapt.

**Logan:**  
That works for us. Thanks for including us—it helps us feel like part of the solution.

**Marco:**  
Of course. We’re all in this together.

**Logan:**  
Thanks for the quick meeting.

**Marco:**  
My favorite kind. Take care.

</details> <br>


---

### Step 3) Policy Finalization and Senior Leadership Sign-Off

After gathering feedback from the server team, the policy is revised, addressing aggressive remediation timelines. With final approval from upper management, the policy now guides the program, ensuring compliance and reference for pushback resolution.  <br><br>
[Finalized Policy](https://docs.google.com/document/d/1QydHEdb3mXx5FdJ5HIZyEoOHfdtefMzNZaFIAdL_bF0/edit?usp=sharing)
<div style="text-align: center;">
    
</div> <br>

---

### Step 4) Meeting: Initial Scan Permission (Server Team)

The team collaborates with the server team to initiate scheduled credential scans. A compromise is reached to scan a single server first, monitoring resource impact, and using just-in-time Active Directory credentials for secure, controlled access.  


<details>
<summary><strong>Click to expand meeting example transcript </strong></summary>

<br>

**Marco:**  
Good morning, Logan. I heard you’re ready to conduct some scans.

**Logan:**  
Yep. Now that our vulnerability management policy is in place, I wanted to get started on running scheduled credentialed scans of your environment.

**Marco:**  
Sounds good to me. What’s involved? How can we help?

**Logan:**  
We’re planning to schedule weekly scans of the server infrastructure. We estimate it’ll take about 4–6 hours to scan all 2,200 assets. We’ll need you to provide administrative credentials so the scan engine can remotely log into the targets and perform a deeper assessment.

**Marco:**  
Whoa, hold on. What exactly does scanning entail? I’m a bit worried about resource utilization. Also—you want admin credentials to all 2,200 machines? That doesn’t sound safe.

**Logan:**  
Those are valid concerns. The scan engine sends different types of traffic to the servers to check for certain vulnerabilities. This includes reviewing registry keys, checking for outdated software, and identifying insecure protocols or cipher suites. That’s why credentials are required.

**Marco:**  
I see. As long as it doesn’t bring the servers offline, we should be fine.

**Logan:**  
Absolutely. Let’s start by scanning a single server for now and monitor resource utilization.

**Marco:**  
Not a bad idea. Also, for the credentials — can you set something up in Active Directory for us? Maybe create an account and leave it disabled until we're ready to scan. During the scan, we can enable it, then disable or deprovision it afterward. Kind of like a just-in-time access model.

**Logan:**  
That sounds good. I’ll ask Susan to begin automating the account provisioning process.

**Marco:**  
Awesome. Talk soon.

**Logan:**  
Sounds good. I’ll get back to you once the credentials are set up. See you later.

**Marco:**  
See you later.

</details> <br>


---

### Step 5) Initial Scan of Server Team Assets

In this phase, an insecure Windows Server is provisioned to simulate the server team's environment. After creating vulnerabilities, an authenticated scan is performed, and the results are exported for future remediation steps.  





---

### Step 6) Vulnerability Assessment and Prioritization

We assessed vulnerabilities and established a remediation prioritization strategy based on ease of remediation and impact. The following priorities were set:

1. Third Party Software Removal (Wireshark)
2. Windows OS Secure Configuration (Protocols & Ciphers)
3. Windows OS Secure Configuration (Guest Account Group Membership)
4. Windows OS Updates  <br> <br>

---

### Step 7) Distributing Remediations to Remediation Teams

The server team received remediation scripts and scan reports to address key vulnerabilities. This streamlined their efforts and prepared them for a follow-up review.  

<img width="635" alt="image" src="https://github.com/user-attachments/assets/bbf9478f-e1d1-4898-846e-b510ec8c6f72">

<br> <br>

---

### Step 8) Meeting: Post-Initial Discovery Scan (Server Team)

The server team reviewed vulnerability scan results, identifying outdated software, insecure accounts, and deprecated protocols. The remediation packages were prepared for submission to the Change Control Board (CAB). 


<details>
<summary><strong>Click to expand meeting example transcript </strong></summary>

<br>

**Marco:**  
Morning, Logan. How are you doing?

**Logan:**  
Not bad for a Monday. And you?

**Marco:**  
I'm still alive so I can’t complain. Before we get into the vulnerabilities — how did the actual scan go on your end? Any outages or overutilization?

**Logan:**  
The scan went well. We monitored everything and aside from the open connections, you wouldn’t have known a scan was running.

**Marco:**  
Yeah, that’s good news. I expected as much. We’ll keep monitoring moving forward, but I don’t think we’ll have any resource utilization issues. Mind if I dive into the findings?

**Logan:**  
Yeah, absolutely.

**Marco:**  
Cool — I’m going to share my screen real quick. So, basically, the majority of these vulnerabilities come from Wireshark being installed. It’s just super out-of-date. You can see all these Wireshark-related findings for that reason.

**Marco:**  
One interesting thing I found is the local guest account on the servers actually belongs to a group — and after checking, it belongs to the **Local Administrators** group. Not sure why that is.

**Marco:**  
Some of these other findings might be resolved automatically by Windows Updates. For example, this Microsoft Edge Chromium one, and possibly this other one. Not entirely sure yet.

**Marco:**  
We also don’t need to worry about the self-signed certificate finding — that’s just the machine signing itself.

**Marco:**  
But the medium-strength cipher suites and TLS 1.0 / 1.1 — those are deprecated protocols and should definitely be remediated.

**Marco:**  
So basically: remove Wireshark, disable/remove the guest account, and fix the cipher suites and deprecated protocols.

**Logan:**  
Very interesting. The good news is I suspect most of our servers have the same vulnerabilities. Hopefully that makes remediation easier.

**Marco:**  
Yeah, that’s actually great — a uniform rollout. Do you foresee any issues with fixing the cipher suites or insecure protocols?

**Logan:**  
I highly doubt it. We'll run everything through the next Change Control Board. Uninstalling Wireshark and fixing the guest account shouldn’t be an issue — those shouldn’t be on the servers anyway. I’ll talk to our CIS admins about that.

**Marco:**  
Perfect. I’ll start building remediation packages to make things easier when it’s time to implement.

**Logan:**  
That sounds great. Oh — do you already have something in place to fix the Windows Update-related vulnerabilities? Patch management, I mean.

**Marco:**  
Oh yes, I'm not worried about those. Windows Update should handle them automatically by next week — we already have patch management in place.

**Logan:**  
Excellent.

**Marco:**  
All right, I’ll start researching the best ways to remediate these findings and get back to you before the next Change Control Board.

**Logan:**  
Sounds good. Talk to you soon.

**Marco:**  
Cool, talk to you soon.

</details>  <br>

---

### Step 9) CAB Meeting: Implementing Remediations

The Change Control Board (CAB) reviewed and approved the plan to remove insecure protocols and cipher suites. The plan included a rollback script and a tiered deployment approach.  


<details>
<summary><strong>Click to expand meeting example transcript </strong></summary>

<br>

**Josh CAB:**  
Okay, next up on the list are a couple of vulnerability remediations for the server team:  
1) Removal of insecure protocols  
2) Removal of insecure cipher suites  

It looks like Marco from the Risk Department is working in conjunction with Logan from Infrastructure on this. Logan, do you want to walk us through the technical aspects of the change being implemented?

**Logan (Infrastructure):**  
Normally I would, but do you mind giving this one to Marco? He actually built the solution for us — we're still getting used to the process.

**Marco (Risk Dept):**  
Yeah, I can explain these. So — insecure cipher suites and protocols: their presence on the system means the machine is capable of negotiating and using deprecated algorithms or protocols.  

If it connects to a server that only supports those older protocols, the computer might fall back to them. These settings are controlled through the Windows Registry.

It’s a simple fix — we wrote a PowerShell script that disables all insecure protocols and cipher suites, and enables the modern, secure standards.

**Jonathan CAB:**  
That sounds good, but what if something goes wrong? Do we have a rollback plan in place?

**Marco (Risk Dept):**  
Yes, absolutely.  
First, we’re doing a **tiered deployment** — a pilot group, pre-production, and then production.  
On top of that, we built **automated rollback scripts** for each remediation.

If something unexpected happens, the script can restore the original protocols and cipher settings.

**Jonathan CAB:**  
Okay, that sounds good. Since the fixes are simple registry updates, I’m not too concerned.

**Marco (Risk Dept):**  
Yep, exactly. Straightforward.

**Josh CAB:**  
Any more questions from anyone?

*— Silence —*

Great, that wraps things up for this week’s CAB meeting. See you all next week.

**Marco:**  
See you later.

</details>  <br>


---
### Step 10 ) Remediation Effort

#### Remediation Round 1: Outdated Wireshark Removal

The server team used a PowerShell script to remove outdated Wireshark. A follow-up scan confirmed successful remediation.  
[Wireshark Removal Script](https://github.com/joshmadakor1/lognpacific-public/blob/main/automation/remediation-wireshark-uninstall.ps1)  




#### Remediation Round 2: Insecure Protocols & Ciphers

The server team used PowerShell scripts to remediate insecure protocols and cipher suites. A follow-up scan verified successful remediation, and the results were saved for reference.  
[PowerShell: Insecure Protocols Remediation](https://github.com/joshmadakor1/lognpacific-public/blob/main/automation/toggle-protocols.ps1)
[PowerShell: Insecure Ciphers Remediation](https://github.com/joshmadakor1/lognpacific-public/blob/main/automation/toggle-cipher-suites.ps1)




#### Remediation Round 3: Guest Account Group Membership

The server team removed the guest account from the administrator group. A new scan confirmed remediation, and the results were exported for comparison.  
[PowerShell: Guest Account Group Membership Remediation](https://github.com/joshmadakor1/lognpacific-public/blob/main/automation/toggle-guest-local-administrators.ps1)  




#### Remediation Round 4: Windows OS Updates

Windows updates were re-enabled and applied until the system was fully up to date. A final scan verified the changes  


---

### First Cycle Remediation Effort Summary

The remediation process reduced total vulnerabilities by 80%, from 30 to 6. Critical vulnerabilities were resolved by the second scan (100%), and high vulnerabilities dropped by 90%. Mediums were reduced by 76%. In an actual production environment, asset criticality would further guide future remediation efforts.  

<img width="602" height="373" alt="Screenshot 2025-12-02 at 4 07 42 PM" src="https://github.com/user-attachments/assets/f35779f7-48a2-4f81-90e7-c722ddb21db2" />

---

### On-going Vulnerability Management (Maintenance Mode)

After completing the initial remediation cycle, the vulnerability management program transitions into **Maintenance Mode**. This phase ensures that vulnerabilities continue to be managed proactively, keeping systems secure over time. Regular scans, continuous monitoring, and timely remediation are crucial components of this phase. (See [Finalized Policy](https://docs.google.com/document/d/1QydHEdb3mXx5FdJ5HIZyEoOHfdtefMzNZaFIAdL_bF0/edit?usp=sharing) for scanning and remediation cadence requirements.)

Key activities in Maintenance Mode include:
- **Scheduled Vulnerability Scans**: Perform regular scans (e.g., weekly or monthly) to detect new vulnerabilities as systems evolve.
- **Patch Management**: Continuously apply security patches and updates, ensuring no critical vulnerabilities remain unpatched.
- **Remediation Follow-ups**: Address newly identified vulnerabilities promptly, prioritizing based on risk and impact.
- **Policy Review and Updates**: Periodically review the Vulnerability Management Policy to ensure it aligns with the latest security best practices and organizational needs.
- **Audit and Compliance**: Conduct internal audits to ensure compliance with the vulnerability management policy and external regulations.
- **Ongoing Communication with Stakeholders**: Maintain open communication with teams responsible for remediation, ensuring efficient coordination.

By maintaining an active vulnerability management process, organizations can stay ahead of emerging threats and ensure long-term security resilience.
