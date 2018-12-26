.. _flow_verify_app:

----------------
Flow: Verify Application
----------------

Overview
++++++++

.. note::

  Estimated time to complete: 15-30 MINUTES

In this exercise you will verify that the Flow security policy is monitoring the new application. For this, the Calm blueprint previously launched should be provisioned successfully.


Verify The Flow Application Security Policy
++++++++++++++++++++++++++++++++++++++++++

Verify Application Deployment
-----------------------------------------
- incorporate the visualization piece in here
- looking for VM counts inside the security policy
- looking for outbound detected traffic flows

Access Task Manager Application
-----------------------------------------
Before evaluating the Flow security policy, verify that the Task Manager application is running.

Open the Console of the Windows client VM through the Calm abc_TaskManager Application. Selecting the Application, click Services, and open the Windows Client service.

Find the IP of the newly deployed Load Balancer VM by selecting the abc_TaskManager application, click Services and select the HAProxy service.

From the Windows Client VM open a web browser and enter the IP address of the load balancer. Confirm that a Task Manager application loads and that tasks can be added or deleted from the web interface.


Verify Application is Categorized
---------------------------------
##VERIFY VM COUNTS HERE##


Access the Restricted DB Tier
-----------------------------------------
The application security policy does not allow any access to the database tier, but this policy is in monitor mode. Confirm that the Windows client VM can ping the database VM.


Add Flows to a Policy Using Flow Visualization
..............................................

View the detected traffic flows from Environment: Dev
-----------------------------------------------------

Navigate to **Explore > Security Policies > App-TaskMan-abc** to view the detected traffic flows from **Environment: Dev**

Confirm that **Environment: Dev** is listed as a source to **AppTier: TMLB-abc**. This can take a few minutes to appear.

.. figure:: images/flow_viz.png

Hover over the yellow flow line from **Environment: Dev** to **AppTier: TMLB-abc** to view the protocol and connection information.

Click the yellow flow line to view a detailed graph of connection attempts.

.. figure:: images/network_flows.png

Add The Detected Flow to The Security Policy
--------------------------------------------

Select **Update** in the top right corner to edit the policy.

Click **Next** and view the detected traffic flows.

Hover over the **Environment: Dev** source in the inbound list.

Select the green check box to add this source to the inbound allowed list.

.. figure:: images/add_env_flow.png

Select OK to Add to Rule

Hover over the blue **Environment: Dev** source and select the pencil icon to edit the rule.

Select the pencil on **AppTier: TMLB-abc** to define specific ports and protocols.

Currently ICMP is allowed due to the ping detected in the previous task.

Select **Save** to save the ICMP rule.

Select **Next** to review the changes to the policy.

Move Policy from **Monitoring** Mode to **Applied** Mode
------------------------------------------------------------

Now that the policy is complete, move it from monitor mode to apply mode.

Select **Apply Now** to save the policy and move it into apply mode.

Navigate to **Explore > Security Policies > App-TaskMan-abc**.

Confirm that **Environment: Dev** shows in blue as an allowed source.

Attempt to send traffic from another source such as your remote desktop or from the DB to the Web tier.

Is this traffic blocked?



Edit the Categories of a Running VM (MAYBE WE DONT DO THIS ONE ANYMORE)
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
