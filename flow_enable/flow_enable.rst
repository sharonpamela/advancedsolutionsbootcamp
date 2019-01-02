.. _flow_enable_and_lab_setup:

--------------------------
Flow: Enable and Lab Setup
--------------------------

Overview
++++++++

.. note::

  Estimated time to complete: 10-20 MINUTES

In this exercise you will enable Nutanix Flow and edit a blueprint within Calm that will be used to create an application that we will protect in the subsequent exercises.

Enabling Flow
++++++++++++++++++++++++++

Open https://<Prism-Central-IP>:9440/ in the Chrome browser and log in.

.. note::

  Do not use Firefox for the Flow policy steps in the following exercises.

From the navigation bar, click the question mark at the top right corner and expand the **New in Prism Central** section of the menu.

Click **Flow**.

Select the **Enable Flow** check box within the **Enable Flow** dialog box.


.. figure:: images/enable_flow.png


.. note::

  Flow can only be enabled once per Prism Central instance. If **Flow** displays a green check mark next to it, that means Flow has already been enabled for the Prism Central instance being used.

Click **Enable**


.. figure:: images/enable.png


Import Blueprint with Calm
++++++++++++++++++++++++++++

.. note::

In this section we will import a Calm Blueprint into Prism Central that will create and configure the VMs needed for this lab.

To import a Calm Blueprint, ensure Calm is enabled (Please see the Enable Calm optional lab if this isn't the case).

Download the blueprint for this lab at the following link:
<TODO BP link>

From the Dashboard in Prism, Click the <icon here> Navigation menu on the top left then select **Services** > **Calm**.

.. figure:: images/access_calm.png

Click on the blueprint icon from the menu on the left (hovering over all of the icons shows their labels).

Click **Upload Blueprint** and navigate to the blueprint provided for this course:

.. figure:: images/blueprint.png

Name the blueprint with your initials, **abc_TaskManager** and choose the **Default** project.

Once the blueprint finishes uploading, it will automatically open.

Let's configure the non-Flow related changes in this blueprint before continuing.

Update the credentials:
  Edit the credentials for Linux machines:
  Click on **Credentials** from the top menu.
  Select **CENTOS**.
  - Ensure the **Username** is **centos**
  - Ensure the **Secret Type** is set to **SSH Private Key**.
  - Paste the private key below into the field provided (include the begin and end tags with all dashes):
  .. code-block:: bash
     -----BEGIN RSA PRIVATE KEY-----
     MIIEowIBAAKCAQEAw6CZT4/gAj8hxptH/hck0D0bfptR+ibLci7bxSVJ7Q8hdv3a
     qXEPUHyisNUHI8xnUkvAeh63Tjoymc+No9Nf2C1hctmKwy0Dh3DSYul6MAkNOfQu
     2x3oT+ZajTem0SM3UJ6hmRmIvIimM1AoTFbrH7D3eWWaNKxwgIggD9chaq3EpqvN
     0DTdV/BWdQjqDAeurysg9qxKHis+JYpRHlisj+ES5pDnNXjGEDXcjDgjRRWypgtZ
     zyfjKcaNR3zUfOEe1jZeaBGjUDjkTfjWjs7uQcYptoYSb1N+yfudOGs2dTwlIh4g
     tPswcOCX3jijL7SJ5pBGUBHd8uEayBy1ygeGGwIDAQABAoIBADINZSx2I1pvzLSE
     Bmd8hG7DM8Ww98iJJISSeKh4YfHFbUqEqO2xf7mYKggUeT8vjUABIb4dHclmGoxA
     Dn1cF6m38rbv8hD982kz9KBaHGkt57RsRZDKliXbSk/XbVcVK5H1BGOnpNSYIe3/
     FFBz7LSvEqJ83Hedpys7qPhkkqg4WsgRZrrQNgkA4WOSm8wSnTHrZnI7VHY/MpYI
     606nKx39O1cjN0tiiXKnasgqKZWDfOO7NvhD+YXPnky2XT+mWoPFmDEx8jrbHt7Q
     DTs7xFpC6TYfQPh7lyhsQDcEYjWZn/ZdEKOhCeo24REbez+tz4s2dL3EyGKbQKkz
     FltVMAECgYEA8IGp5e8zJBhwWq/N7bM5NutUZn9SsEQ039KUTzGUmeE4nnt+0iFf
     t4Uor1/Hzj1PrYqgJl9tHhAXQslYH/l6W7X+u49TJAl5SuESfrH3x5+V95lC5nI4
     SEai7PjmTRZ45jc0tCKnxOgQnCcS6qHgyxWxItr3ps7aMCHrmaBTjCsCgYEA0DrO
     YdRxWCFZOrmwP0xfbPKbuv2sjV6MN+SeDFAl4MV+DYMIF0xgESakLWybisaYytwH
     IRANEDAEuXMUblCJic+a35FC14IlzU3ksZVf83zyleKB15iEgDkI7EoyczumlKiD
     sumBoCBALWzwxNd1tiDm9LyHjnpx2+y640VfxdECgYAPleeDrg+bXDYTumbW65Fe
     nLt4dPHP2GuwwX248BaYLj80Df628VC5nNh5HPTeyZxbO6uLMQ3qL9LCEjgywkEK
     pm2ei/gwUqjYkGNZcIEFH7NhOz5ZnrdE/8bZInwSLM2i5Zr1vXUvznYdGG8iY2Ek
     5//1qUj5N1huXBRffUNMxwKBgELQq8p+ZYQ25y/Nx3z4H6KQ0mGU5lpSXUHODNy8
     lvrhxAnH4r+/FRBLyuB8egh0ozBsm6kDQn3QOqPbBlJDa26Z/AMC1GTccQ7IkLpe
     yPQTQq/Ph4RLfzC5nGBdioSpPlFzJRcykBJ2ZsFstHElBbNUKWecWw7fwUslUe59
     IzcRAoGBAJsNwacNC6VeojCKcp4aaQhH8vEd8F5cff2qGTMjplhqSyl1eqr7IJ3n
     AajZbsS2UJa35UxpSXzeMoUaQB6EG5e//BG5Br+6n1aOHlERJV7t9/Z4re9g2lIk
     msuEm+VNsXpZQ4lspARV8kqWcNzrhGSfgq1BEHWIHBKp93mMigL4
     -----END RSA PRIVATE KEY-----

  Edit the credentials for Windows machines:
  Click on **Credentials** from the top menu (if not there already).
  Select **WINDOWS**.
  - **Username** - Administrator
  - **Secret** - Password
  - **Key** - nutanix/4u

Click **Save** from the top right menu, then click the **Back** green button.

Update the application profile variables:
  1. Edit the Mysql_password variable:
  On the left hand side menu, click on the application overview box and select the Nutanix Profile.
  Locate the Mysql_password from the right hand side menu and type **nutanix/4u** in the **Password** field.
  .. figure:: images/Mysql_password.png

  2. Edit the INSTANCE_PUBLIC_KEY variable by pasting the public key below beginning with ssh-rsa and ending with .com:
  .. code-block:: bash
     ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDDoJlPj+ACPyHGm0f+FyTQPRt+m1H6JstyLtvFJUntDyF2/dqpcQ9QfKKw1QcjzGdSS8B6HrdOOjKZz42j01/YLWFy2YrDLQOHcNJi6XowCQ059C7bHehP5lqNN6bRIzdQnqGZGYi8iKYzUChMVusfsPd5ZZo0rHCAiCAP1yFqrcSmq83QNN1X8FZ1COoMB66vKyD2rEoeKz4lilEeWKyP4RLmkOc1eMYQNdyMOCNFFbKmC1nPJ+Mpxo1HfNR84R7WNl5oEaNQOORN+NaOzu5Bxim2hhJvU37J+504azZ1PCUiHiC0+zBw4JfeOKMvtInmkEZQEd3y4RrIHLXKB4Yb centos@nutanix.com

  Click **Save** from the top right menu.

Set the NIC network in each of the VMs to the **Primary** network.
  Select each of the Services in the blueprint pane.
  Select **VM** in the right hand pane and scroll down to **NETWORK ADAPTERS (NICS) (1)**.
  Select the **Primary** network.
  Repeat for each service.

Edit the VM Name field in each of the VMs to add your initials. Select VM Configuration in the right pane and place your initials in front of the name field similar to the example shown belowm replacing abc with your initials:
abc-MYSQL-@@{calm_array_index}@@-@@{calm_time}@@

.. figure:: images/calm_prefix_vm_name.png


Takeaways
+++++++++

- Microsegmentation, part of Flow, is a decentralized security framework managed from Prism Central.
- Microsegmentation offers additional protection against malicious threats that originate from within the data center and spread laterally, from one machine to another.
- Once Flow is enabled in the cluster, VMs can be easily protected through Security Policies created in the Prism Central UI. These function as labels that can easily be applied to VMs without any additional network setup.
- Calm blueprints can be used to quickly import an application configuration and have the cluster provision the resources needed for the particular application to run automatically.
