# Vulnerability Management Program Implementation

In this project, we simulate the implementation of a comprehensive vulnerability management program, from inception to completion.

_**Inception State:**_ the organization has no existing policy or vulnerability management practices in place.

_**Completion State:**_ a formal policy is enacted, stakeholder buy-in is secured, and a full cycle of organization-wide vulnerability remediation is successfully completed.

---

<img width="1000" alt="image" src="https://github.com/user-attachments/assets/cfc5dbcf-3fcb-4a71-9c13-2a49f8bab3e6">

# Technology Utilized
- Tenable (enterprise vulnerability management platform)
- Azure Virtual Machines (Nessus scan engine + scan targets)
- PowerShell & BASH (remediation scripts)

---


# Table of Contents

- [Vulnerability Management Policy Draft Creation](#vulnerability-management-policy-draft-creation)
- [Mock Meeting: Policy Buy-In (Stakeholders)](#step-2-mock-meeting-policy-buy-in-stakeholders)
- [Policy Finalization and Senior Leadership Sign-Off](#step-3-policy-finalization-and-senior-leadership-sign-off)
- [Mock Meeting: Initial Scan Permission (Server Team)](#step-4-mock-meeting-initial-scan-permission-server-team)
- [Initial Scan of Server Team Assets](#step-5-initial-scan-of-server-team-assets)
- [Vulnerability Assessment and Prioritization](#step-6-vulnerability-assessment-and-prioritization)
- [Distributing Remediations to Remediation Teams](#step-7-distributing-remediations-to-remediation-teams)
- [Mock Meeting: Post-Initial Discovery Scan (Server Team)](#step-8-mock-meeting-post-initial-discovery-scan-server-team)
- [Mock CAB Meeting: Implementing Remediations](#step-9-mock-cab-meeting-implementing-remediations)
- [Remediation Round 1: Outdated Wireshark Removal](#remediation-round-1-outdated-wireshark-removal)
- [Remediation Round 2: Insecure Protocols & Ciphers](#remediation-round-2-insecure-protocols--ciphers)
- [Remediation Round 3: Guest Account Group Membership](#remediation-round-3-guest-account-group-membership)
- [Remediation Round 4: Windows OS Updates](#remediation-round-4-windows-os-updates)
- [First Cycle Remediation Effort Summary](#first-cycle-remediation-effort-summary)

---

### Vulnerability Management Policy Draft Creation

This phase focuses on drafting a Vulnerability Management Policy as a starting point for stakeholder engagement. The initial draft outlines scope, responsibilities, and remediation timelines, and may be adjusted based on feedback from relevant departments to ensure practical implementation before final approval by upper management.  

[Draft Policy](https://docs.google.com/document/d/1dKZhAS2cY65BKnCFbKsFKswdkFmZsQ1QVM8IMyucsr0/edit?tab=t.0)

---

### Step 2) Mock Meeting: Policy Buy-In (Stakeholders)

In this phase, a meeting with the server team introduces the draft Vulnerability Management Policy and assesses their capability to meet remediation timelines. Feedback leads to adjustments, like extending the critical remediation window from 48 hours to one week, ensuring collaborative implementation.

**Wilson:**  
Morning, Jimmy! How’s everything going lately? Feels like it’s been nonstop these last few weeks.

**Jimmy:**  
Morning, Wilson. Yeah, it’s been a little crazy, but we’re managing. Appreciate you checking in.  
I went through the draft policy, it makes sense overall. That said, with where we’re at staffing-wise, hitting those remediation timelines, especially the 48-hour one for criticals... it's going to be tough.

**Wilson:**  
Yeah, I figured that might be a pain point. It is pretty aggressive, especially right out of the gate.  
I'll tel you what, what if we stretched the critical window to a week for now? We could save the 48-hour window for the really nasty stuff, like zero-days for software we currently have.

**Jimmy:**  
That actually sounds like a good middle ground. Thanks for being flexible on this.  
Would it be okay if we also had a little breathing room early on? Just while we get used to the process... maybe the first few months?

**Wilson:**  
Absolutely. Once the policy’s finalized, we’ll officially roll things out, but the plan is to give all the teams around six months to adjust and settle in.  Does that work for you?

**Jimmy:**  
Yeah, that works. We’ll get on it.  
Really appreciate you looping us in on this. Tt helps to feel like we’re part of the solution instead of just reacting to it.

**Wilson:**  
Totally. We’re all trying to pull in the same direction here. Thanks for being open about what you need.

**Jimmy:**  
No problem, and hey, thanks for keeping this meeting short.

**Wilson:**  
Anytime. Short meetings are the best meetings.

**Jimmy:**  
Can’t argue with that. Catch you later!

**Wilson:**  
Have a good day! Bye.

---

### Step 3) Policy Finalization and Senior Leadership Sign-Off

![image](https://github.com/user-attachments/assets/85a75c8b-1a8b-4bd4-8d71-528f49cffe09)

After gathering feedback from the server team, the policy is revised, addressing aggressive remediation timelines. With final approval from upper management, the policy now guides the program, ensuring compliance and reference for pushback resolution. 
 
[Finalized Policy](https://docs.google.com/document/d/1Ees8s1ueW-URcNuc7B3n0RGmzhPNaycNtTAPiZHZEKc/edit?tab=t.0)



</div>

---

### Step 4) Mock Meeting: Initial Scan Permission (Server Team)

The team collaborates with the server team to initiate scheduled credential scans. A compromise is reached to scan a single server first, monitoring resource impact, and using just-in-time Active Directory credentials for secure, controlled access.  

**Wilson:**  
Hey Jimmy, morning!

**Jimmy:**  
Morning, Wilson. I heard you're getting ready to kick off some scans?

**Wilson:**  
Yep, now that we’ve got the vulnerability management policy in place, I figured it’s a good time to start scheduling some credentialed scans of your environment. I also figured I'd do the polite thing and let you know before I start.

**Jimmy:**  
Alright, sounds fair. What’s the process look like? Anything you need from us?

**Wilson:**  
Yeah, so we’re planning to run weekly scans on the server infrastructure. Scanning all 200 assets should take around 4 to 6 hours.  
To do it properly, we’ll need administrative credentials so that way the scan engine can log into each system and get deeper visibility into potential issues.

**Jimmy:**  
Hmm, okay. But what exactly does the scan do? I’m a little concerned about how much load it puts on the servers.  
And you’re asking for admin access to *everything*? That gives me a bit of worry. 

**Wilson:**  
Totally get it. The scanner sends targeted traffic to each system, stuff like checking for known vulnerabilities, out-of-date software, weak protocols, that kind of thing. It also looks at registry settings and installed applications deep on the operating system.  
The credentials just let it access those deeper system details. It’s not actually executing anything destructive or invasive.

**Jimmy:**  
Got it. So it’s more like deep inspection. As long as it’s not going to spike CPU or take anything offline, I think we’re okay with that.

**Wilson:**  
Exactly. We can start small, maybe just scan one system first and monitor how it behaves. That’ll give us both some peace of mind.

**Jimmy:**  
Yeah, I like that. Easier to explain if anything goes sideways.

**Wilson:**  
For sure. Also, on the credential side, can you set up a dedicated account in Active Directory for us? Something we can leave disabled until we’re ready to scan, then enable temporarily and shut off right after?  
Basically a just-in-time access setup.

**Jimmy:**  
Yeah, that works. I’ll have Susan spin something up and we can automate the provisioning piece. I’d rather not keep those accounts live longer than necessary.

**Wilson:**  
Perfect. Appreciate that. I’ll check back once you’ve got it in place, and we’ll get the first scan on the calendar.

**Jimmy:**  
Cool. Thanks for walking through all that—makes a lot more sense now.

**Wilson:**  
Anytime. Talk to you later!

**Jimmy:**  
Later, Wilson.

---

### Step 5) Initial Scan of Server Team Assets

In this phase, an insecure Windows Server is provisioned to simulate the server team's environment. After creating vulnerabilities, an authenticated scan is performed, and the results are exported for future remediation steps.  

![image](https://github.com/user-attachments/assets/a77d0d1b-e95f-4a9d-a4b1-306472fd8faf)

[Scan 1 - Initial Scan](https://drive.google.com/file/d/1c2AEwFQscE3khnZ12iaaJcYt_14c89tc/view?usp=sharing)




---

### Step 6) Vulnerability Assessment and Prioritization

We assessed vulnerabilities and established a remediation prioritization strategy based on ease of remediation and impact. The following priorities were set:

1. Third Party Software Removal (Wireshark, easiest to get rid of)
2. Windows OS Secure Configuration (Protocols & Ciphers, second easiest to get rid of with registry modifications)
3. Windows OS Secure Configuration (Guest Account Group Membership, could be harder if the guest account was being actively used for a legitimate business process). 
4. Windows OS Updates (Updates must be tested first, Windows is known for releasing glitchy patches)

---

### Step 7) Distributing Remediations to Remediation Teams

The server team received remediation scripts and scan reports to address key vulnerabilities. This streamlined their efforts and prepared them for a follow-up review.  

<img width="635" alt="image" src="https://github.com/user-attachments/assets/bbf9478f-e1d1-4898-846e-b510ec8c6f72">

[Remediation Email](https://github.com/joshmadakor1/lognpacific-public/blob/main/misc/remediation-email.md)

---

### Step 8) Mock Meeting: Post-Initial Discovery Scan (Server Team)

The server team reviewed vulnerability scan results, identifying outdated software, insecure accounts, and deprecated protocols. The remediation packages were prepared for submission to the Change Control Board (CAB). 

This is a cleaned-up transcript of a real-world technical conversation between a security analyst (Wilson) and a system administrator (Jimmy). It reflects a follow-up discussion after a vulnerability scan was conducted on a set of internal servers. The conversation focuses on interpreting scan results, planning remediation, and ensuring minimal business impact.

**Wilson:**  
Morning, Jimmy! How’s it going?

**Jimmy:**  
Not bad for a Monday. You?

**Wilson:**  
Still breathing, so no complaints.  
Before we jump into the vulnerabilities, how did the scan go on your end? Any outages, resource spikes, or strange behavior?

**Jimmy:**  
Nope, smooth sailing. We kept an eye on things, and aside from a bunch of open connections, you wouldn’t have known anything was happening.

**Wilson:**  
That’s great to hear. We’ll continue monitoring just in case, but I’m not expecting any issues going forward.  
Mind if we go into the findings?

**Jimmy:**  
Go for it.

**Wilson:**  
Alright. Sharing my screen now.  
Most of the findings trace back to outdated versions of **Wireshark** being installed on several systems. That’s the bulk of it.

**Jimmy:**  
Ah yeah, I figured that might come up.

**Wilson:**  
Also noticed something odd; the local *Guest* account is a member of the **Administrators group** on a few boxes. That definitely shouldn’t be the case.

**Jimmy:**  
Yikes. That sounds bad, I'm surprised that was overlooked.

**Wilson:**  
Yep.  
There are a few vulnerabilities tied to outdated Microsoft Edge Chromium versions and similar stuff that will likely be resolved through **Windows Updates**, so those aren’t as urgent.  
The **self-signed certificate** warnings are also non-critical—it’s just local certs.

**Jimmy:**  
Makes sense.

**Wilson:**  
The stuff we do want to act on:
- Deprecated protocols like **TLS 1.0 / 1.1**
- **Medium-strength cipher suites**
- Removing unnecessary software like **Wireshark**
- Fixing that **Guest account membership**

**Jimmy:**  
Got it. Hopefully the same issues are present across most systems—that’ll make remediation easier.

**Wilson:**  
Exactly. Everything looks pretty uniform, which is great for scripting the fixes.

**Jimmy:**  
Do you anticipate any trouble disabling the older cipher suites and protocols?

**Wilson:**  
Not really. We’ll route it through the next **Change Control Board (CCB)** cycle just in case, but I don’t expect any blowback.  
And uninstalling Wireshark or correcting account permissions should be low-risk. I’ll sync with the CIS admins just to double-check policy.

**Jimmy:**  
Sounds good.

**Wilson:**  
I’ll also put together a set of remediation packages—scripts, steps, documentation—to help streamline the whole process.

**Jimmy:**  
Appreciate that. Quick question, do we have patching in place for those Windows update-related findings?

**Wilson:**  
We do. Patch management is already in place, so updates should roll out automatically by next week.

**Jimmy:**  
Perfect.

**Wilson:**  
Alright. I’ll start building out the remediation plan and check back in before the next CAB.

**Jimmy:**  
Awesome. Talk to you soon.

**Wilson:**  
You got it. See you.

---

### Step 9) Mock CAB Meeting: Implementing Remediations

The Change Control Board (CAB) reviewed and approved the plan to remove insecure protocols and cipher suites. The plan included a rollback script and a tiered deployment approach.  

<a href="https://youtu.be/zOFPkTa9kY8" target="_"><img width="600" src="https://github.com/user-attachments/assets/07164e63-fbce-471a-b469-29a6d41b7bb8"/></a>

[Meeting Video](https://youtu.be/zOFPkTa9kY8)

---
### Step 10 ) Remediation Effort

#### Remediation Round 1: Outdated Wireshark Removal

The server team used a PowerShell script to remove outdated Wireshark. A follow-up scan confirmed successful remediation.  
[Wireshark Removal Script](https://github.com/joshmadakor1/lognpacific-public/blob/main/automation/remediation-wireshark-uninstall.ps1)  

<img width="634" alt="image" src="https://github.com/user-attachments/assets/7b4f9ab2-d230-4458-ac0f-c0ff070ae79a">

[Scan 2 - Third Party Software Removal](https://drive.google.com/file/d/1UiwPPTtuSZKk02hiMyXf31pXUIeC5EWt/view?usp=drive_link)


#### Remediation Round 2: Insecure Protocols & Ciphers

The server team used PowerShell scripts to remediate insecure protocols and cipher suites. A follow-up scan verified successful remediation, and the results were saved for reference.  
[PowerShell: Insecure Protocols Remediation](https://github.com/joshmadakor1/lognpacific-public/blob/main/automation/toggle-protocols.ps1)
[PowerShell: Insecure Ciphers Remediation](https://github.com/joshmadakor1/lognpacific-public/blob/main/automation/toggle-cipher-suites.ps1)

<img width="630" alt="image" src="https://github.com/user-attachments/assets/0e96120d-8ec9-4f76-8e42-79c752200010">

[Scan 3 - Ciphersuites and Protocols](https://drive.google.com/file/d/1Qc6-ezQvwReCGUZNtnva0kCZo_-zW-Sm/view?usp=drive_link)


#### Remediation Round 3: Guest Account Group Membership

The server team removed the guest account from the administrator group. A new scan confirmed remediation, and the results were exported for comparison.  
[PowerShell: Guest Account Group Membership Remediation](https://github.com/joshmadakor1/lognpacific-public/blob/main/automation/toggle-guest-local-administrators.ps1)  

<img width="627" alt="image" src="https://github.com/user-attachments/assets/870a3eac-3398-44fe-91c0-96f3c2578df4">

[Scan 4 - Guest Account Group Removal](https://drive.google.com/file/d/1jVgikjfrV1YjOcL3QRT_oUB0Y82w22V7/view?usp=drive_link)


#### Remediation Round 4: Windows OS Updates

Windows updates were re-enabled and applied until the system was fully up to date. A final scan verified the changes  

<img width="627" alt="image" src="https://github.com/user-attachments/assets/870a3eac-3398-44fe-91c0-96f3c2578df4">

[Scan 5 - Post Windows Updates](https://drive.google.com/file/d/1tmDjeHl5uiGitRwWy8kFRi33q-nGi1Zt/view?usp=drive_link)

---

### First Cycle Remediation Effort Summary

The remediation process reduced total vulnerabilities by 80%, from 30 to 6. Critical vulnerabilities were resolved by the second scan (100%), and high vulnerabilities dropped by 90%. Mediums were reduced by 76%. In an actual production environment, asset criticality would further guide future remediation efforts.  

<img width="1920" alt="image" src="https://github.com/user-attachments/assets/51f0aae8-7f36-4d90-b29f-5257e57155f9">

[Remediation Data](https://docs.google.com/spreadsheets/d/1FTtFfZYmFsNLU6pm8nTzsKyKE-d2ftXzX_DPwcnFNfA/edit?gid=0#gid=0)

---

### On-going Vulnerability Management (Maintenance Mode)

After completing the initial remediation cycle, the vulnerability management program transitions into **Maintenance Mode**. This phase ensures that vulnerabilities continue to be managed proactively, keeping systems secure over time. Regular scans, continuous monitoring, and timely remediation are crucial components of this phase. (See [Finalized Policy](https://docs.google.com/document/d/1rvueLX_71pOR8ldN9zVW9r_zLzDQxVsnSUtNar8ftdg/edit?usp=drive_link) for scanning and remediation cadence requirements.)

Key activities in Maintenance Mode include:
- **Scheduled Vulnerability Scans**: Perform regular scans (e.g., weekly or monthly) to detect new vulnerabilities as systems evolve.
- **Patch Management**: Continuously apply security patches and updates, ensuring no critical vulnerabilities remain unpatched.
- **Remediation Follow-ups**: Address newly identified vulnerabilities promptly, prioritizing based on risk and impact.
- **Policy Review and Updates**: Periodically review the Vulnerability Management Policy to ensure it aligns with the latest security best practices and organizational needs.
- **Audit and Compliance**: Conduct internal audits to ensure compliance with the vulnerability management policy and external regulations.
- **Ongoing Communication with Stakeholders**: Maintain open communication with teams responsible for remediation, ensuring efficient coordination.

By maintaining an active vulnerability management process, organizations can stay ahead of emerging threats and ensure long-term security resilience.
