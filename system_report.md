# System Report Script

This script is a mini Bash CLI tool to display system information with colors.

## Features

- Shows RAM: Total, Used, Available
- Shows Disk: Total, Used, Available
- Shows Uptime
- Shows Users: names and count
- Color-coded sections for better readability

## Code

```bash
#!/bin/bash

# Couleurs
RED='\033[0;31m'
GREEN='\033[0;32m'
BLUE='\033[0;34m'
MAGENTA='\033[0;35m'
CYAN='\033[0;36m'
NC='\033[0m'

# Header
echo -e "${BLUE}===== SYSTEM STATUS =====${NC}"

# RAM
total=$(free -h | grep "Mem" | awk '{print $2}')
used=$(free -h | grep "Mem" | awk '{print $3}')
available=$(free -h | grep "Mem" | awk '{print $7}')
echo -e "${RED}========== RAM ==========${NC}"
echo "Total : $total    Used : $used    Available : $available"

# Disk
disque_t=$(df -h | awk '$6 == "/" {print $2}')
disque_u=$(df -h | awk '$6 == "/" {print $3}')
disque_a=$(df -h | awk '$6 == "/" {print $4}')
echo -e "${GREEN}======= DISK =======${NC}"
echo "Total : $disque_t    Used : $disque_u    Available : $disque_a"

# Uptime
uptime=$(uptime | awk -F'up |,' '{print $2}')
echo -e "${MAGENTA}====== UPTIME =======${NC}"
echo "You have been connected for $uptime" 

# Users
number=$(users | tr ' ' '\n' | uniq | wc -l)
user=$(users | tr ' ' '\n' | uniq )
echo -e "${CYAN}====== USERS ======${NC}"
echo "Users are : $user"
echo "Number of users is : $number"
