---
share: true
---


The **0x11** tool is a Bash-based automation script designed for penetration testing workflows. It streamlines reconnaissance and vulnerability detection by providing a simple menu interface to run tools like `amass`, `gobuster`, `dirsearch`, and `sqlmap`. It automatically checks for dependencies, installs missing ones, and saves scan results to organized output files. Ideal for beginners and professionals, it enhances efficiency in security assessments. Future updates will add more modules and improvements.


```Bash
#!/bin/bash

Installing() {
    local cmd="$1" pkg="$2"
    if ! command -v "$cmd" >/dev/null 2>&1; then
        echo "[*] $cmd not found — installing $pkg"
        sudo apt update -y
        sudo apt install -y "$pkg"
    else
        echo "[*] $cmd is already installed."
    fi
}

safe_name() {
    local s="$1"
    s="${s#http://}"
    s="${s#https://}"
    s="${s%%/*}"
    echo "$s" | sed 's/[^A-Za-z0-9._-]/_/g'
}

ping_sweep() {
    read -r -p "Enter IP base (e.g. 192.168.1): " base
    if [[ -z "$base" ]]; then
        echo "[!] Empty input"
        return 1
    fi

    echo "[*] Scanning $base.1-254 ..."
    for i in $(seq 1 254); do
        ip="$base.$i"
        ( ping -c 1 -W 1 "$ip" >/dev/null 2>&1 && echo "$ip is up" ) &
    done
    wait
    echo "[*] Done."
}

recon() {
    echo "Recon options:"
    echo "1) amass"
    echo "2) dirb"
    read -r -p "Choose: " ch
    read -r -p "Target (domain): " target
    if [[ -z "$target" ]]; 
    then
        echo "[!] Empty target"
        return 1
    fi
    tfile=$(safe_name "$target")
    case "$ch" in
        1)
            Installing amass amass
            echo "[*] Running: amass enum -d $target"
            amass enum -d "$target" -o "${tfile}_amass.txt"
            echo "[+] Saved: ${tfile}_amass.txt"
            ;;
        2)
            Installing dirb dirb
            echo "[*] Running: dirb https://$target"
            dirb "https://$target"
            ;;
        *)
            echo "Invalid choice"
            ;;
    esac
}

scanning() {
    echo "Scan options: 1) dirsearch  2) gobuster"
    read -r -p "Choose [1/2]: " ch
    read -r -p "Target (URL): " target
    if [[ -z "$target" ]]; then
        echo "[!] Empty target"
        return 1
    fi
    tfile=$(safe_name "$target")
    WORDLIST="/usr/share/wordlists/dirb/common.txt"
    case "$ch" in
        1)
            Installing dirsearch dirsearch
            echo "[*] Running dirsearch -u $target"
            dirsearch -u "$target" -e php,html,js -o "${tfile}_dirsearch.txt"
            echo "[+] Saved: ${tfile}_dirsearch.txt"
            ;;
        2)
            Installing gobuster gobuster
            echo "[*] Running gobuster -u $target -w $WORDLIST"
            gobuster dir -u "$target" -w "$WORDLIST" -o "${tfile}_gobuster.txt"
            echo "[+] Saved: ${tfile}_gobuster.txt"
            ;;
        *)
            echo "Invalid choice"
            ;;
    esac
}

vuln() {
    echo "Vuln options: 1) sqlmap"
    read -r -p "Choose [1]: " ch
    read -r -p "Target (URL): " target
    if [[ -z "$target" ]]; then
        echo "[!] Empty target"
        return 1
    fi
    case "$ch" in
        1)
            Installing sqlmap sqlmap
            mkdir -p reports
            echo "[*] Running basic sqlmap scan (reports/sqlmap)"
            sqlmap -u "$target" --batch --output-dir=reports
            echo "[+] Check: reports"
            ;;
        *)
            echo "Invalid choice"
            ;;
    esac
}

echo "Welcome with My tool 0x11"
echo "  _____           __   __ "
echo " / ___ \\ \\ \\ / / /_ | /_ |"
echo "| |   | | \\ V /   | |  | |"
echo "| |   | |  > <    | |  | |"
echo "| |___| | / . \\   | |  | |"
echo " \\__
___/ /_/ \\_\\  |_|  |_|"
echo

echo "**********************"
echo " Information Gathering"
echo "     More Simple      "
echo "**********************"
while true; do
    echo
    echo "1) Ping sweep"
    echo "2) Recon (amass/dirb)"
    echo "3) Scanning (dirsearch/gobuster)"
    echo "4) Vulnerability (sqlmap)"
    echo "q) Quit"
    read -r -p "Choose an option: " choice

    case "$choice" in
        1) ping_sweep ;;
        2) recon ;;
        3) scanning ;;
        4) vuln ;;
        q|Q) echo "Goodbye!"; break ;;
        *) echo "[!] Invalid selection, try again." ;;
    esac
done

```
