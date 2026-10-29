# Privacy Policy

[← www.orcaslicer.com](https://www.orcaslicer.com/)

## Privacy Policy

OrcaSlicer desktop application · Effective: June 12, 2026 · Version 1.0

The English version of this Privacy Policy is the legally authoritative text; translations are provided for convenience.

OrcaSlicer is a free, open-source slicer for FDM 3D printers, licensed under AGPL-3.0. It is designed to run entirely on your computer. This policy explains what the application does — and deliberately does not do — with your data.

This policy covers the **OrcaSlicer desktop application** only. The optional Orca Cloud service is covered by the [Orca Cloud Terms of Service & Privacy Policy](https://cloud.orcaslicer.com/terms-and-privacy), which likewise does not apply to purely local use of the desktop application.

**In short:** OrcaSlicer works offline. Your 3D models, project files, G-code, and printer settings stay on your device. The app collects no telemetry and requires no account. It only connects to the internet for things you can see and control: update checks, profile updates, and printer/cloud integrations you choose to enable.

### 1. Who we are

OrcaSlicer is maintained by the OrcaSlicer open-source community. The legal entity responsible for this policy and for handling privacy requests is:

**OrcaSlicer Pte. Ltd.** (UEN 202546300C)\
160 Robinson Road, #14-04, Singapore Business Federation Center, Singapore 068914\
Email: [privacy@orcaslicer.com](mailto:privacy@orcaslicer.com)

For the purposes of the EU/UK General Data Protection Regulation (GDPR) and the Singapore Personal Data Protection Act (PDPA), OrcaSlicer Pte. Ltd. is the data controller for the limited processing described below.

### 2. What stays on your device

Everything you create or configure in OrcaSlicer is stored locally on your computer. We never see your models, your prints, or your settings — unless you choose to upload profiles via the optional Orca Cloud service. The application does not include analytics, advertising SDKs, or usage tracking, and it does not phone home in the background.

### 3. Network connections the app makes

OrcaSlicer connects to the internet only in the following cases:

| Connection                                                                                                                                                    | When                                                 | Data involved                                                                                                                                                                                                            | Your control                                             |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------- |
| Software update check                                                                                                                                         | On startup (periodic)                                | Limited technical request data: IP address, timestamp, application version, and operating-system information. No local projects, profiles, print jobs, or printer data are uploaded.                                     | Disable in Preferences                                   |
| Printer profile / preset updates                                                                                                                              | On startup (periodic)                                | Same request data as above                                                                                                                                                                                               | Disable in Preferences                                   |
| Orca Cloud profile sync (optional)                                                                                                                            | Only if you create an Orca Cloud account and sign in | Account details and the profiles, presets, and configuration files you choose to upload, sync, or share — governed by the [Orca Cloud Terms of Service & Privacy Policy](https://cloud.orcaslicer.com/terms-and-privacy) | Optional; the app is fully functional without an account |
| Your own printer (LAN)                                                                                                                                        | When you add a printer                               | G-code, print commands, camera stream — sent directly to your device on your network, not to us                                                                                                                          | Only if you connect a printer                            |
| Print host integrations — self-hosted (OctoPrint, Klipper/Moonraker, PrusaLink, Duet, etc.) or third-party cloud services (SimplyPrint, Obico, Prusa Connect) | When you configure them                              | Host address and API key you enter (stored locally), files you send. Cloud print services are governed by their own privacy policies.                                                                                    | Only if you configure them                               |
| Bambu Network Plugin (third-party)                                                                                                                            | Only if you install it and sign in                   | Your Bambu Lab account login and cloud printing traffic, handled by Bambu Lab's proprietary plugin under _their_ privacy policy                                                                                          | Optional download; never installed silently              |
| Linked websites / model libraries                                                                                                                             | When you click a link                                | Governed by that website's own policy                                                                                                                                                                                    | Only when you choose to visit                            |

Like any internet request, these connections expose your IP address to the receiving server (e.g., GitHub for releases and profiles, or our update servers). We do not use this to identify or profile you. Where requests reach servers we operate, technical logs are kept for security and reliability purposes only and are purged within 90 days, consistent with the Orca Cloud Privacy Policy.

To the extent this transient technical data (such as your IP address) constitutes personal data, we process it on the basis of our legitimate interest in operating, securing, and maintaining the software's update and profile infrastructure (Art. 6(1)(f) GDPR). Our infrastructure is provided by Cloudflare, Inc. (United States); where the GDPR requires transfer safeguards, we rely on appropriate safeguards such as standard contractual clauses, as further described in the [Orca Cloud Privacy Policy](https://cloud.orcaslicer.com/terms-and-privacy).

### 4. What we do not do

* No telemetry, usage statistics, or behavioral analytics in the desktop app. The application even explicitly disables the telemetry capability of the third-party Bambu network plugin before it starts — verifiable in the source code.
* No account or registration required to use OrcaSlicer.
* No selling, renting, or sharing of personal data — we have none to sell.
* No advertising or third-party tracking SDKs.
* No automatic upload of crash dumps. If the app crashes, you may _choose_ to share logs with us via a GitHub issue; anything you post there is public and governed by GitHub's privacy policy.

### 5. Third-party services

Some optional features rely on third parties, each with their own privacy policy:

* **Orca Cloud** — our optional profile backup, sync, and sharing service, operated by OrcaSlicer Pte. Ltd. under the [Orca Cloud Terms of Service & Privacy Policy](https://cloud.orcaslicer.com/terms-and-privacy).
* **GitHub** — hosts our releases, profiles, and issue tracker.
* **Bambu Lab** — provides the proprietary Bambu Network Plugin and cloud services for Bambu printers.
* **Your print host software** (OctoPrint, Moonraker, PrusaLink, Duet and similar) — runs on your own hardware under your control.
* **Cloud print services** (SimplyPrint, Obico, Prusa Connect and similar) — optional integrations you configure with your own account; data you send goes to those services under their own policies.

We encourage you to review their policies before enabling these features. Disabling or not configuring them does not limit core slicing functionality.

### 6. Your rights

Apart from the short-lived technical request data described in Section 3, the desktop application collects no personal data — so in most cases there is nothing for us to access, correct, or delete; your data is already in your hands, on your device.

If you believe we hold personal data about you (for example, from a support email you sent us), you have the right to request access, correction, or deletion of that data:

* **Singapore (PDPA):** you may make access and correction requests, and withdraw consent, under the Personal Data Protection Act 2012. Our Data Protection Officer can be reached at [privacy@orcaslicer.com](mailto:privacy@orcaslicer.com). You may also complain to the Personal Data Protection Commission (PDPC).
* **EU/EEA & UK (GDPR):** you have rights of access, rectification, erasure, restriction, portability, and objection (Articles 15–21 GDPR), and the right to lodge a complaint with your local supervisory authority.

We respond to verified requests within 30 days.

### 7. Children

OrcaSlicer is general-purpose software and does not knowingly collect personal data from anyone, including children. Since no data is collected by the app, no parental-consent mechanism is required for its use.

### 8. Security

Update and profile downloads are delivered over HTTPS from official sources and should only be obtained from [our official GitHub repository](https://github.com/OrcaSlicer/OrcaSlicer) or orcaslicer.com. Credentials you enter for print hosts are stored locally on your device. To report a security vulnerability, contact [security@orcaslicer.com](mailto:security@orcaslicer.com).

### 9. Changes to this policy

If we change this policy, we will post the updated version on this page with a new effective date and summarize material changes in the release notes. Because the application's behavior is open source, you can always [verify what it does in the code itself](https://github.com/OrcaSlicer/OrcaSlicer).

### 10. Contact

Privacy questions and data requests: [privacy@orcaslicer.com](mailto:privacy@orcaslicer.com)\
Security reports: [security@orcaslicer.com](mailto:security@orcaslicer.com)\
Postal: OrcaSlicer Pte. Ltd., 160 Robinson Road, #14-04, Singapore Business Federation Center, Singapore 068914
