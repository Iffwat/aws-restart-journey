# EC2 Lab Notes

Use this file for observations from your own lab. Keep notes specific to what actually happened.

## Apache service checks
```bash
sudo systemctl status httpd
sudo systemctl enable httpd
sudo systemctl start httpd
```

## Test the local web-server response
```bash
curl -I http://localhost
curl http://localhost
```

## HTTP troubleshooting checklist
1. Confirm the instance is running and status checks pass.
2. Confirm the attached security group permits inbound TCP port 80 from the intended source.
3. Confirm Apache is active.
4. Check subnet routing, internet gateway, and public addressing when testing from the internet.
5. Check network ACLs if connectivity is still blocked.

## Reminders
- A security-group rule alone does not guarantee internet reachability.
- Avoid exposing SSH (TCP 22) to the entire internet.
- Stop an instance before changing its instance type.
- Increasing EBS size may require expanding the partition and filesystem in the guest OS.
- Termination protection is not a backup.

## My observations
- **Date:**
- **What I did:**
- **What happened:**
- **Issue / error:**
- **How I resolved it:**
- **What I learned:**
