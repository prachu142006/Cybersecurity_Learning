# Day 02 - Practical Investigation

## Objective
Investigate basic network information, running processes,
authentication logs and firewall status on Kali Linux.

## Commands Used

1. ip -br addr
2. ss -tuln
3. ps aux
4. sudo journalctl -u ssh -n 30 --no-pager
5. sudo journalctl -n 50 --no-pager
6. sudo ufw status verbose

## Investigation Areas

- Network interfaces
- Listening ports
- Running processes
- Authentication events
- Firewall status

## Learning Outcome

I learned how network information, system processes
and authentication logs help SOC Analysts investigate
potential security risks.

## Conclusion

Basic system investigation helps identify unusual
activities and understand the attack surface.

