# SEIR Foundations — Lesson 1 Lab Notes

**Student:** Sid Owsley  
**Assignment:** Week 3 — EC2 and COBOL Banking  
**Environment:** AWS EC2, Amazon Linux 2023

## Initial Deployment Practice — November 2, 2026

**Instance ID:** i-0fce237d4cf96e52e  
**Status:** Initial deployment completed; qualification as one of the seven required lab runs has not been verified.

### What I Did

I launched an EC2 t3.micro instance and connected to it using SSH from Windows PowerShell. I worked through installing the Balerica Legacy Bank application, configuring Python FastAPI, and testing the COBOL banking programs.

The deployment required some troubleshooting because the application wasn't installed correctly during the initial setup.

### Problems I Encountered and How I Fixed Them

**1. Missing Legacy Bank application**

The `/opt/balerica-bank` directory wasn't available after the initial deployment. I manually cloned the SEIR Foundations repository and ran the installation script.

**2. SSH connection problems**

My SSH sessions disconnected while I was working. I learned how to reconnect to EC2 and restart the FastAPI application when necessary.

**3. FastAPI payment request error**

My initial payment request failed with HTTP 422 because of a JSON formatting problem. I corrected the request using Python and successfully submitted a payment.

### Commands I Used

Connect to EC2:

```bash
ssh -i "SEIR-Lab-Key.pem" ec2-user@<EC2-PUBLIC-IP>
```

Start FastAPI:

```bash
cd /opt/balerica-bank
source venv/bin/activate
uvicorn app.main:app --host 127.0.0.1 --port 8000
```

Test the account lookup:

```bash
./cobol/bin/account_lookup 100001
```

Check API status:

```bash
curl -s http://127.0.0.1:8000/status
```

View transactions:

```bash
curl -s http://127.0.0.1:8000/transactions
```

### Verification Results

- Successfully retrieved Alice Johnson's account information.
- Verified that the FastAPI service was online.
- Successfully processed a $25.00 payment.
- Confirmed the payment was POSTED and APPROVED.
- Verified the account balance was $4,975.00.
- Confirmed the transaction appeared in the transaction history.

An exact API response field I observed was:

```text
"core_banking":"GnuCOBOL"
```

### What I Learned

I learned more about connecting to EC2 using SSH, navigating Linux directories, troubleshooting installation problems, and managing a Python virtual environment.

I also gained a better understanding of how a COBOL banking application can communicate with a modern REST API.

## Mistakes I Made

- Initially used incorrect EC2 User Data.
- Assumed the application installation had completed successfully.
- Had trouble distinguishing between my local PowerShell terminal and my EC2 SSH session.
- Submitted a payment request with incorrectly formatted JSON.

## Commands I Now Know by Heart

- `pwd`
- `ls`
- `cd`
- `ssh`
- `git clone`
- `source venv/bin/activate`
- `uvicorn`
- `curl`

## Upcoming Lab Runs

The seven required manual deployments will be recorded separately with their actual instance IDs, screenshots, boot times, troubleshooting notes, and results.

## COBOL Practice

Return codes 0, 4, 8, and 12, along with fixed-width ledger decoding, will be documented after completing and verifying each test.
