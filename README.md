# 🕵️ MyLast

## 🌟 Overview

**MyLast** is a Bash script designed to analyze authentication logs within `/var/log/`. It reproduces the functionality of the standard Linux `last` and `lastb` commands by parsing `auth.log` files, including historical logs compressed with `gzip`.

---

## ✨ Key Idea

* **State machine:** Built the session recosntruction model on a **Finite State Machine** architecture.

---

## 🔧 Features and Tools

* **Successful Logins (-l):** Analyzes the full lifecycle of successful user sessions.
* **Failed Logins (-lb):** Isolates unauthorized access attempts.
* **Temporal Filtering:**
* **-s (Since):** View sessions starting after a specific date.
* **-t (Until):** View sessions ending before a specific date.
* **-p (Present):** Audit who was logged in at a specific timestamp.


* **Output Formatting:** Displays data in a clean, tabular layout with calculated session durations.

---

## 🚀 Installation

### Option 1: Quick Setup

```bash
# Clone and prepare the script
git clone https://github.com/Dontmindmeifido/MyLast.git && cd MyLast && chmod +x mylast.sh

```

### Option 2: Run as Root

> [!IMPORTANT]
> Because `/var/log/auth.log` is restricted for security, this script must be run with `sudo`.

```bash
sudo ./mylast.sh -l

```

---

## 📂 State Machine Architecture

* **Queue:** Stores users currently logged in but not yet disconnected.
* **Session:** Stores completed session objects once a "removed session" or "power down" event is detected.
* **Auxiliary Utilities:**
* `get_duration`: Calculates duration.
* `get_date` / `get_time`: Parses authlog timestamps for processing.



---

## 📊 Usage Examples

### Standard Audit

```bash
# View all successful login history
sudo ./mylast.sh -l

# View failed login attempts
sudo ./mylast.sh -lb

```

### Advanced Filtering

```bash
# Show only the last 5 sessions
sudo ./mylast.sh -l -n 5

# Check who was active during a specific incident
sudo ./mylast.sh -l -p 2025-12-25-14-30

```

---

## 🔄 Dependencies

* `bash`
* `less`
* `awk` & `grep`

---

## 📜 License

This project is licensed under ME.

## 👏 Credits

* **Developer:** Ruslan Gaitur
* **Academic Context:** Developed as part of the First Semester curriculum at the **University of Bucharest**.