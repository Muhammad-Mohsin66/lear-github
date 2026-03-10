# Microsoft 365 for Mac – "Ready to View Documents" Troubleshooting Guide

> **Symptom:** Word (or another Office app) on macOS shows a banner like:
> *"Your account … can view documents, but it doesn't allow editing on a Mac."*

This guide explains why it happens and how to fix it yourself, step by step.

---

## Table of Contents

1. [Why This Happens (and Why It Can Work Fine Then Suddenly Stop)](#why-this-happens)
2. [Quick Checklist Before You Start](#quick-checklist)
3. [Step 1 – Sign Out and Back In to the Correct Account](#step-1)
4. [Step 2 – Check Activation Status Inside Word](#step-2)
5. [Step 3 – Clear Office / Identity Tokens from macOS Keychain](#step-3)
6. [Step 4 – Update Office via Microsoft AutoUpdate](#step-4)
7. [Step 5 – Try Activating from Another Office App](#step-5)
8. [Step 6 – Workaround: Use Office Online](#step-6)
9. [When You Cannot Fix It Yourself](#when-you-cannot-fix-it-yourself)
10. [Copy-Paste Message Template for IT Admins](#it-message-template)

---

## Why This Happens {#why-this-happens}

Microsoft 365 uses **token-based activation** that is refreshed periodically (typically every 30 days, but also on each sign-in). Several events can break it mid-session:

| Cause | Explanation |
|---|---|
| **Token / activation refresh** | Office silently contacts Microsoft's licensing servers in the background. If it cannot renew the activation token (network block, expired session), Word falls into view-only mode. |
| **License assignment change** | An IT admin added or changed your license. The new license may include only web/mobile access, not desktop apps. |
| **Stale Keychain credentials** | macOS saves old Office sign-in tokens. When they expire or conflict, Office cannot re-authenticate automatically. |
| **Multiple Microsoft accounts** | Word can silently switch to a different signed-in account that has no desktop license. |
| **Office update** | A new Office version occasionally resets activation state and requires you to sign in again. |

This is why the product worked fine for several days and then stopped without any action on your part.

---

## Quick Checklist {#quick-checklist}

Before following the detailed steps, run through this list:

- [ ] Am I signed in with the **correct school/work account** (not a personal Microsoft account)?
- [ ] Can I edit documents in **Word Online** ([office.com](https://www.office.com)) with the same account?
- [ ] Is my **macOS up to date**?
- [ ] Is **Microsoft Office up to date**?

If Word Online works but the desktop app does not → your license may not include desktop apps (see [Step 6](#step-6) and [When You Cannot Fix It Yourself](#when-you-cannot-fix-it-yourself)).

---

## Step 1 – Sign Out and Back In to the Correct Account {#step-1}

1. Open **Word**.
2. In the menu bar, click **Word → Sign Out** and sign out completely.
3. Quit Word: **Cmd + Q**.
4. Reopen Word.
5. Click **Sign In** and enter your **school or work email address**.
6. Complete multi-factor authentication if prompted.
7. Try editing a document.

> **Tip:** Make sure you are not accidentally signing in with a personal `@outlook.com` or `@gmail.com` account. Schools often provide an address like `student@university.edu`.

---

## Step 2 – Check Activation Status Inside Word {#step-2}

1. Open **Word**.
2. Go to **Word → Preferences → Account** (or **File → Account** depending on your version).
3. Look at the **Product Information** section.
   - ✅ **"Subscription Product – Microsoft 365"** with your email = activated correctly.
   - ❌ **"Unlicensed Product"** or **"View Only"** = activation failed.
4. If unlicensed, click **Sign In** or **Change License** and sign in with your school account.

---

## Step 3 – Clear Office / Identity Tokens from macOS Keychain {#step-3}

Stale saved tokens are one of the most common causes of this issue.

1. Open **Keychain Access** (use Spotlight: **Cmd + Space** → type *Keychain Access*).
2. In the search box at the top right, search for each of the following terms one at a time and delete any items found:
   - `Microsoft Office`
   - `Microsoft Identity`
   - `ADAL`
   - `MSAL`
   - `com.microsoft`
3. For each item: right-click → **Delete** → confirm.
4. **Restart your Mac.**
5. Open Word and sign in fresh with your school account.

> **Note:** Removing these entries is safe. They are cached credentials that will be recreated when you sign in again. You will be asked to sign into Office apps once more after restarting.

---

## Step 4 – Update Office via Microsoft AutoUpdate {#step-4}

Running an outdated version of Office can cause licensing errors.

1. In Word, click **Help → Check for Updates** in the menu bar.
2. **Microsoft AutoUpdate** will open. Click **Update All**.
3. Wait for all updates to install.
4. Reboot your Mac and test Word again.

If **Help → Check for Updates** is missing, download **Microsoft AutoUpdate** directly from [Microsoft's support page](https://support.microsoft.com/en-us/office/update-office-for-mac-automatically-bfd1e497-c24d-4754-92ab-910a4074d7c1).

---

## Step 5 – Try Activating from Another Office App {#step-5}

Sometimes one Office app is stuck in a bad state but another can trigger activation for the whole suite.

1. Close Word completely (**Cmd + Q**).
2. Open **Excel** (or **PowerPoint**, or **Outlook**).
3. Sign in when prompted.
4. Once activated in Excel, reopen **Word** and check if editing is now available.

---

## Step 6 – Workaround: Use Office Online {#step-6}

If the desktop app is not working, you can still create and edit documents fully in the browser:

1. Go to [https://www.office.com](https://www.office.com).
2. Sign in with your school account.
3. Click **Word** to open Word Online.
4. Create or upload your document and edit it there.

> **What this tells you:** If Word Online works but the desktop app does not, your Microsoft 365 license likely provides **web and mobile access only**, not desktop (Mac/PC) apps. This is a license-level restriction that only your IT admin can change.

---

## When You Cannot Fix It Yourself {#when-you-cannot-fix-it-yourself}

If you have completed all the steps above and Word still shows the view-only message, the issue is **a license restriction set by your IT administrator**. Common scenarios:

| Scenario | What IT needs to do |
|---|---|
| License assigned is "Microsoft 365 Business Basic" or "A1" | Upgrade to a license that includes desktop apps (e.g., Microsoft 365 Apps for Students, A3, or A5) |
| Desktop activation disabled for your account | Enable the **"Apps for Office"** toggle in the Microsoft 365 admin portal for your account |
| Multiple licenses conflicting | Remove the old license and reassign the correct one |

You **cannot change these settings yourself** — they are controlled in the Microsoft 365 admin portal by your IT department.

---

## Copy-Paste Message Template for IT Admins {#it-message-template}

Send this to your IT department for a fast resolution:

---

```
Subject: Microsoft 365 Desktop Apps Not Activated – Editing Disabled on Mac

Hi IT Team,

I am experiencing an issue with Microsoft Word on macOS. The app displays:

  "Your account [my email] can view documents, but it doesn't allow
   editing on a Mac. To edit, use another account to activate Microsoft 365."

Steps I have already tried (without success):
  1. Signed out and back in with my school account.
  2. Cleared Microsoft Office / MSAL / ADAL tokens from macOS Keychain.
  3. Updated Office to the latest version via Microsoft AutoUpdate.
  4. Restarted my Mac.

I can edit documents in Word Online, which suggests my license may be
web-only (e.g., Microsoft 365 Business Basic or A1) or desktop activation
may be disabled for my account.

Could you please:
  - Verify my license includes Microsoft 365 desktop apps for Mac.
  - Enable desktop activation for my account in the Microsoft 365 admin portal.
  - Or upgrade my license to one that includes Office desktop apps
    (e.g., Microsoft 365 Apps for Students, A3, or A5).

Thank you!
[Your Name]
[Student / Employee ID]
```

---

## Additional Resources

- [Microsoft Support: Activate Office for Mac](https://support.microsoft.com/en-us/office/activate-office-for-mac-7f6646b1-bb14-422a-9ad4-a53410fcefb2)
- [Microsoft Support: What to try if you can't install or activate Office](https://support.microsoft.com/en-us/office/what-to-try-if-you-can-t-install-or-activate-office-for-mac-5efba2b4-b1e6-4e5f-bf3c-6ab945d03dea)
- [Compare Microsoft 365 Education plans](https://www.microsoft.com/en-us/microsoft-365/academic/compare-office-365-education-plans)
