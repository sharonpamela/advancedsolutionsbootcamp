.. _flow_secure_app:

----------------
Flow: Verify Application
----------------

Overview
++++++++

.. note::

  Estimated time to complete: 15-30 MINUTES

In this exercise you will verify that the security policy created before is in effect. For this, the Calm blueprint previously launched should be provisioned successfully.


Verify The Flow Security Policies
++++++++++++++++++++++++++++++++++++++++++

Verify Application Deployment
-----------------------------------------
- incorporate the visualization piece in here
- looking for VM counts inside the security policy
- looking for outbound detected traffic flows

Access Task Manager Application
-----------------------------------------
- VERIFY THE APP FUNCTIONALITY: ADD TASK Workloads

Ping the DB VM
-----------------------------------------
- Proof security policy is active but not blocking any traffic.

Apply Security Policy
-----------------------------------------
- No one outside of the production and PC environment will be able to access the Task Manager Application.

Edit the Categories of a Running VM
-----------------------------------------
- Change windows client from environment: dev to environment: prod
- Verify WindowsClient can access the task manager app

##################################################################
Rest of flow lab
- isolation:
    - Environment: dev-abc and Environment:prod-abc applied to the client and LB VMs
- quarantine:
    - strict quarantine the db VM and confirm the app stops working
##################################################################


Takeaways
+++++++++
