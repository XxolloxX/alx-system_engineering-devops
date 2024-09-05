Postmortem Report: Outage of Web Application Service
Issue Summary:

Duration: April 4, 2024, 14:00 - 16:30 UTC
Impact: Our web application service experienced a significant outage. Users reported that they were unable to access the application, resulting in a 90% service downtime. Users encountered HTTP 500 errors and could not complete transactions.
Root Cause: A misconfiguration in the load balancer resulted in an improper distribution of traffic, overwhelming a specific backend server and causing it to crash.
Timeline:

14:00 UTC: Issue detected. Users started reporting access issues via the support ticket system.
14:05 UTC: Monitoring alerts were triggered, indicating a spike in error rates and increased response times.
14:10 UTC: Initial investigation began. Logs showed increased error rates and server crashes. The first assumption was that the issue might be related to recent code deployments.
14:30 UTC: Misleading investigation path. Assumed the issue was due to a recent database schema change, leading to unnecessary database rollback attempts.
15:00 UTC: Investigation refocused. The team checked the load balancer configuration and found discrepancies in traffic distribution.
15:15 UTC: Incident escalated to the DevOps team for a deeper investigation of load balancer settings.
15:30 UTC: The root cause was identified as a misconfiguration in the load balancer settings, which led to uneven traffic distribution and server overload.
16:00 UTC: The load balancer configuration was corrected, and traffic was redistributed properly.
16:30 UTC: Service was fully restored, and normal operations resumed.
Root Cause and Resolution:

Root Cause: The issue was caused by a misconfiguration in the load balancer. Specifically, the load balancer was incorrectly routing a disproportionate amount of traffic to a single backend server, which could not handle the load, resulting in server crashes and HTTP 500 errors.
Resolution: The misconfiguration was corrected by updating the load balancer settings to ensure even distribution of traffic across all backend servers. Traffic was rebalanced, and the overloaded server was brought back online after being properly scaled.
Corrective and Preventative Measures:

Improvements:
Implement automated checks and validation for load balancer configurations.
Enhance monitoring to include alerts for potential load balancing issues and server overloads.
Tasks to Address the Issue:
Patch Load Balancer Configuration: Update the load balancer settings to ensure proper traffic distribution.
Add Automated Tests: Implement automated tests to verify load balancer configurations before deployment.
Enhance Monitoring: Improve monitoring and alerting systems to detect uneven traffic distribution and server performance issues early.
Conduct a Postmortem Review: Schedule a review meeting with all involved teams to discuss the incident and ensure all lessons learned are documented and acted upon.
This postmortem outlines the steps taken to identify and resolve the outage, and the measures put in place to prevent similar issues in the future.
