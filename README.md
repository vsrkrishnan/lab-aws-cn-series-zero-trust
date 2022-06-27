![](https://lh3.googleusercontent.com/yfauRkorcR5tsFglEdZxcCNB9Q8gvT4mggnkshWrB8q_-cYqvLyIQ3E6ice1-LyU_1RPOSOBQGJV4ioYEMUHmnaA-vR0-QEf6n2DMsuSKShlMMkT3icnW8YPWsmNZqpHNCoQOXPJagUvsjXvUA)

![](https://lh4.googleusercontent.com/WklkdY_mjQ-WBwYKvAXSKjASdEiaovVgOuy133k8FckQasbq6zfUE8IOanAYXWWTk55OFwO2_02oyD7aUGUl27s-3ukZ6bnurY3tdMs7qIehSPukBaWLyZMblNzI6cfsN1fU8klkGLSyCq8n7g)

# Zero Trust AWS CN-Series

## QwikLab Guide

# Overview

A Zero Trust implementation should provide security administrators with the visibility and the ability to secure traffic between the various applications. 

## Hands-On Lab – Palo Alto Networks Product Coverage

- **[CN-Series Virtual Next-Generation Firewalls](https://www.paloaltonetworks.com/network-security/cn-series)**
    - Protect Kubernetes Containers
    - Keep cloud native applications nimble and secure with the industry's first ML-Powered Next-Generation Firewall (NGFW) built for Kubernetes® environments.

- **[Panorama™](https://www.paloaltonetworks.com/network-security/panorama)**
    - Consolidate policy management. Panorama™ network security management simplifies policies across infrastructures and clouds. Seamless integration. Increased oversight.
    - Panorama can be deployed as a virtual appliance on VMware ESXi™ and vCloud<sup>®</sup> Air, Linux KVM, and Microsoft Hyper-V<sup>®</sup>.

# Application Environment Overview

## Launch the lab environment

In this section, we will launch the lab environment. These are the steps that we will accomplish at this time.

- Start the lab on your designated Qwiklab account.
- Login to the AWS Console using the provided credentials and set up  IAM roles
- Subscribe to the Panorama appliance on the AWS Marketplace.
- Deploy lab environment using Terraform
- Deploy the CN-Series firewalls
- Deploy a sample application for the activity 

## Start qwiklabs lab environment and login to AWS

Please follow the link provided below to open the Qwiklab classroom on which the lab is being hosted.

<https://paloaltonetworks.qwiklabs.com/focuses/1494>

1. On the Qwiklab environment, Click on _Start Lab_ Button to start the lab.
    - At this point, Qwiklabs will build an AWS account for you.
    - In order to access the EC2 application instances via SSH in your environment, you will be using keys generated by Qwiklabs. There are two types of keys generated; PEM and PPK keys.

![](https://lh5.googleusercontent.com/Lyh1ZJqYRte_EGk2qoWbIk2H6HQlPB8iOhiLMmztE7Cizc9I2f_UR60Rnc6dZGZNborwjS5uJF2Gq5C_cAay9ME0mSmyKObmnB9haGp9cYyHdlikZN2xD9UK3QvjFWxD0WoVrsaMefiJzlcQkg)

2. If you are on a MAC, you will be using ‘Terminal’ to connect to the devices via SSH. For this, click on the “Download PEM” link. This will download a file named “qwikLABS-L\*\*\*\*\*-\*\*\*\*\*.pem”.
    - Make sure to note the location where the file is downloaded. On a Mac, by default, it will be downloaded to “/Users/&lt;username>/Downloads”

3. If you are using a windows laptop to access this lab, you will need to have a ssh application like PuTTY installed.
    - In this case, click on the “Download PPK” link. This will download a file named “qwikLABS-L\*\*\*\*\*-\*\*\*\*\*.ppk”.

![](https://lh6.googleusercontent.com/xkgZ8yO0Ji3rytcjjzCM629cDkm_vsjB9FbDpwkcmhdG85vI7i3f6KeoiK7uzU8tgcHfPQbFRchDdMKb07LQO0lFCPNwqwrSCMgM4sTnsxrZUGic8GRTWNhBrnjIHsLZ8Cil8U6DN7D5l3soOA)

![](https://lh4.googleusercontent.com/fwrFpuVr6eVhozTtYCOKMGAPOiGV0v6guMB-WL9vY0KnJQpoZDgVE6Lrjgpz18V-sXv2wRRmD1dT8nfpZJeZqFLd7HvGTTF3RgdQqxOGyd4oT-CQM4qV5jjzXmk9H66T1qH3jvwuHGx7qltj4A)

4. To login to the AWS environment, right click on “Open Console’ and “Open link in Incognito window” for Chrome-based browsers. For other browsers, use the appropriate option to open the AWS Console in a new private tab.

![](https://lh4.googleusercontent.com/C2Zb6FWjVU5YTx9i0RK_Njnj2l6hA4Pxwm15Lpu-bDmI8p5dbMaktVElnd7EXCEx9SvKGXtru5JXRUJgEf8QuYhaB4T-sBTe7ooIpvdvvdslXM0XftvxAoNgdQm61e6iGyYscGHcwVuTgOOUiCM)

5. On the AWS Console, copy over the IAM username and password from the previous tab.

![](https://lh6.googleusercontent.com/IHtN1_Qz7CbUhTc-0OXQdQG5IGNOcJbtR3wg8eD2IfJjq55W1K5uRbG4WiHRZAZvE7bJPaoq9TtAZrR-BX6Y9kZ-uGw0CzEN8hR_hLYefLjh6YIfX2l7WEgBVcxCBjq4gGBbdsg5myia4G8CDw)![](https://lh5.googleusercontent.com/-6aCr6AOw9OWs54ccczfFAkHAb-Cvq-PR8UI6ByTtavTPf5jqpwKc7dveKdcJHxomQDT50GpufdcY-6C7o2MGdEskrE3gfrRrGLUBIfkXCR5k3gMXZ3ogc6j7MWIrm6yD7m048SvfWzQeiD14w)

6. Now, click on “Sign In”.

![](https://lh3.googleusercontent.com/P6a_F9N2HumktXzhaQpBE_hKFShZKThHpcKi4FvXc3ZNOs7l9iZyc6HrdUs15pZUqiZmsRalToQylYqhtImHpoEJId50mGhP3x2zYAevlVB7SUnc49jmy7kaZo2QvgsOHm6Ev0wRrdYdZZWgoQ)

Once you are successfully logged in, you will land on the AWS Management Console.

![](https://lh6.googleusercontent.com/3b0XW8901RrdkxXRNaURxFmXj98W6Lp097-LxttiRQyaRe0yCwIEjEzNCwddq_QjJYLzoR0OYPLjcwgqfL4MqZxUz2S4tagF7RtRDcM7xmmOU2qS0D_BVKL8idkzNypsIjTJlZ98HPJ5J_kZxg)
**Figure:** The AWS Management Console

## Set up AWS Account permissions

As mentioned earlier, the Qwiklab user account, by default, does not have the permissions to AWS Marketplace and CloudShell services, which are required for the purpose of this lab. We will now edit the permissions for the Qwiklab user account to provide access to those services.

On the AWS console,

7. If you see a message for ‘new AWS Console’ click on ‘Switch now’
8. On the search bar type ‘iam’.
9. Click on the link to _IAM_. A new IAM dashboard window will open.

![](https://lh6.googleusercontent.com/h5G5FJET_LxslwyLXBKaLD3Q69R89JaeN44Wk8PnWXou9TUzP3yK0DU-NhdwDN-adn9M7FJmVG2VtE2Wa_p9HzBgXj6EJp80u81cmDmhrEdJqW2rOOsQFUA3onGhn-jYBSpY9HgoxdGFLcQi7w)

10. Click on ‘2’ below users.

![](https://lh5.googleusercontent.com/zF21p1uDqd2jseyvF43DLpB8O6RWFTzOBs6mSQhN68lniPSZ2M2ur31MpdSFOy-aBKH0m7IDlKbXRluENfEVLb0eo_eNmTiOHcCZvV8FDx43afpsmAFQwCJuZ1kStQQYLOS17u7uw-fwBZIw3Q)

11. Click on ‘awsstudent’.

![](https://lh3.googleusercontent.com/nqkqv9aFumM7Tl6bT01TVIDPdW2yUl0IbXMbF8kiI17MDvmAB0HWPED44FIus67r8diyul7woqily3QlSQk-ROUphP2QIVnIHBtb_9zKBMeY21VnIU7UvPAUjlY8v8_KiHg2rOZNBtZAfhDjwQ)

12. Expand the default policy by clicking on the small triangle icon against default_policy in the list.

![](https://lh3.googleusercontent.com/7t7v44sdaXuo-tI0vUC-KkrCp_slHBeawefE0tHmZHF4E5yElKxI7QHd_eSyFE-JuDY-zZFlISTDqx6MAfaiqnuUXDkh0SuhZtLVMjD7Fnjoc6PwMQJgBGKsolDaZ8wCWR2smlHKto0BASFLeA)

13. Click on the ‘Edit Policy’ button.

![](https://lh5.googleusercontent.com/3irmJ6sDcTg0J7PTuOz2wvHqsQrcSPpnCNNjrPG5ZJAwGnpG1lJ3AeC8Ej25iCfkS2-8QJYpEgtGD0ft8IGKm_Im-Iu3ue2KmK7OsZwLTO9378ssG_BdiVRc-CAe44l6KckhXUDSKflOe8y4Jg)

14. Click the ‘JSON’ tab.

![](https://lh6.googleusercontent.com/yxOPeSd47272XGme_HDXKn7ai0mwtICseizFAZnJ4tkfFSsK4McEcltsasCBDh4U7aYxItm-0_xcctvf_pWgXo8qFXP98a4n-0MhopdxYJ0M0vHPSC4uPlOrOj3ky65A5E6OHnSKrUZ6dWrlFQ)

15. Scroll down to the Deny policy and remove two lines (**line number 27** and **line number 36**) listed below

```
"aws-marketplace:\*ubscribe",
...
"cloudshell:\*",
```

Make sure to delete the whole line.

![](https://lh3.googleusercontent.com/FspYiFEH8jYRGWFkGVYgs4PXO-F1nprLbaUD4FM_Zm0vGpY8VkvlQ0-eUig-LwoKSMvoXTqV7Ix1uwF9GAimWfVE8du3Dq568LW7vZ6eurApaMtmvFRXKJqBXTXDj2Iok3HUh85t6XMyp9ir1Q)

16. Click on ‘Review policy’ at the bottom of the screen.
17. On the next screen, click on ‘Save changes’.

![](https://lh4.googleusercontent.com/aUOgibI4-rVikTyIACJo0oSV8LzgNcmOK3D_a-Mdsh71AHMSBZAR3gPZPSE7CQDWdDuPVEX4c5LPSVZKYISBBPwi_HA9r8M1Nac9iBXPL7_DvtaUc_LhHDocO8xkpLt_SahnYMjO_QIOg9LXhQ)

18. Account setup is now complete.


## Subscribe to Panorama on the AWS Marketplace

In this section, we will deploy the AWS Cloud resources required for the purpose of this lab using Terraform. 

19. Click on ‘AWS’ on the top left hand corner to navigate to the primary console.
20. Make sure that the region is N.Virginia.

![](https://lh6.googleusercontent.com/m7e8Bp9ujnI3TgHsKlXyrg7s595dH6aFudk3g74cYU49ojPjJ84PZ2XN5cK_umTXAxeHN7Q5gge6eWM0dfxXE7yvU7WcD1PlqVurcoPF4kTptQAwWiY_3mNve7_w4hdID6ptORsdwbAvP11iaQ)

21. Subscribe to Panorama.
    - Click on the link below and the page that opens up, Click on “Continue to Subscribe” and then Click on “Accept Terms”.

<https://aws.amazon.com/marketplace/pp?sku=eclz7j04vu9lf8ont8ta3n17o>

![](https://lh3.googleusercontent.com/Z3M9rCfoIZ0kqjvdiG9jbQ6R-wYFxfvb0UE_5reV51Km1a8YnVFAX-MRdcJ5HPTkU2yBXgtX0CQJEYlLzSVlBR9f5iQDQTNZZ6viCr8LoXzhKSYjD2symBiA8yRMe2wGRRMe--Qdo4oPVRsOdQ)

![](https://lh3.googleusercontent.com/ZGRKc-avkU2M5QaMA4fPa3rIMFvvXGc-LQhOqeIeDOrSvZs_EGi4jz5l2zZOWTLBSO2wrXHdoDabB7Kkka5UXj3vkToa2sb488O6u2gMvw_IZSYcV5UtYflZQ1v2vij2ObBEhzWu6uf2M5SRdQ)

22. Wait till Effective date changes from ‘Pending’ to today’s date. This will take a few minutes.

![](https://lh6.googleusercontent.com/g6G4A0Gai3-59OvOagie6pjfMhPWTSohZnzyWiEq2WUzVk0h1H1Gkz-pEnBhHCNDehcGNaUGKBzSJVFwwh0Ub5mOXNrm-Npws5PmKraFFS1x_Mpim3wHUPJ0SbmGv1idb3uF4fW4R_PWlBPp-g)

## Deploy the Lab resources using Terraform

23. From the AWS management Console, launch CloudShell using the icon on the top right side of the console.

![](https://lh3.googleusercontent.com/Mvsc0SsCrQIFdcut0lKrKNmtRcSmfhGnea5ZDeRcVpi03FkR9Yd7tnGTQpLOO2kYf-C1E3ztUSHYzsvywTlINUmSYFD3wxRlKmMATrk2cUn6kLTNBIG-Wf9ml9hkFCFpMOd6Ve-ydFt-06BtgQ)

If you do not see the icon as shown in the image above, please check the region and ensure that you are in the _N. Virginia_ region.

24. Close out the welcome pop up.

![](https://lh3.googleusercontent.com/q6XVOI930ynOU7qZ05aaQubOYF_rlGehIiXvMP6FGdzm-7mMTguw2kfKNOoUOz-8kgQiCVZB5Oh8GYgd-_IgE238OwHEHlz9GifNoKzN9X1SCYkek9LJ29wFhI8ckC3LZKNLq-qVJw6_jnYvCw)

It takes around a minute for cloudshell to launch and to get the prompt as shown in the example below.

25. After the cloudshell is launched, we will start by cloning the following github repository:

```
git clone https://github.com/PaloAltoNetworks/lab-aws-cn-series-zero-trust.git
```

![](https://lh5.googleusercontent.com/p6GGG8Y5xKwZzz-QCqWC2heq0HJzDO5fw1aGSgWHmGR9yW4SKFYQ1cGe4-LJUvRaG_Qx6r9QTjXh6VBLQanDrqOfiJmUgKiLTm_G6Mse_0DsKRAM5olyIZwPd0_PlnIbtaNSOlnX_5-8qkUjIA)
**Figure:** Example of cloning the GitHub repository

26. Change current directory to git repositories’ root directory:

```
cd lab-aws-cn-series-zero-trust
```

27. Run the setup script:

```
./setup.sh
```

It will take sometime (**~10 mins**) to deploy all the lab components. Status will be updated on the cloudshell console as deployment progresses. At the end of deployment, you should see the message “Completed successfully!”

![](https://lh4.googleusercontent.com/5pn1Xs_pyrkuEHwC9d-FiY4t_Fy190qp4MievBYVVvJsAN2SCHFZXrgb56yHPPSzw2BFoMKNbdJ74fiVOCOJuFiF74aMrif8mP9vTgCoSzJoFu0umD36Q9xFDQunuMXUKHfsTYlqktqUBST49Q)
**Figure:** Completion message of the Lab Setup script

28. Make a note of the “**eks_cluster_endpoint**” value as shown in the figure above. This will be used for configuring the Kubernetes Plugin on Panorama at a later step.
29. Review the deployed lab environment with the topology diagram shown below.

![](https://lh5.googleusercontent.com/eN1DkPygZKYYKVoJCwI2PKoSqVCwX4DLmv4-8X-zxcokyOvCeFUPmnkL8bD3E4-g4kTmV8yzmCRRoCf0RvHkRKbsQzOWIZQeX-2gpXj3YhoSMxoxIHezsgxHYKsp8yy9CnGYM3Jq2KPKVpqLSZE)
**Figure**: The network topology deployed for the CN-Series lab

30. On the AWS Console, on the search bar at the top, type EKS and select _Clusters_ from the listed results. For ease of use, open the same on a New Tab, so that we can continue to use CloudShell on the existing tab.

![](https://lh3.googleusercontent.com/93YIuU8v9fvpz2Q-7W5-j0SWtpa0mCVnJPk5ne4Q0mOftkFHODj1-Ea-o25cwJbbQ7CAvkUsjLbucMyEivR4fL4boHQAYpHHtiRouBw1TSYtEycquJ7h0Wfe9fXu7QmaVuPK-lofJ5cRuSuNIw)

31. Review the EKS Cluster that was created.

![](https://lh4.googleusercontent.com/bzp3rnpTwMFSoi39Gll6U_lPscUfKVvnfcwMNRY_U4hjEKVwTHC3JqDpHimjf1dxcGvDw7KohOZlHnrTa3YLjWpT2eDnV7pHUBjy1guF4xrYMmAR9Nz7KB0S5CLU0qIYFpO4gIg3aUxYXbk73w)

## Deploy CN-Series firewalls and the Application

Before deploying the CN-Series firewalls, we need to configure the public IP address on Panorama.

32. On the CloudShell tab, run the following commands. Note the Panorama public IP address.

```
cd ~/lab-aws-cn-series-zero-trust/terraform/panorama
```

```
terraform output
```

![](https://lh6.googleusercontent.com/I-sGEqF9QM5ugsLA2sF8s9wFz0BpOlmy8j5xpEn8GUxc2YHl4_46EoUZH5QdLyacZAPEgxQFC3vBTVucNe1DjIgl4w5IXI9E2g66PP66u30GS3BEqcTOlw3IQtgshHJj3zUAOxyXLbS8WvwJog)

33. Open a New Tab on the browser and open the Panorama console using the IP address noted in the previous step. Make sure to add “https&#x3A;//” before the IP address.

![](https://lh6.googleusercontent.com/ghlFO6Y9nKslfqWt9EK_zIk2TQkS2kZhPhKQsM23AYzoFAsiaCcTpPgveeLS-x-CpsAXeUwPJygLwh-M7R6dQwnN0O7xg8aS-Sj72Iz5gwrsHDis7le6hqDMAxj_WCJ2cwleaQ9Gj9RIYDecMg)

34. Log in to Panorama management console:

|              |            |
| ------------ | ---------- |
| **Username** | paloalto   |
| **Password** | Paloalto@1 |

**![](https://lh4.googleusercontent.com/T2Ogda1qIu8YcQJilleqEXfJR__0z8JPcyi9YfJzyi4z1bx6UI42TENnU7UPpbYHfpYtIyT4ypRDP2e-uzPzb4P9ObQxDGfiCAJCEbdCLhub9R0s-1gQ0zjQ-WqWc19Op5D5j_aPyT6fIUCIkg)**

35. Once you have logged in, navigate to Panorama > Setup > Management, as shown in the figure below.

![](https://lh3.googleusercontent.com/KEse9NUtf_t0TJCiWsG2f5-cgVFGjBM8W0X1aw3jhGkjRZTUHwqr2cFXkeXfQTv6aruv1OLEorhjSdTcmKVBD6M1a_X0TDUCOq_mLHH3Vbeo1g7GXwXAKHqk0EpO7nbnWbsSOvwn1nMQ-PmCfg)

36. On the Management popup, enter the public IP address of Panorama as noted before and Click OK.

![](https://lh3.googleusercontent.com/PuBJPBh33zZxdnpoy0K2qJqAIZABtSwkWpqc5QhuU9skwhX5TrjQDJLJGMmIrY9gW5gGg99vhkFgBCK3KbXPQS6wcN-RN02rEPeobFkojTJD9lEdRjLpb8o5AEVh_JiafoYCUgwOCJX7WC-oVA)

37. On the top-right side of the page, locate and click on the “Commit” dropdown list and select Commit to Panorama.

![](https://lh6.googleusercontent.com/67OZQWOjmelEXB8AVPaPrO98TGdpETHI0y4-8SqmFGJI08KgT4PspfGZgZ-VX_wlQUxFggactTfdb18_tC1DbjL_HV-6WcH0O998A5KiBDbfgRoKh3-88kwqAqfAE2B12EN5vvibdl_mRFXdEw)

38. Navigate back to the CloudShell tab and run the below commands. These commands are to deploy the CN-Series firewalls.

```
cd ~/lab-aws-cn-series-zero-trust/terraform/cnseries/cn-series
```

```
./install-cn.sh
```

![](https://lh3.googleusercontent.com/61Oyuh4K_CEXcIcvG3h5Ouyj_0ok3ePUpSyyM4oB3T7SEO0A_R1uL2XvAUv4DeYSG-KgF1N1P7v2Sb1yIx5jbThvEeOcpnGZkcoeFUpym-jYGZezJcmKSVjxHx7M82ShW1Om_1dDgy9zr0vIMA)

39. Now, deploy the sample application by running the below commands.

```
cd ~/lab-aws-cn-series-zero-trust/terraform/cnseries
```

```
kubectl apply -f ./sample-app/guestbook.yml
```

The deployment of the pods for both the CN-Series and the Sample Application will take **around 10 mins** to complete. During this time, the deployed CN-Series firewalls will attach themselves to the Panorama as well.

We can review the status of the pods by running the below commands.

For CN-Series,

```
kubectl get pods -n kube-system
```

![](https://lh5.googleusercontent.com/XA4DIa_PfpLvwBqLhctkOgpn04MDWizIamy96wCfcChkIc7pmzT0M9AO9TiDIR4re_bJFtWGtn-tYyVEqZ7xxJrmA8x10rVKUjWdmDoNmQBb6AvMcRv7RR4sHuoC7VCwiwXvlu-HaqoJt9oy4A)

For the sample application,

```
kubectl get pods -n sample-app
```

![](https://lh4.googleusercontent.com/Jwr4kQBFnXi84CCbOOLTbNkaCDHogOfudxNzUTMfQzfKm8kYB4gVFsJSM52eVxZp_uKzTQe3pUdTgeiikSmSyCyg6tZNAU8_tOetUC8Zph0sPuln7hjakoPvCW9YQSl9lCkdnCJG4pfYN6MiRw)

40. As seen on the images above, under the READY column, all pods should be **1/1**, and under the STATUS column, all pods should be **Running**. This can take from 5-10 mins.
41. Once all the pods are up and running, navigate to the tab with the Panorama console and on the console, navigate to Panorama > Managed Devices > Summary. Note that the CN-Series firewalls were added through bootstrapping.

![](https://lh5.googleusercontent.com/LsM4-vAARHXoO_s22AyEU-0ROnZcQiQvM6X7AZCNYCemcvbJSlQzA4wKD3Kxqtlftj6L8cxiuuNCw7mKvcD1PLaQkTRj05BJImrlznKCbptQcyO5GmV4ga60-U5WqQRrm-TV7jBhAEtOyNqXyw)

## Configure the Kubernetes plugin

42. On the CloudShell tab, run the below commands.

```
MY_TOKEN=`kubectl get serviceaccounts pan-plugin-user -n kube-system -o jsonpath='{.secrets[0].name}'`
```

```
kubectl get secret $MY_TOKEN -n kube-system -o json > ~/pan-plugin-user.json
```

This will create a credentials file to be used while adding the Kubernetes cluster in Panorama.

43. Download the file by locating and clicking on the “Actions” dropdown list on the top-right side of the console.

![](https://lh5.googleusercontent.com/J5-FZsgxV4Z0CcKn45ZfeQrv0Amy9mFa84CFomx7P14LnQcYANz5hrtZdcPR5V2ar_ycnkXGZKLcO-pFx8BArnH9PSs6-mbw-PQErEXvMiASRvud9G484pxQIcT9l6N9emqDqOKiRqsoXjnmIw)

44. In the Download File popup, enter the following path in the text field and click on Download. This will download the given file into the Downloads folder of your system.

```
/home/cloudshell-user/pan-plugin-user.json
```

45. On the Panorama console, navigate to Panorama > Kubernetes > Setup > Cluster and click Add.

![](https://lh4.googleusercontent.com/EaoMdSMHi9F3ejyOpibCDSCax3BrRtRVf6JH1UPNQ_UiZClxgi8bcMiikppNDOL-hMycHcVqoLIWBtQP4zxMEFG8kiHNbjav6f65FJrwC8hb7UXfeokVgbzFw9ejUylQbsiSuizRNYbd-6EgvQ)

46. Enter the fields as given below.
    - **Name** – k8s_cluster
    - **API Server Address** – &lt;eks_cluster_endpoint> value noted post the terraform deployment.
    - **Type** – EKS
    - **Credentials** – Click on Credentials. Browse to the Downloads folder that contains the pan-plugin-user.json file that was downloaded in the previous step.
    - **Label Filter** – “Select All Labels”.
    - Click on **Validate,** to ensure that things are in order.
    - Click on **OK**.

![](https://lh4.googleusercontent.com/lEgxlm8dmSPU49whRbaoWe0LGQmdqNks-GYHAddwrB8J__0xgHCpRt6Z1LtZxfE-0LxkyXFo3rLGB2FQ4kBSTdn6B1vSuBKgVgLGjwNf21-dkgIeOpQ4D0_qahG3KKbFtw5T3XcZmCIsqPYPQQ)

47. Configure ‘Monitoring’ by selecting the **Notify Group **tab, click **Add** to add Notify Group.  Setting up a Notify Group will allow you to segment which Device Group receives notification for changes to a given cluster.  This allows for very granular rules.
    - **Name**: k8s-notify-group
    - **Enable sharing internal tags with Device Groups**: Check
    - **Select Device Group**: cnseries
    - Click **OK**.

![](https://lh6.googleusercontent.com/AjrlgrugqGkDMN4CggC3CuW-2bhyko0nZK5Gb4kTprbN9HbLOwvV9v7scFsGwkit8YQeJNtsN-ynqQIeZwx4JrTVaU93-oE0O-TZTFTow00sRG-nrzUVKHV6eHKx3jq8OEL4lYzjO0hJvnDtLQ)

![](https://lh3.googleusercontent.com/Uaelp_Jf3bLYM4i0kGjeXdfStgzMriU59n5kZbKhnIL5fl_mK6DeKxLZkGhELPZepUzDPvzrzMWLP8U8eFxUNIKhqogNL5-oJeY3v-VqVtAWLY13q8zCJcvfM2mJAqrmSOHw02TmFQjFBTqKzQ)

48.   Now configure the Monitoring Definition and specify the cluster you created in the previous step. Navigate to Kubernetes > Monitoring Definition > Add. Fill out the Monitoring Definition form:
    - **Name**: k8s-monitoring-definition
    - **Description**: k8s-monitoring-definition
    - **Cluster**: k8s-cluster
    - **Notify Group**: k8s-notify-group
    - **Enable**: Check
    - Click **OK**.

![](https://lh6.googleusercontent.com/B-fN-9EZ7gFiysMXPE2rwoDgb4TLsaXTnsi_aQQU5LzQlNLLsVJwhnSCkxzZ1okdHKpeCrpLJklP3OaKwjdlFBHI4df5dk5d6VDOf3J7QnhdGts7Oq63Y-xRgui2WOzqyLo5I1HPpvA_-LDqdQ)

49. Now that you have created the Monitoring Definition, you can see that the status is Initializing.

![](https://lh6.googleusercontent.com/8bGzLhnMXlL9jIBrJ5cczB0gFPREq0CBDguQyTFnQRpvvDd1NCySWF8ReMfE_A6tYN6UmXcPnUyfn7GSGHgYRr3nLv2jEIx4UCzgYfRj9uIXfTvl0jKAnDGEvwHFAjongeapLegL_FHAsdgU6wk)

50.   You need to Commit and Push the configuration. In the upper right corner select the Commit Icon then choose Commit and Push. 

![](https://lh5.googleusercontent.com/1BrSP8vrTDplycPkJoJFlvuaSWFw1OGZkmzZMzRW_hRkUbdjmZRLnE3jZpFBKBmH7WgiWNzk4wnGVdAii9zRl7PT5iIEJMHhLn98fMYaVR3epMLhbBo8K45jVK2ax0Gc4G5G5Xd_c6vTQUp75Q)

51. In the “Commit and Push” popup, Click on **Edit Selections**.

![](https://lh4.googleusercontent.com/tR6QRAkS-dZ0SgKpRVZ6Td94zZy_-9wzhJmNNV9YdjnumElokpa9XjWthXyW5VVVUCC_FeKnbPAJ4_BEyvhno5mZ8PEo8xfT8okVKA1YiY0pSs_2eIT4ek6jMNFeGZumCZrQOee87WGqzxzQBpA)

52. On the **Device Groups** tab on the popup, check the checkbox against the _cnseries_ device group.

![](https://lh5.googleusercontent.com/HZxA3fdGfQDxYOrjUpUzBzyeAjd3KXmCh6xtx8BlRJEPgpVXT2eg-iIM8nsZqU6s6nYw-Pf61h5bZqpktlo9kdVo_cOXbpXOzm9htSVG9C6Xxmtt98i4bUMvhMVr6Dt71JWsn4IuQMgiONRmmiE)

53. Navigate to the **Collector Groups** tab in the same popup and check the checkbox against _panorama_.
54. Click **OK**.

![](https://lh6.googleusercontent.com/cbuPtGe6Dq5iFYp-NOrVAVG5_kJSLvgWaPKoBPqh2B0csS41DbgcoG_VZ4SCYghWSWRyyQm4KUjPdCHTbQcRmx7DWh8zNLDEc-ug4VYG0edbXKRRUx4Ouoduk2HvNXMV0hf7Z_fOf5nKkyUeUXc)

55. Check **Tasks** to confirm all jobs are completed.

![](https://lh6.googleusercontent.com/YvopcvXG2RuNf4rMvFKg5UAHBOhMrCdPWFTKFciClXUyGLxaEBySge87j4khprp-sNL8ANEk_0iahB_ftvcMvHQviCXQCgthoY35lIaCDKLJUqFgtWLfgblu2ML6VYTci2Pi8vLiH8fvMbuLTA)

56. Once the commit is completed, check the status of the newly create Monitoring Definition, _k8s-monitoring-definition_. The Status should say ‘Polling Connected’
57. Click on Dashboard

![](https://lh6.googleusercontent.com/frsN1APFmUlZXQgz9hH7ujX9KXT-S2KcrtjdNnfIZeilY6K8o124dWPOTGO7hxNL8wEi0QQ7pU1TikaOSKgdH8LBMBkCipGeoYfZBZ5B9ZKptL3UH8d6aEPs1lWqHR8rNBFa_qzVDkTN7nUYOQ)

58. You can now see that the Panorama Kubernetes plugin has connected with your kubernetes environment and synchronized the kubernetes tags.

![](https://lh4.googleusercontent.com/aDQmasuzUdlZc8orD0JQhG22CvsTDRFvhuppyzqKuAy_SrZTBNw9cCLkFX8VDUe2NK1_L8OdpJiv08xP0dGdg301qE6DzzlNpVsSZUOXGcncBrGar65ZWMNFW0oMBcvqGTomJqtfD_B1X5dEtA)

# Activity 1: Protect Against Log4j Attack

To secure your containerized application you need to be able to visualize and control the traffic between your pods. Plato Alto CN series firewall allows you to granularly control this traffic.

In step 39 of the previous activity we deployed a ‘Guestbook’ application.The ‘Guestbook’ application a 2-tier simple redis application with a frontend and backend tier. The backend tier will consist of a **_redis-master_** and **_redis-slave_** for db redundancy. Even though there are two tiers in the application, only one (the frontend service) is exposed to the outside world via a load balancer. 

First we would see how having a CN series container Firewall inside your K8s environment gives you visibility to your inter-pod traffic. Then you will use the granular controls using kubernetes tags to control that traffic.

Add diagram


## Activity 1a - Gain Visibility on inter-pod traffic

59. On the Panorama tab on your browser, navigate to ‘Policies’ and select the _cnseries_ **Device Group**.

![](https://lh5.googleusercontent.com/WzYVPpqcfwUvfvIJiqWVA3nQSbUWlWDMGuqz_xahiMqgor9U-AS6CJV95U9hTwdT2Y0vzJYkFHNThdYZY3gy3d3fyuu2lldUGLVzVnTaYWbQRGgOHWVD_llv0fFff6vcNz8a2aQ_U7xntIrUow)

60. Review the policies. There is an allow-all policy that will allow access to all traffic.
61. Access the web frontend of the two tier application. On the cloudshell window execute the command below.

```
kubectl get services -n sample-app
```

![](https://lh5.googleusercontent.com/ou2h4yyP3-OlNupZKmUuj2Noda6R1FWIAkfHMERc4mPDp4MMVYYFOr4M2KHCrL-us3Z-TOCEefxlWIbW2SVS3B2Gtfho4VrW-kkW62SDXdyv_42V-BvmQMnqorPxdIU66K5Cszj5bj7b7drayw)

62. Copy the URl to a new browser tab and enter.

![](https://lh3.googleusercontent.com/ihCrQoMKv4ItrgMYcVtjItG9ar1RBfA6pXKFAL_03LOA6tvGj_0XjCMAKxyk4ZMSWjdCUyp9cjQV1ID7BxGZQ6BSL7LqADeVXlRFICepYZA-HToSADvXdnZXAeX7MGVTLrLcOqQ-HeVjjyOY8w)

63. Enter ‘Hello World’ on the ‘Messages’ tab  and Click Submit

![](https://lh3.googleusercontent.com/oBKpHI8par_tHnqayGeYvS0Ht5jwAWJzDNl2h0zaK_dtTyzEvKguQRCv1OHr7oHbzBxv3W2Bw4wR5dcKrZ0DwfnRaZsbwpYSF5vj-r5jgQkbjP5PxfvdeBCbdPMCiA5r08otoAoXo6wR5PeDPA)

64. Guestbook app saves you message in the back end database and prints it back on the webpage.

![](https://lh6.googleusercontent.com/0ztC7Xm9gCSpuQhcq70iT2FuUbDgvDUBgTxVCKm0njHiEGCrjyFrSkYKQHIc9aG2WiQLpQS02H0rIkUIOzflpAfhSJP-kDkkOCBlRkRuzX2wU2Mr9isUFa6afYI1lJxQlHG2yFzpjsasx-45sQ)

65. Navigate back to Panorama and select the **Monitor** tab. Under traffic log you can now gain visibility into the communication between the Web Frontend pod and the Backend Database. Note that the CN-Series firewall identifies the Layer 7 application as the ‘Redis’ database application.

![](https://lh6.googleusercontent.com/UN3evzIWIs9JKn5gJlmB6qgyfTpVn-uxFans9F_HooPdFiUBvMveMnpj57KrQjDRTepBROPTbFV861CyuchLfbETKGz0KwNsDCxbY66PVm4Tie0UihISLn6HlLuHN7udW4JiLj1Dxl0fOzkjPw)


## Activity 1b- Granular control of Inter-pod Traffic

In this section we will create granular policies on K8s tags and use the policies on CNseries container FW to control interpod traffic

66. Navigate to ‘Objects’ tab on Panorama and locate ‘Address Groups’ on the vertical bar and click on Add button at the bottom of the screen

![](https://lh4.googleusercontent.com/yBzO7iFrIRr6eFwcMRuB07YreIMXwu8WjpjCl2QgAg1gzGMDuO4eMOH51WqYjotuj33BY20ghaII7agl_gX9ZGGohlsfBnzyBaNL1-2i5ouLhyiVHwjj4wDArJJ_yLoVSVip4TUpnnL4M-4qHw)

67. Name the object ‘Frontend’ and select Type as ‘Dynamic’

![](https://lh4.googleusercontent.com/u8B5jWFbL_06sSDupJE2JTjfbAyLiT-9TxK1RgTpQSsBBYCsZ7g4GfFzj62oo1kObvgmqAxiHO8VDc4ulTm5b9mp-cSHdHtfr5MP-fWpDpTfGKYT8y3-z0oQGhzL8kEnXSaO4y4xKGaZeoDw2g)

68. Click on the **Add Match Criteria** button. This brings up a window that lists all the K8S tags learned from the K8S environment.

![](https://lh3.googleusercontent.com/rujIm2HHwP6e2KwCntyIfgf4_VulVC7ldtimivfl4AUGVL1lV4JdgYSAis1QQL2_4p8dxrkdg1qSojIvAvhbKMdfXcl2zPXxtihxk0j23Zh2CZJia1abV5GqeSbl9YPaFIFhr9d9r9Wi7Yyh6A)

69. Now we will  define the match criteria to match all tags that have the frontend string. Select “**OR**”. Type in **frontend** in the filter and click on the → button.

![](https://lh3.googleusercontent.com/Xd66OwJPGuKcXrp6AQIqEj_MDX9N3Vz4cg3q_ElamjhGY1A0WebyncfwmGrG9dlLTvro2hkn8blHr0goIlSx6O9-P-zQPlpTZiO04qBvrGerdtVekRPaUBA69kzFHpJBR16LQgLSwlluOCh8YQ)

70. Click on the + button against each of the tags to add them to match criteria.
71. Click on **OK** to create the DAG.

![](https://lh6.googleusercontent.com/3n9_nJ3KAkel-vq5ZNmHyGPKeQORG2GJO5tyjTXjwORcygpcbtN4ggOYWxb8cvSpSUblg54k8QstKCTl5ioIW51WLAAiJpGG_ZfZgVl38GWEekEboUjrmk4BzYFGFYxyizyKLKMcVfwQi1NyVQ)

72. Now that we have created a ‘Dynamic Address Group’ for the web Frontend, let's create a second one for the Backend Database. Click on **Add** button

![](https://lh5.googleusercontent.com/yC4NMJE-luPpQaTNab5Qz03312lkGqQboyYBY7J1BprY5Vz1Twl9wd6TqP6bCTJmpF_IapsqL6p1Hn-dWpnbdwNe5UG83_X5V0-gMZIFMWXz-FJnudPZsZquUZyedGys0VWHajapxDwdW54rpg)

73. Name the object ‘Backend’. Click on **Add Match criteria**. Select **OR**. Type in “**redis**” on the filter and click →.

![](https://lh6.googleusercontent.com/sqGfvZ9f30lITDvyNZcFaYp0ZpYCwon5MbmIPuQ6WGXytB3u6jJQgVFZ1JxSBYr5YbLwgXsYeOuQcL2B-C7UDLO5sQc8a0ceLRo-tSLQbDCrs6IDLdvrbFd1Y_7L0ZPaEZMFA62A5FVbYZk4dQ)

74. Select all the tags and click on **OK**.

![](https://lh4.googleusercontent.com/dUGPrU_D4lKJwD4wDq12qpxTF-2T_4uxPwA0gglyLjxt7UVAxCtvAwi_KwYhULUzHm8Q9DiaMiCQlacMWWlDmvv9TYAlPDvufSa7MgxpUl_LeasIi088FyMAeKOP2nbsKVqJHmvwrkY0XiWGgg)

75. Navigate to the **Policies **tab. We will now use the DAGs to define policy to control traffic from Frontend and backend Pods. Select the first rule by clicking on ‘1’. Click on the **Enable** button to enable the policy.

![](https://lh3.googleusercontent.com/NhcgXUrkBQRheN-ZdGwO5_cYz4ormGSXJYqrio1BlNPxltFZaZELByf1RZ2TOeJAU_MXAnllfy29IGKmoiQ8o4TZPtjV9ktsXl407xi3jLzRIbs8KzBF35ShbffVUF0LKsytp6SAAjQoJ0Znww)

76. Click on the policy name to edit the policy

![](https://lh5.googleusercontent.com/foyjYh8CVdggXjHk8hjXRdZ61o7sjzrLmMS7R6uNTP5LRsHu8VKIvfT2my6eiHwSk_f1JyV7F6DapEouusBUT152zgGpURb_et7YGOeDe_NrZxbd3nYUDkNjgAraYBArchwtLCbwfgFi8ryDpA)

77. Navigate to the Source tab. On Source address click on ‘+’ and select ‘Frontend’ from the object drop down.

![](https://lh6.googleusercontent.com/Tjcbv4twP9NG7flbWKMPMEOxmAjopWYssZ4xZ8B9UigAyD8EP_E-dvGkHwsKaHCsc7d_j_nfF-FkpycALJlh-PgO0xDrdStDVuzV3edw8KzPwxmkgsmpN4Bb6mGmq-UTQFL9GkTALEYzd-kq_Q)

78. Navigate to the Destination tab and follow the same method to select ‘Backend’ as destination.

![](https://lh4.googleusercontent.com/DQgjnh8T33AS7cT0tjhn4huc5ZKAnKm85_EWKKt_rd2-BbQFL7mnV7nIRwXYfKuMaKfrRxku8XhJwjVd859sIX-77PpmUuqLmDyijontBTUZpb3vPZddvntHm25U2NpMjnjqzNaiKniGCxq66w)

79. Navigate to the Application tab. Click on the ‘+’ button, on the search bar type in ‘redis’ and select the application ‘_redis_’ from the list.

![](https://lh4.googleusercontent.com/693DBWpLrBZuXkhKzDEeJNV03BYFKEzT-_w8tei3d4DGa8MsPD1DDTY-JqtCN-TF_bHzhet1SplsN1y-8ce8KjMWa3Y2KMDQdtoz7sKEnRTfDgrU2A9jNC5X_srb7wvxjtHdg6_Kacg9zn340Q)

80. Navigate to the ‘Action’ tab. Ensure that the Action is ‘Deny’. Click on **OK** to save the policy.

![](https://lh4.googleusercontent.com/iRvM9xlyJdg12CIP8H637vyCLiA7RcFvxW6fiiOpdgH3HlDuf_sWUfyMZniSyRxodSo0jiAseRnr1FlBrI82TACsN_0FgUJIU-KFlLUtBjKQH99PPROlSmQavHu7QHTjvlf6on4OTZK2wg9ONA)

81. Commit and Push

![](https://lh4.googleusercontent.com/Bb-RLLUrohEyyMbGx8do12wLVlfnqlJXlOt-2icDKdN2Lxasp0ngGsVEa8N0SKcm67DmqafRj4LnkpVNY7SCD6qOelNA9CUzchZMbiw6LVXzHl50DRdRyktSvztwWqqw6L7DdK1ZgJcDocIkHg)

82. Ensure _cnseries_ is in the push scope and click on ‘Commit and Push’.![](https://lh5.googleusercontent.com/eqMM7GlLnDSYHGA-GuawO15apT7yAeIppdXolz2KdOiX211qcZEf--BpSUlEo2SZE7Q2UwwKkaFJ1w99GA-2IAcWJCdhNL3jdaTqeyxZ-hs9zXNfFHF0LRCY1dJIXUY1vGd7ISDTjrNHw1O-GQ)
83. Wait for all tasks to complete.
84. Navigate to the tab where the frontend web page for the guestbook app is open. Refresh the page.
85. Type in ‘Hello World Again’ on the message tab and click submit.

![](https://lh4.googleusercontent.com/g18okAUXDCJ-iBYnZGjliSt0m_iVhw5vJsZZFsuZ4925dNFlcYhLhigpogJ7YX1m7RFvnGDmo2eN-aDQketQH2PoQn7PNO4c7q4IUmUFB8prBilSkWun5IBOdix8S2DFfvMi9d_alUFFGlXNgg)

86. You will see that this time the application will not echo back the message;
87. Open the Panorama tab on the Browser and navigate to the Monitor tab and visualize the traffic log corresponding to the firewall policy now blocking the redis application between Frontend pod and the Backend pod of your two tier container application.

![](https://lh6.googleusercontent.com/Yqj5ZiQmxPYqi_l3AZKWPZsbUbVxVjkUqYwEoeU0dPzn_DEgxhQXm6TEce7RQ9aSlQKyf_AX_Xh18aYUZy4RJxwUe9RMuKJgoHTqSBIyOPBTNZLNaCE_uIwybp68642O4Dh1VMU1TRJH6pM5yg)


## Conclusion

Shubam!