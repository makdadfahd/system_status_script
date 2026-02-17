# Disk Alert Script

This script checks disk usage for `/` and alerts if it exceeds a threshold.

## Features

- Alerts if usage exceeds threshold (default 80%)  
- Shows actual percentage and threshold  
- Useful for monitoring servers  

## Code

```bash
#!/bin/bash

usage=$(df -h | awk '$6 == "/" {print $5}' | sed 's/.$//')
threshold=80  

if [ $usage -gt $threshold ]; then
        echo "Alert!! Disk is almost full "
        echo "The actual percentage is : $usage%"
        echo "The threshold is : $threshold%"
else 
        echo "The actual percentage is : $usage%"
        echo "Disk usage is normal"
fi 
