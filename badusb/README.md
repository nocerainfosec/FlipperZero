# Use Base64 Powerhsell Commands for FlipperZero
## 💥 Why You Should Use Base64 PowerShell Commands in Flipper Zero BadUSB Payloads

So if you've ever tried to send a command with Flipper Zero's BadUSB and it totally messed up something like `https://`, you're not crazy. It’s a **known issue** and it happens a lot.

The short version?
Flipper sends **US keyboard scancodes**, but if your target is using a different layout (like DE, FR, or whatever), then symbols like `:`, `/`, `@`, and others just don’t come out right.

Also, Flipper types fast as hell, and sometimes the OS just can’t keep up — stuff gets skipped, keys get dropped, modifiers don’t work. It’s a mess.

---

### ❌ Example of What Goes Wrong

You try to type:

```powershell
Start-Process "https://nocerainfosec.github.io/pranks"
```

But Flipper says otherwise


### ✅ The Workaround: Use PowerShell Base64 Mode

Instead of typing out the whole command raw, we let PowerShell decode and run it from Base64. It’s clean, fast, and **way more reliable**.

So like, do this:

```powershell
powershell -EncodedCommand UwB0AGEAcgB0AC0AUA...etc
```

Then in your Ducky Script:

```ducky
GUI r
DELAY 300
STRING powershell -encodedCommand UwB0AGEAcgB0AC0AUA...
ENTER
```

Just sends plain text letters and numbers. No weird symbols. No broken URLs.

---

### 🔧 How to Encode It

Wanna do it yourself? Easy.

1. Open PowerShell
2. Run this:

```powershell
[Convert]::ToBase64String([Text.Encoding]::Unicode.GetBytes("Start-Process 'https://nocerainfosec.github.io/pranks'"))
```

3. Boom — it spits out the Base64. Use that in your payload.

---

### 😬 Why You Even Need This

Here’s what usually breaks:

* `:` needs Shift + ; on US layout → not the same on others.
* `/` sometimes doesn’t register at all.
* URLs like `https://` get turned into `https;/ /`
* Some symbols just don’t work on non-US layouts at all.

Also Flipper doesn’t know what layout the computer has, so it just guesses — badly.

---

### 🔒 TL;DR

Using Base64 PowerShell commands is the **best way to avoid layout bugs and dumb symbol errors** in Flipper Zero BadUSB payloads.

Don’t fight with `:`, `/`, or `@`. Just encode it once, and you're golden. 💯
