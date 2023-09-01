# Publicly accessible

To make sure that a database is public we have to check the "Publicly accessible" option and the VPC configuration.

The "Publicly accessible" option just needs to be set to "Yes".

![Screenshot 2023-05-19 at 9.24.59.png](./attachments/Screenshot%202023-05-19%20at%209.24.59.png)
To verify the VPC configuration, click on it (VPC security groups).

![Screenshot 2023-05-19 at 9.25.51.png](./attachments/Screenshot%202023-05-19%20at%209.25.51.png)
Once the VPC to be verified has been selected, click on "Inbound rules" and then on "Edit Inbound rules".

![Screenshot 2023-05-19 at 9.26.34.png](./attachments/Screenshot%202023-05-19%20at%209.26.34.png)
We will make sure that we have the configuration with 0.0.0.0.0/0 or we will create it.

Finally, we will use our favorite DB client to [test the connection](/wiki/spaces/SOFT/pages/1185874124).
