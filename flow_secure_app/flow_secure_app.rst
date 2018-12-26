.. _flow_secure_app:

----------------
Flow: Secure App
----------------

Overview
++++++++

.. note::

  Estimated time to complete: 15-30 MINUTES

In this exercise you will create a security policy to restrict communication between the application VMs.

Secure Applications with Flow
++++++++++++++++++++++++++++++++++++++++++

Create and Assign Categories
............................

Update **AppType** with a new category value **TaskMan-abc**.
----------------------------------------------------------------

Log on to the Prism Central environment and navigate to the <icon>hamburger menu. Once there click on **Virtual Infrastructure > Categories**.

Click the check box beside **AppType**. Click **Actions > Update**.

Scroll down and click the plus sign beside the last entry.

Enter **TaskMan-abc**, replacing abc with your initials and click **Save**.

Update **AppTier** with 3 New Category Values
---------------------------------------------

Select the check box beside **AppTier**. Click **Actions > Update**.

Scroll down and click the plus sign beside the last entry.

Enter **TMWeb-abc**, replacing abc with your initials.

Repeat the above steps for TMDB-abc, and TMLB-abc.

Click **Save**.


Assign Categories to the Calm Blueprint.
---------------------------------------------------------

Within the <icon>hamburger menu in Prism Central, navigate to **Services > Calm**.

Click on the Blueprint and select the **abc_TaskManager** blueprint you imported and edited earlier.

Click on the WebServer_AHV service in the blueprint pane > Click the **VM** tab in the right side menu.

Scroll down until you see the **CATEGORIES** section > Click **Key:Value** > Select **AppTier: TMWeb-abc** and **AppType: TaskMan-abc**.

Repeat the same steps with each of the services in the blueprint:
HAProxy -> AppTier: TMLB-abc and AppType: TaskMan-abc
MySQLAHV -> AppTier: TMDB-abc and AppType: TaskMan-abc
WindowsClient -> Environment: Dev

Launch a Service from the Calm Blueprint.
-----------------------------------------

Launch the application blueprint to initiate the creation of the VMs associated with the application. These VMs will be created with the appropriate network and category settings from the blueprint.

Select Save to commit any changes.

Click Launch and name the application **abc_TaskManager**, replacing abc with your initials.

Finally, Click Create.

Move on to the next tasks while the application deploys.


Secure the Task Manager Application
...................................

Create a security policy to protect the Task Manager application.
--------------------------------------------------------------------

Navigate to the <icon>hamburger menu **Virtual Infrastructure > Policies > Security Policies**.

Click **Create Security Policy > Secure an Application**.

Fill out the following fields and click **Next**:

- **Name** - App-TaskMan-abc, replacing abc with your initials.
- **Purpose** - Protect the Task Manager application by restricting unnecessary access.
- **Secure this app** - AppType: TaskMan-abc.
Do NOT select the check box for the option **Filter the app type by category**.

Click **Next**

.. figure:: images/create_app_vm_sec_pol.png

Click on **Ok, Got it!** if prompted with the tutorial diagram.

Add Tiers to Security Policy
----------------------------

Click on **Set rules on App Tiers, instead**

Click on **+ Add Tier**

Select **AppTier: TMLB-abc** from the drop down.

Repeat for **AppTier: TMWeb-abc** and **AppTier: TMDB-abc**


Add New Inbound Source Production: Environment
----------------------------------------------

In the Inbound rules section, allow incoming traffic with the following steps:

- Leave **Whitelist Only** selected.
- Select **+ Add Source**.
- Leave **Add source by: Category** selected.
- Type **production** and select **Environment: Production**. Click Add.

Click + which appears on the left side of **AppTier: TMLB-abc**.

This opens the Create Inbound Rule window.

In the Protocol column, select **TCP** and type port 80 to allow web traffic into the load balancer. Click **Save**.

Add New Inbound Source Calm
---------------------------
Calm requires access to log into newly provisioned VMs.

- Select **+ Add Source**.
- Select **Add source by: Subnet/IP** using the drop down.
- Type enter the IP for Prism central followed by /32. Example: 10.20.X.39/32. Click Add.

Click + which appears on the left side of **AppTier: TMLB-abc** after completing the steps above.

This opens the Create Inbound Rule window.

In the Protocol column, select **TCP** and type port 22 to allow Calm to access Linux VMs. Click **Save**.

With the Subnet/IP inbound connection selected, repeat this step for all remaining tiers to allow TCP port 22 from Calm.

Add New Outbound Source
-----------------------
The newly provisioned VMs will need access to an external DNS server.

Change the outbound source to **Whitelist Only**
- Select **+ Add Destination**.
- Select **Add destination by: Subnet/IP** using the drop down.
- Type enter the IP for DNS followed by /32. Example: 10.20.X.40/32. Click Add.

Click + which appears on the right side of **AppTier: TMDB-abc** after completing the steps above.

This opens the Create Outbound Rule window.

In the Protocol column, select **UDP** and type port 53. Click **Save**.
<image>

Set Rules within Application
----------------------------
Each tier of the application communicates with other tiers and the policy must allow this. Some tiers such as the load balancer and web do not require communication within the same tier.

Click **Set Rules within App**

Select AppTier: TMLB-abc and click on "No" under the question to disallow communication between VMs within this tier.

With the AppTier: TMLB-abc selected, click on the + sign net to the AppTier: TMWeb-abc.

This opens the Create Tier to Tier Rule window.

In the Protocol column, select **TCP** and type port 80. Click **Save**.
<image>

Select AppTier: TMWeb-abc and click on "No" under the question to disallow communication between VMs within this tier.

With the AppTier: TMWeb-abc selected, click on the + sign net to the AppTier: TMDB-abc.

This opens the Create Tier to Tier Rule window.

In the Protocol column, select **TCP** and type port 3306. Click **Save**.
<image>

Click **Next**.

Click **Save and Monitor**.

Takeaways
+++++++++

- Categories created in Prism Central are available inside Calm blueprints.
- Security policies leverage the text based categories in Prism Central.
- Calm Blueprints can deploy applications that are automatically secured with Flow. 
- Flow can restrict traffic on certain ports and protocols for VMs running on AHV.
- The policy is created in **Save and Monitor** mode, meaning traffic is not actually blocked until the policy is applied. This is helpful to learn the connections and ensure no traffic is blocked unintentionally.
