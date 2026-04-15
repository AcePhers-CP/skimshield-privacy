# Privacy Policy for SkimShield

**Last Updated:** 2026-04-15
**Extension Name:** SkimShield
**Developer:** AcePhers
**Contact:** songheon0421@gmail.com
**This Policy (Public URL):** https://acephers-cp.github.io/skimshield-privacy/PRIVACY_POLICY

---

## Overview

SkimShield is a browser security extension that detects formjacking (web skimming) attacks in real time. It protects your payment information and personal data by monitoring network requests made from web pages you visit.

**All analysis is performed entirely on your device. SkimShield does not collect, transmit, or share any personal data with any external server or third party.**

---

## 1. What Data SkimShield Accesses

To detect formjacking attacks, SkimShield accesses the following data **on your device only**:

### 1.1 Network Request Data (In-Memory Only)
When you interact with a payment form on a webpage, SkimShield temporarily inspects:
- The destination URL (domain) of outgoing network requests
- The HTTP method and request type (fetch, XHR, WebSocket, Image, etc.)
- The request payload (body content, up to 50 KB) to detect encoded card data

This data is used **only for real-time analysis** within the extension's runtime memory. It is **never stored to disk** and **never transmitted externally**.

### 1.2 Detection Event Logs (Stored Locally)
When a suspicious or dangerous request is detected, SkimShield saves a detection event to your device's local browser storage (IndexedDB). Each log entry contains:

| Field | Description |
|-------|-------------|
| `verdict` | Analysis result: DANGEROUS / POSSIBLE_ATTACK_STRONG / POSSIBLE_ATTACK_MEDIUM / SAFE |
| `targetDomain` | The domain the suspicious request was sent to |
| `currentDomain` | The domain of the page you were visiting |
| `requestType` | Request method (FETCH, XHR, BEACON, FORM, IMAGE, WS, LOCAL_STORAGE) |
| `reason` | Human-readable description of why the request was flagged |
| `timestamp` | Time the event was detected |

**No URLs, page content, form field values, or personal information are stored.**

### 1.3 Extension Settings (Stored Locally)
User preferences are stored in `chrome.storage.local` on your device:
- Alert sensitivity level (`alertLevel`: 1–3)
- Data retention period (`dataRetentionHours`: 1–168 hours)
- User-defined whitelist of trusted domains
- UI language preference

---

## 2. How SkimShield Uses Data

| Data | Purpose | Stored? | Sent Externally? |
|------|---------|---------|-----------------|
| Network request payload | Detect card data exfiltration patterns | No (in-memory only) | No |
| Destination domain | Identify suspicious domains | Only in detection logs | No |
| Source page domain | Correlate attack to page visited | Only in detection logs | No |
| Extension settings | Apply user preferences | Yes (local only) | No |
| Detection logs | Display attack history in popup | Yes (local only) | No |

SkimShield does **not** use your data for advertising, analytics, profiling, or any purpose beyond real-time security analysis on your device.

---

## 3. Data Retention and Deletion

Detection event logs are automatically deleted from your device based on your configured retention period (default: **24 hours**). The cleanup runs once per hour via Chrome's Alarms API.

You can also:
- Change the retention period in the extension settings (1 hour to 7 days)
- Clear all stored data by uninstalling the extension

When the extension is uninstalled, all `chrome.storage.local` and IndexedDB data is automatically removed by Chrome.

---

## 4. Permissions Justification

SkimShield requests the following permissions. Each is strictly necessary for its security function.

| Permission | Why It Is Required |
|------------|-------------------|
| `<all_urls>` (host permission) | Formjacking attacks can occur on any website. SkimShield must monitor network requests on all pages to detect attacks wherever they occur. |
| `activeTab` | Used to update the extension icon to reflect the security status of the currently active tab. |
| `storage` | Stores extension settings and detection logs locally on your device. No data leaves your device. |
| `alarms` | Triggers periodic cleanup of detection logs older than the configured retention period. |
| `declarativeNetRequest` | Blocks confirmed malicious domains at the network layer without needing to read page content. |
| `tabs` | Updates the security status icon when you switch tabs, and clears per-tab state when a tab is closed. |
| `world: "MAIN"` (content script) | To intercept native browser APIs (fetch, XMLHttpRequest, WebSocket, Image.src) before they execute, SkimShield must run in the same JavaScript environment as the webpage. This is the only way to detect data exfiltration at the source. |

---

## 5. Data Sharing

SkimShield **does not share any data** with any third party, analytics service, advertising network, or external server. There is no cloud component, no telemetry, and no remote configuration.

The extension operates entirely offline. No network connection is required for SkimShield to function.

---

## 6. Children's Privacy

SkimShield does not knowingly collect any information from children under 13. The extension does not collect personal information from any user.

---

## 7. Changes to This Policy

If this privacy policy is updated, the "Last Updated" date at the top of this document will reflect the change. Significant changes will be noted in the extension's update changelog.

---

## 8. Contact

If you have questions or concerns about this privacy policy, please contact:

**Email:** songheon0421@gmail.com
**GitHub:** https://github.com/BlueDongas/Skimshield_extension

---

## 한국어 요약 (Korean Summary)

SkimShield는 폼재킹(결제 정보 탈취) 공격을 실시간으로 탐지하는 보안 확장 프로그램입니다.

**수집하지 않는 것**: 개인정보, 결제 카드 번호, 비밀번호, 검색 기록, 위치 정보

**로컬에 저장하는 것**: 탐지 이벤트 로그(의심 요청의 도메인과 판정 결과), 사용자 설정

**외부 전송**: 없음. 모든 분석은 사용자 기기에서만 이루어집니다.

**보존 기간**: 탐지 로그는 설정한 기간(기본 24시간) 이후 자동 삭제됩니다.

문의: songheon0421@gmail.com
