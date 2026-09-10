# 📱 Merchant Wallet Application — Android Developer Task Assignment Document

**Project:** Merchant Wallet Application
**Platform:** Android (Native)
**Prepared by:** Project Lead
**Date:** 2026-09-10

---

## 📌 Overview

The Merchant Wallet Application is an Android-based digital wallet solution designed for merchants. It supports device binding, KYC verification, UPI payments, wallet operations, and complete profile & transaction management. Each feature below is a standalone task with clear scope, deliverables, and acceptance criteria.

---

## ✅ TASK 1 — Device Binding

**Task ID:** `MWA-01`
**Priority:** 🔴 Critical
**Estimated Effort:** 3–4 days

### Description
Implement device binding to securely associate the merchant's account with a specific physical device. This ensures that wallet operations can only be performed from a registered device.

### Scope
- Generate and store a unique device fingerprint (Device ID)
- API integration for device registration/binding
- Handle re-binding on device change or app reinstall
- Secure storage of binding tokens (Android Keystore)
- Show appropriate UI states: binding in progress, bound, binding failed

### Acceptance Criteria
- [ ] Device is successfully registered on first login
- [ ] Binding token is stored securely and persists across sessions
- [ ] Re-binding flow is triggered on device change
- [ ] Error states are handled with user-friendly messages

---

## ✅ TASK 2 — KYC (Know Your Customer)

**Task ID:** `MWA-02`
**Priority:** 🔴 Critical
**Estimated Effort:** 5–6 days

### Description
Implement the KYC verification flow allowing merchants to submit identity documents for verification. This is a prerequisite to enable full wallet functionality.

### Scope
- Multi-step KYC form (personal details, business details, document upload)
- Document capture via camera (Aadhar, PAN, GST, etc.)
- Image upload APIs with progress indication
- KYC submission and confirmation screen
- Real-time KYC status polling / webhook integration
- KYC Status display (Pending / Approved / Rejected / Re-submission required)

### Acceptance Criteria
- [ ] Merchant can complete KYC in a guided multi-step flow
- [ ] Documents are captured, compressed, and uploaded successfully
- [ ] KYC status is reflected in real time across the app
- [ ] Re-submission is supported when KYC is rejected with reason displayed

---

## ✅ TASK 3 — KYC Status Screen

**Task ID:** `MWA-03`
**Priority:** 🟡 High
**Estimated Effort:** 1–2 days

### Description
A dedicated screen to display the current KYC verification status of the merchant.

### Scope
- Show current KYC status with visual indicators (icon + color coding)
- Display submission date and last updated timestamp
- Show rejection reason (if applicable) with re-submit CTA
- Navigate to KYC flow from this screen if not yet submitted

### Acceptance Criteria
- [ ] All KYC states (Not Started, Pending, Approved, Rejected) are visually distinct
- [ ] Rejection reason is clearly displayed
- [ ] Re-submission CTA navigates to the KYC form with prefilled data

---

## ✅ TASK 4 — UPI Scan and Pay

**Task ID:** `MWA-04`
**Priority:** 🔴 Critical
**Estimated Effort:** 5–7 days

### Description
Enable merchants to initiate payments by scanning UPI QR codes using the device camera.

### Scope
- QR code scanner using CameraX / ML Kit / ZXing
- Parse and validate UPI deep links from scanned QR (`upi://pay?...`)
- Pre-fill payment screen with payee VPA, name, and amount (if encoded)
- Allow merchant to enter/edit amount before confirming
- Initiate UPI payment via wallet backend API
- Show payment success/failure screen with transaction reference

### Acceptance Criteria
- [ ] QR scanner opens and correctly reads UPI QR codes
- [ ] Invalid or non-UPI QR codes show an appropriate error
- [ ] Payment confirmation screen shows correct payee details
- [ ] Success/failure feedback is shown with transaction ID

---

## ✅ TASK 5 — Wallet to Wallet Transfer

**Task ID:** `MWA-05`
**Priority:** 🔴 Critical
**Estimated Effort:** 4–5 days

### Description
Allow merchants to transfer funds directly from their wallet to another wallet (peer-to-peer).

### Scope
- Beneficiary search / entry (mobile number, wallet ID, or VPA)
- Amount entry with wallet balance validation
- Transfer confirmation screen with summary
- PIN / biometric authentication before transfer
- API integration for wallet-to-wallet transfer
- Success/failure result screen with transaction reference

### Acceptance Criteria
- [ ] Beneficiary can be searched and selected
- [ ] Insufficient balance prevents transfer with clear messaging
- [ ] Auth (PIN/biometric) is enforced before executing transfer
- [ ] Transaction reference is displayed and logged in transaction history

---

## ✅ TASK 6 — Load Wallet

**Task ID:** `MWA-06`
**Priority:** 🟡 High
**Estimated Effort:** 3–4 days

### Description
Allow merchants to add funds (load money) into their wallet from linked bank accounts or payment methods.

### Scope
- Load amount entry screen with preset quick-amount chips
- Payment method selector (Bank account / UPI / Net Banking)
- Integration with payment gateway for fund loading
- Loading status screen (pending → success/failure)
- Update wallet balance on success

### Acceptance Criteria
- [ ] Merchant can load wallet from at least one payment method
- [ ] Load status transitions are clearly shown
- [ ] Wallet balance updates immediately after successful load
- [ ] Failed loads show reason and retry option

---

## ✅ TASK 7 — Unload Wallet (Withdrawal)

**Task ID:** `MWA-07`
**Priority:** 🟡 High
**Estimated Effort:** 3–4 days

### Description
Allow merchants to withdraw/unload wallet balance to a linked bank account.

### Scope
- Unload amount entry with min/max validation
- Bank account selection (from pre-registered accounts)
- Confirmation screen with summary
- PIN / biometric authentication
- API integration for withdrawal
- Status tracking (initiated, processing, completed)

### Acceptance Criteria
- [ ] Merchant cannot unload more than available balance
- [ ] Auth is enforced before initiating withdrawal
- [ ] Withdrawal status is tracked and displayed
- [ ] Success confirmation includes estimated credit time

---

## ✅ TASK 8 — Wallet Transfer (Internal Transfer)

**Task ID:** `MWA-08`
**Priority:** 🟡 High
**Estimated Effort:** 3 days

### Description
Support internal fund transfers between sub-wallets or designated wallet accounts within the platform.

### Scope
- Source and destination wallet selection
- Amount entry with balance validation
- Transfer confirmation with breakdown
- PIN / biometric authentication
- API integration and success/failure handling

### Acceptance Criteria
- [ ] Transfer between valid wallet accounts is successful
- [ ] Balance is updated in both source and destination
- [ ] Auth is enforced and logged

---

## ✅ TASK 9 — Deregister Wallet

**Task ID:** `MWA-09`
**Priority:** 🟠 Medium
**Estimated Effort:** 2–3 days

### Description
Allow a merchant to deregister / close their wallet account. This should be a safeguarded flow with explicit confirmations.

### Scope
- Deregister option under Settings / Profile
- Multi-step confirmation (reason selection → warning screen → final confirm)
- Balance check — block deregistration if balance > 0 (prompt to unload first)
- API call for deregistration
- Clear session and redirect to onboarding/login on success

### Acceptance Criteria
- [ ] Merchant with non-zero balance is blocked from deregistering
- [ ] Multi-step confirmation prevents accidental deregistration
- [ ] On success, all local data is cleared and session is terminated

---

## ✅ TASK 10 — Transaction List / History

**Task ID:** `MWA-10`
**Priority:** 🟡 High
**Estimated Effort:** 3–4 days

### Description
Display a comprehensive, paginated list of all wallet transactions for the merchant.

### Scope
- Paginated/infinite scroll transaction list
- Transaction types: Credit, Debit, Load, Unload, Transfer, Payment, Refund
- Filter by: date range, transaction type, status
- Search by transaction ID or amount
- Transaction detail screen (tap to expand)
- Download / export as PDF or CSV (optional v2)

### Acceptance Criteria
- [ ] All transaction types are listed and visually differentiated
- [ ] Filters and search work correctly
- [ ] Transaction detail screen shows complete information
- [ ] Pagination loads without UI jank

---

## ✅ TASK 11 — Balance Display

**Task ID:** `MWA-11`
**Priority:** 🟡 High
**Estimated Effort:** 1–2 days

### Description
Display the merchant's current wallet balance prominently across the app (dashboard, wallet screen).

### Scope
- Wallet balance widget on the home/dashboard screen
- Show/hide balance toggle (eye icon)
- Real-time balance refresh (pull-to-refresh + auto-refresh on transaction)
- Multi-wallet balance display (if applicable)
- Handle balance fetch errors gracefully

### Acceptance Criteria
- [ ] Balance is displayed correctly on all relevant screens
- [ ] Show/hide toggle persists user preference
- [ ] Balance refreshes correctly after any transaction

---

## ✅ TASK 12 — Profile Management

**Task ID:** `MWA-12`
**Priority:** 🟠 Medium
**Estimated Effort:** 3–4 days

### Description
Allow merchants to view and manage their profile information within the app.

### Scope
- View profile: name, mobile, email, business name, address
- Edit profile fields (with validation)
- Profile photo upload / capture
- Change MPIN / password flow
- Linked bank accounts section
- Logout option

### Acceptance Criteria
- [ ] All profile fields are editable with appropriate validations
- [ ] Profile photo updates are reflected immediately
- [ ] MPIN change requires current MPIN verification
- [ ] Logout clears all local session data

---

## 📦 Shared / Cross-Cutting Tasks

| Task ID   | Task                                                       | Priority       | Effort  |
|-----------|------------------------------------------------------------|----------------|---------|
| `MWA-13`  | App Navigation & Deep Linking Setup                        | 🔴 Critical    | 2 days  |
| `MWA-14`  | Authentication (Login / MPIN / Biometric)                  | 🔴 Critical    | 3 days  |
| `MWA-15`  | Network Layer & API Client Setup (Retrofit/OkHttp)         | 🔴 Critical    | 2 days  |
| `MWA-16`  | Local DB & Secure Storage (Room + Keystore)                | 🟡 High        | 2 days  |
| `MWA-17`  | Error Handling & Global Exception Management               | 🟡 High        | 1 day   |
| `MWA-18`  | UI Component Library / Design System Setup                 | 🟡 High        | 2 days  |
| `MWA-19`  | Push Notifications (FCM) for transaction alerts            | 🟠 Medium      | 2 days  |
| `MWA-20`  | Analytics & Crash Reporting (Firebase)                     | 🟠 Medium      | 1 day   |

---

## 📋 Reporting & Progress Tracking

Developers must update task status using the following stages:

| Status | Meaning |
|--------|---------|
| 🔲 Not Started | Task not yet begun |
| 🔄 In Progress | Development underway |
| 👁️ In Review   | PR raised, under code review |
| 🧪 In Testing  | Handed to QA |
| ✅ Done        | QA signed off, merged to main |
| 🚫 Blocked     | Blocked by dependency or issue |

### Daily Standup Update Format (per task)

```
Task ID   : MWA-XX
Feature   : <Feature Name>
Status    : <Current Status>
Done Today: <What was completed>
Next      : <What is planned next>
Blocker   : <Any blockers, or None>
```

---

## 🗓️ Suggested Development Sequence

```
Week 1:  MWA-13 → MWA-14 → MWA-15 → MWA-16   (Foundation & Setup)
Week 2:  MWA-01 (Device Binding) → MWA-02 (KYC) → MWA-03 (KYC Status)
Week 3:  MWA-11 (Balance Display) → MWA-06 (Load) → MWA-07 (Unload)
Week 4:  MWA-04 (UPI Scan & Pay) → MWA-05 (Wallet-to-Wallet)
Week 5:  MWA-08 (Internal Transfer) → MWA-10 (Transaction List) → MWA-09 (Deregister)
Week 6:  MWA-12 (Profile) → MWA-17 → MWA-18 → MWA-19 → MWA-20
```

---

## 📊 Task Summary

| Task ID  | Feature                    | Priority    | Effort     |
|----------|----------------------------|-------------|------------|
| MWA-01   | Device Binding             | 🔴 Critical | 3–4 days   |
| MWA-02   | KYC                        | 🔴 Critical | 5–6 days   |
| MWA-03   | KYC Status Screen          | 🟡 High     | 1–2 days   |
| MWA-04   | UPI Scan and Pay           | 🔴 Critical | 5–7 days   |
| MWA-05   | Wallet to Wallet Transfer  | 🔴 Critical | 4–5 days   |
| MWA-06   | Load Wallet                | 🟡 High     | 3–4 days   |
| MWA-07   | Unload Wallet              | 🟡 High     | 3–4 days   |
| MWA-08   | Internal Transfer          | 🟡 High     | 3 days     |
| MWA-09   | Deregister Wallet          | 🟠 Medium   | 2–3 days   |
| MWA-10   | Transaction List           | 🟡 High     | 3–4 days   |
| MWA-11   | Balance Display            | 🟡 High     | 1–2 days   |
| MWA-12   | Profile Management         | 🟠 Medium   | 3–4 days   |
| MWA-13   | Navigation & Deep Linking  | 🔴 Critical | 2 days     |
| MWA-14   | Authentication             | 🔴 Critical | 3 days     |
| MWA-15   | Network Layer Setup        | 🔴 Critical | 2 days     |
| MWA-16   | Local DB & Secure Storage  | 🟡 High     | 2 days     |
| MWA-17   | Error Handling             | 🟡 High     | 1 day      |
| MWA-18   | UI Component Library       | 🟡 High     | 2 days     |
| MWA-19   | Push Notifications (FCM)   | 🟠 Medium   | 2 days     |
| MWA-20   | Analytics & Crash Reporting| 🟠 Medium   | 1 day      |

---

*Document maintained by Project Lead. Update task statuses regularly during standups.*

---

## 🖼️ ASCII Wireframes for All 20 Screens

---

### MWA-01 — Device Binding Screen

```
┌─────────────────────────────────┐
│  ←  Device Binding              │
├─────────────────────────────────┤
│                                 │
│       🔒                        │
│   Secure Your Device            │
│                                 │
│  ┌───────────────────────────┐  │
│  │  Device ID:               │  │
│  │  XXXX-XXXX-XXXX-XXXX      │  │
│  └───────────────────────────┘  │
│                                 │
│  Status: ● Binding in Progress  │
│  ████████░░░░░░░░░░  45%        │
│                                 │
│  ┌───────────────────────────┐  │
│  │      BIND DEVICE          │  │
│  └───────────────────────────┘  │
│                                 │
│  ⚠ Already bound to a device?  │
│  [Re-bind this device]          │
│                                 │
└─────────────────────────────────┘
```

---

### MWA-02 — KYC Submission Flow (Step 1: Personal Details)

```
┌─────────────────────────────────┐
│  ←  KYC Verification     1/3   │
│  ●────────○────────○            │
├─────────────────────────────────┤
│                                 │
│  Personal Details               │
│  ─────────────────              │
│  Full Name *                    │
│  ┌───────────────────────────┐  │
│  │ Enter full name           │  │
│  └───────────────────────────┘  │
│                                 │
│  Date of Birth *                │
│  ┌───────────────────────────┐  │
│  │ DD / MM / YYYY        📅  │  │
│  └───────────────────────────┘  │
│                                 │
│  Aadhar Number *                │
│  ┌───────────────────────────┐  │
│  │ XXXX XXXX XXXX            │  │
│  └───────────────────────────┘  │
│                                 │
│  PAN Number *                   │
│  ┌───────────────────────────┐  │
│  │ ABCDE1234F                │  │
│  └───────────────────────────┘  │
│                                 │
│  ┌───────────────────────────┐  │
│  │        NEXT →             │  │
│  └───────────────────────────┘  │
└─────────────────────────────────┘
```

---

### MWA-03 — KYC Status Screen

```
┌─────────────────────────────────┐
│  ←  KYC Status                  │
├─────────────────────────────────┤
│                                 │
│         🟡 PENDING              │
│    Verification in Progress     │
│                                 │
│  ┌───────────────────────────┐  │
│  │  Submitted: 10 Sep 2026   │  │
│  │  Last Updated: 10 Sep 2026│  │
│  └───────────────────────────┘  │
│                                 │
│  Checklist:                     │
│  ✅ Personal Details            │
│  ✅ Business Details            │
│  ⏳ Document Verification       │
│                                 │
│  ┌───────────────────────────┐  │
│  │    REFRESH STATUS         │  │
│  └───────────────────────────┘  │
│                                 │
│  (If Rejected)                  │
│  ⚠ Reason: Document unclear    │
│  ┌───────────────────────────┐  │
│  │      RE-SUBMIT KYC        │  │
│  └───────────────────────────┘  │
└─────────────────────────────────┘
```

---

### MWA-04 — UPI Scan and Pay Screen

```
┌─────────────────────────────────┐
│  ←  Scan & Pay                  │
├─────────────────────────────────┤
│                                 │
│  ┌───────────────────────────┐  │
│  │                           │  │
│  │   [ Camera Viewfinder ]   │  │
│  │                           │  │
│  │   ┌─────────────────┐     │  │
│  │   │                 │     │  │
│  │   │   QR Frame      │     │  │
│  │   │                 │     │  │
│  │   └─────────────────┘     │  │
│  │                           │  │
│  └───────────────────────────┘  │
│                                 │
│  Align QR code within the frame │
│                                 │
│  ──────────── OR ────────────── │
│                                 │
│  ┌───────────────────────────┐  │
│  │   ENTER UPI ID MANUALLY   │  │
│  └───────────────────────────┘  │
│                                 │
│  ┌── Payee: ─────────────────┐  │
│  │ merchant@upi   ₹500.00    │  │
│  │     [CONFIRM & PAY]       │  │
│  └───────────────────────────┘  │
└─────────────────────────────────┘
```

---

### MWA-05 — Wallet to Wallet Transfer Screen

```
┌─────────────────────────────────┐
│  ←  Wallet Transfer             │
├─────────────────────────────────┤
│                                 │
│  Available Balance: ₹12,400.00  │
│                                 │
│  Beneficiary                    │
│  ┌───────────────────────────┐  │
│  │ 🔍 Search mobile / VPA    │  │
│  └───────────────────────────┘  │
│  ┌──────────┐ ┌──────────┐      │
│  │ Recent 1 │ │ Recent 2 │      │
│  └──────────┘ └──────────┘      │
│                                 │
│  Amount (₹)                     │
│  ┌───────────────────────────┐  │
│  │        0.00               │  │
│  └───────────────────────────┘  │
│  [₹100] [₹500] [₹1000] [₹5000] │
│                                 │
│  Remarks (optional)             │
│  ┌───────────────────────────┐  │
│  │                           │  │
│  └───────────────────────────┘  │
│                                 │
│  ┌───────────────────────────┐  │
│  │      PROCEED TO PAY       │  │
│  └───────────────────────────┘  │
└─────────────────────────────────┘
```

---

### MWA-06 — Load Wallet Screen

```
┌─────────────────────────────────┐
│  ←  Load Wallet                 │
├─────────────────────────────────┤
│                                 │
│  Current Balance: ₹12,400.00    │
│                                 │
│  Enter Amount (₹)               │
│  ┌───────────────────────────┐  │
│  │        0.00               │  │
│  └───────────────────────────┘  │
│  [₹500][₹1000][₹2000][₹5000]   │
│                                 │
│  Select Payment Method          │
│  ┌───────────────────────────┐  │
│  │ ○ 🏦 Net Banking           │  │
│  │ ● 💳 UPI                   │  │
│  │ ○ 🏧 Debit Card            │  │
│  └───────────────────────────┘  │
│                                 │
│  ┌───────────────────────────┐  │
│  │         LOAD NOW          │  │
│  └───────────────────────────┘  │
│                                 │
│  Loading Status:                │
│  ⏳ Processing...               │
│                                 │
└─────────────────────────────────┘
```

---

### MWA-07 — Unload Wallet (Withdrawal) Screen

```
┌─────────────────────────────────┐
│  ←  Withdraw Funds              │
├─────────────────────────────────┤
│                                 │
│  Available Balance: ₹12,400.00  │
│                                 │
│  Withdraw Amount (₹)            │
│  ┌───────────────────────────┐  │
│  │        0.00               │  │
│  └───────────────────────────┘  │
│  Min: ₹100   Max: ₹50,000       │
│                                 │
│  Destination Bank Account       │
│  ┌───────────────────────────┐  │
│  │ HDFC Bank ••••6789    ▼   │  │
│  └───────────────────────────┘  │
│                                 │
│  ┌───────────────────────────┐  │
│  │  Estimated credit: 1-2    │  │
│  │  business days            │  │
│  └───────────────────────────┘  │
│                                 │
│  ┌───────────────────────────┐  │
│  │     INITIATE WITHDRAWAL   │  │
│  └───────────────────────────┘  │
└─────────────────────────────────┘
```

---

### MWA-08 — Wallet Internal Transfer Screen

```
┌─────────────────────────────────┐
│  ←  Internal Transfer           │
├─────────────────────────────────┤
│                                 │
│  From Wallet                    │
│  ┌───────────────────────────┐  │
│  │ Main Wallet   ₹12,400  ▼  │  │
│  └───────────────────────────┘  │
│                                 │
│          ⇅  (swap)              │
│                                 │
│  To Wallet                      │
│  ┌───────────────────────────┐  │
│  │ Savings Wallet  ₹3,200 ▼  │  │
│  └───────────────────────────┘  │
│                                 │
│  Amount (₹)                     │
│  ┌───────────────────────────┐  │
│  │        0.00               │  │
│  └───────────────────────────┘  │
│                                 │
│  ┌───────────────────────────┐  │
│  │    TRANSFER FUNDS         │  │
│  └───────────────────────────┘  │
└─────────────────────────────────┘
```

---

### MWA-09 — Deregister Wallet Screen

```
┌─────────────────────────────────┐
│  ←  Close Wallet Account        │
├─────────────────────────────────┤
│                                 │
│         ⚠️  WARNING             │
│                                 │
│  This action will permanently   │
│  close your wallet account.     │
│                                 │
│  Reason for closing *           │
│  ┌───────────────────────────┐  │
│  │ Select reason          ▼  │  │
│  └───────────────────────────┘  │
│                                 │
│  ┌───────────────────────────┐  │
│  │ ⚠ Current balance: ₹0.00 │  │
│  │ Balance must be ₹0 to     │  │
│  │ proceed.                  │  │
│  └───────────────────────────┘  │
│                                 │
│  ☐ I understand this action     │
│    cannot be undone             │
│                                 │
│  ┌───────────────────────────┐  │
│  │   CLOSE MY ACCOUNT        │  │
│  └───────────────────────────┘  │
└─────────────────────────────────┘
```

---

### MWA-10 — Transaction List / History Screen

```
┌─────────────────────────────────┐
│  ←  Transactions     🔍  ⬇️    │
├─────────────────────────────────┤
│  [All][Credit][Debit][Transfer] │
│  Date Range: [Today ▼]          │
├─────────────────────────────────┤
│                                 │
│  Today                          │
│  ┌───────────────────────────┐  │
│  │ ↑ UPI Payment    -₹500   │  │
│  │   merchant@upi  2:30 PM  │  │
│  └───────────────────────────┘  │
│  ┌───────────────────────────┐  │
│  │ ↓ Load Wallet   +₹2000   │  │
│  │   Net Banking   10:15 AM │  │
│  └───────────────────────────┘  │
│                                 │
│  Yesterday                      │
│  ┌───────────────────────────┐  │
│  │ ↑ Transfer      -₹1500   │  │
│  │   user@wallet   5:00 PM  │  │
│  └───────────────────────────┘  │
│                                 │
│  ▼ Load more...                 │
└─────────────────────────────────┘
```

---

### MWA-11 — Balance Display / Dashboard Screen

```
┌─────────────────────────────────┐
│  Merchant Wallet         🔔 👤  │
├─────────────────────────────────┤
│                                 │
│  ┌───────────────────────────┐  │
│  │  💳 Main Wallet           │  │
│  │  ₹12,400.00           👁  │  │
│  │  Last updated: Just now   │  │
│  └───────────────────────────┘  │
│                                 │
│  ┌──────┐ ┌──────┐ ┌──────┐    │
│  │  ↓   │ │  ↑   │ │  ⇄   │    │
│  │ Load │ │Unload│ │ Pay  │    │
│  └──────┘ └──────┘ └──────┘    │
│                                 │
│  Recent Transactions            │
│  ┌───────────────────────────┐  │
│  │ ↑ UPI Pay       -₹500    │  │
│  └───────────────────────────┘  │
│  ┌───────────────────────────┐  │
│  │ ↓ Load          +₹2000   │  │
│  └───────────────────────────┘  │
│                                 │
│  [View All Transactions →]      │
└─────────────────────────────────┘
```

---

### MWA-12 — Profile Management Screen

```
┌─────────────────────────────────┐
│  ←  My Profile                  │
├─────────────────────────────────┤
│                                 │
│         [ 👤 Photo ] ✏️         │
│         John Merchant           │
│         +91 98765 43210         │
│                                 │
│  ─── Account Details ─────────  │
│  Email       john@biz.com  ✏️  │
│  Business    ABC Stores    ✏️  │
│  Address     123 Main St   ✏️  │
│                                 │
│  ─── Security ────────────────  │
│  ┌───────────────────────────┐  │
│  │  🔑  Change MPIN          │  │
│  └───────────────────────────┘  │
│  ┌───────────────────────────┐  │
│  │  🏦  Linked Bank Accounts │  │
│  └───────────────────────────┘  │
│                                 │
│  ┌───────────────────────────┐  │
│  │  🚪  LOGOUT               │  │
│  └───────────────────────────┘  │
└─────────────────────────────────┘
```

---

### MWA-13 — App Navigation / Home Dashboard

```
┌─────────────────────────────────┐
│  Merchant Wallet         🔔    │
├─────────────────────────────────┤
│                                 │
│  Good Morning, John! 👋         │
│                                 │
│  ┌───────────────────────────┐  │
│  │  Balance: ₹12,400.00  👁  │  │
│  └───────────────────────────┘  │
│                                 │
│  ┌──────┐ ┌──────┐ ┌──────┐    │
│  │ 📷   │ │  ↑   │ │  ⇄   │    │
│  │ Scan │ │ Send │ │ More │    │
│  └──────┘ └──────┘ └──────┘    │
│                                 │
│  Quick Links                    │
│  ┌──────────┐  ┌──────────┐    │
│  │  Load    │  │ Withdraw │    │
│  └──────────┘  └──────────┘    │
│  ┌──────────┐  ┌──────────┐    │
│  │ History  │  │ Profile  │    │
│  └──────────┘  └──────────┘    │
│                                 │
├─────────────────────────────────┤
│  🏠 Home  💳 Wallet  📋 Txns  👤│
└─────────────────────────────────┘
```

---

### MWA-14 — Authentication / Login / MPIN Screen

```
┌─────────────────────────────────┐
│                                 │
│         🔐                      │
│    Merchant Wallet Login        │
│                                 │
│  Mobile Number                  │
│  ┌───────────────────────────┐  │
│  │ +91  |  Enter mobile no.  │  │
│  └───────────────────────────┘  │
│                                 │
│  ──── OR Enter MPIN ──────────  │
│                                 │
│        ● ● ● ● ● ●              │
│                                 │
│  ┌───┐ ┌───┐ ┌───┐             │
│  │ 1 │ │ 2 │ │ 3 │             │
│  ├───┤ ├───┤ ├───┤             │
│  │ 4 │ │ 5 │ │ 6 │             │
│  ├───┤ ├───┤ ├───┤             │
│  │ 7 │ │ 8 │ │ 9 │             │
│  ├───┤ ├───┤ ├───┤             │
│  │   │ │ 0 │ │ ⌫ │             │
│  └───┘ └───┘ └───┘             │
│                                 │
│  [Use Biometric 👆]             │
│  [Forgot MPIN?]                 │
└─────────────────────────────────┘
```

---

### MWA-15 — Network / API Status Screen (Error/Retry State)

```
┌─────────────────────────────────┐
│  ←  Connection Error            │
├─────────────────────────────────┤
│                                 │
│                                 │
│         📡                      │
│                                 │
│   Unable to connect to server   │
│                                 │
│  ┌───────────────────────────┐  │
│  │  Error: Network timeout   │  │
│  │  Code: 504                │  │
│  └───────────────────────────┘  │
│                                 │
│  Please check your internet     │
│  connection and try again.      │
│                                 │
│  ┌───────────────────────────┐  │
│  │         RETRY             │  │
│  └───────────────────────────┘  │
│                                 │
│  ┌───────────────────────────┐  │
│  │      GO TO HOME           │  │
│  └───────────────────────────┘  │
│                                 │
└─────────────────────────────────┘
```

---

### MWA-16 — Secure Storage / PIN Setup Screen

```
┌─────────────────────────────────┐
│  ←  Set Up MPIN                 │
├─────────────────────────────────┤
│                                 │
│   Create a 6-digit MPIN for     │
│   secure access                 │
│                                 │
│  Enter New MPIN                 │
│        ○ ○ ○ ○ ○ ○              │
│                                 │
│  Confirm MPIN                   │
│        ○ ○ ○ ○ ○ ○              │
│                                 │
│  ┌───┐ ┌───┐ ┌───┐             │
│  │ 1 │ │ 2 │ │ 3 │             │
│  ├───┤ ├───┤ ├───┤             │
│  │ 4 │ │ 5 │ │ 6 │             │
│  ├───┤ ├───┤ ├───┤             │
│  │ 7 │ │ 8 │ │ 9 │             │
│  ├───┤ ├───┤ ├───┤             │
│  │   │ │ 0 │ │ ⌫ │             │
│  └───┘ └───┘ └───┘             │
│                                 │
│  ☑ Enable Biometric Login       │
└─────────────────────────────────┘
```

---

### MWA-17 — Error Handling / Global Error Screen

```
┌─────────────────────────────────┐
│  ←  Something Went Wrong        │
├─────────────────────────────────┤
│                                 │
│                                 │
│         ❌                      │
│                                 │
│      Oops! An error occurred    │
│                                 │
│  ┌───────────────────────────┐  │
│  │  Error ID: ERR-0042       │  │
│  │  Module: Payment API      │  │
│  │  Time: 10 Sep 2026 09:15  │  │
│  └───────────────────────────┘  │
│                                 │
│  Transaction could not be       │
│  completed. Your money is safe. │
│                                 │
│  ┌───────────────────────────┐  │
│  │         TRY AGAIN         │  │
│  └───────────────────────────┘  │
│  ┌───────────────────────────┐  │
│  │      CONTACT SUPPORT      │  │
│  └───────────────────────────┘  │
└─────────────────────────────────┘
```

---

### MWA-18 — UI Component Library / Design System Screen

```
┌─────────────────────────────────┐
│  UI Components Preview          │
├─────────────────────────────────┤
│                                 │
│  Buttons                        │
│  ┌───────────────────────────┐  │
│  │  PRIMARY BUTTON           │  │
│  └───────────────────────────┘  │
│  ┌ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┐  │
│   SECONDARY BUTTON              │
│  └ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┘  │
│                                 │
│  Typography                     │
│  H1 — Screen Title              │
│  H2 — Section Heading           │
│  Body — Regular text content    │
│  Caption — Small helper text    │
│                                 │
│  Input Field                    │
│  ┌───────────────────────────┐  │
│  │ Placeholder text          │  │
│  └───────────────────────────┘  │
│  ⚠ Error helper text            │
│                                 │
│  Toast: [ ✅ Success message ]  │
└─────────────────────────────────┘
```

---

### MWA-19 — Push Notifications (FCM) Screen

```
┌─────────────────────────────────┐
│  ←  Notifications               │
├─────────────────────────────────┤
│                                 │
│  Notification Preferences       │
│  ─────────────────────────────  │
│  Transaction Alerts    [ ON  ◉] │
│  Load / Unload Alerts  [ ON  ◉] │
│  KYC Updates           [ ON  ◉] │
│  Promotional           [ OFF ○] │
│                                 │
│  Recent Notifications           │
│  ─────────────────────────────  │
│  ┌───────────────────────────┐  │
│  │ ✅ Payment of ₹500 sent   │  │
│  │    Today, 2:30 PM         │  │
│  └───────────────────────────┘  │
│  ┌───────────────────────────┐  │
│  │ 💳 Wallet loaded ₹2000   │  │
│  │    Today, 10:15 AM        │  │
│  └───────────────────────────┘  │
│  ┌───────────────────────────┐  │
│  │ 🔔 KYC Approved!          │  │
│  │    Yesterday              │  │
│  └───────────────────────────┘  │
└─────────────────────────────────┘
```

---

### MWA-20 — Analytics & Crash Reporting Screen

```
┌─────────────────────────────────┐
│  ←  App Analytics               │
├─────────────────────────────────┤
│                                 │
│  Usage Statistics               │
│  ─────────────────────────────  │
│  Sessions Today:       12       │
│  Avg Session Duration: 3m 24s   │
│  Transactions Today:   8        │
│                                 │
│  Transaction Volume (This Week) │
│  ┌───────────────────────────┐  │
│  │  ▁▃▅▇█▇▅  Bar Chart      │  │
│  │  M T W T F S S            │  │
│  └───────────────────────────┘  │
│                                 │
│  Crash Reports                  │
│  ─────────────────────────────  │
│  ✅ No crashes in last 7 days   │
│                                 │
│  App Version: 1.0.0 (Build 42) │
│  Firebase Project: mwa-prod     │
│                                 │
│  ┌───────────────────────────┐  │
│  │   VIEW FULL REPORT        │  │
│  └───────────────────────────┘  │
└─────────────────────────────────┘
```

