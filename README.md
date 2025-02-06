# ec2-backup-s3
# EC2 Instance Backup to S3

This project demonstrates how to automatically back up files from an EC2 instance to an S3 bucket using AWS CLI and cron jobs.

## Steps to Implement:
1. **Create an S3 Bucket**  
2. **Launch an EC2 Instance** (Ubuntu, `t2.micro`)  
3. **Install AWS CLI on EC2**  
4. **Create Sample Files** (`sample1.txt`, `sample2.txt`)  
5. **Automate Backups using Cron Job**  
6. **Create a Backup Script** (Sync folder to S3)  
7. **Restore Backup from S3**  
8. **Testing**: Create `testing.txt`, wait 5 minutes, and verify backup in S3.

## Backup Script (`backup_script.sh`)

```bash
#!/bin/bash

# Define variables
BACKUP_DIR="/home/ubuntu/backup"
S3_BUCKET="your-s3-bucket-name"
TIMESTAMP=$(date +%Y%m%d%H%M%S)

# Create a backup directory if it doesn’t exist
mkdir -p $BACKUP_DIR

# Copy home directory files to the backup directory
cp -r /home/ubuntu/*.txt $BACKUP_DIR/

# Sync the backup folder to S3
aws s3 sync $BACKUP_DIR s3://$S3_BUCKET/backup_$TIMESTAMP/

echo "Backup completed at $(date)"
