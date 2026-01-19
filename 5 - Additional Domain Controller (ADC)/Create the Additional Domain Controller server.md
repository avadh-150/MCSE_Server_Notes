   
   
  1. I Create the **PC2 as ADC** 

---

   2. First Change the Name OR Hostname of PC2 
			REPLACE `PC2 with ADC`
				Go to and

	`**search** -> **sysdm.cpl** -> **change**... -> then **HOST_name**`
---

   2. Open Server Manager.

[![ADCpromotion](https://itingredients.com//wp-content/uploads/2015/07/ADCpromotion-81.png)](https://itingredients.com//wp-content/uploads/2015/07/ADCpromotion-81.png)

---

4. On Dashboard of Server Manager click on ‘Add Roles and Features’ to install AD DS role.

[![ADCpromotion](https://itingredients.com//wp-content/uploads/2015/07/ADCpromotion-9-e1437716202179-300x220.png)](https://itingredients.com//wp-content/uploads/2015/07/ADCpromotion-9-e1437716202179.png)

---

5. On “Add Roles and Features Wizard” we’ll verify all the prerequisites like administrator account has a password, IP address configured etc.To continue, click Next.

[![ADCpromotion](https://itingredients.com//wp-content/uploads/2015/07/ADCpromotion-10-300x211.png)](https://itingredients.com//wp-content/uploads/2015/07/ADCpromotion-10.png)

---

6. Select “Role-based or feature-based installation” and click on Next.

[![ADCpromotion](https://itingredients.com//wp-content/uploads/2015/07/ADCpromotion-11-300x214.png)](https://itingredients.com//wp-content/uploads/2015/07/ADCpromotion-11.png)

---
7. In ‘Select destination server’ wizard, in server pool all remotely manageable servers are listed but here only one name is listed there i.e. **DC.iforward.in.** Select the box on which you want to install Active Directory.

[![ADCpromotion](https://itingredients.com//wp-content/uploads/2015/07/ADCpromotion-12-300x214.png)](https://itingredients.com//wp-content/uploads/2015/07/ADCpromotion-12.png)

---
8. Some features are required to install AD DS role. Click on Add Features to install those features that are required for DC promotion.

[![ADCpromotion](https://itingredients.com//wp-content/uploads/2015/07/ADCpromotion-13-287x300.png)](https://itingredients.com//wp-content/uploads/2015/07/ADCpromotion-13.png)

---

9. On “Add Roles and Features Wizard” select **Active Directory Domain Services Role** to install and click next.

[![ADCpromotion](https://itingredients.com//wp-content/uploads/2015/07/ADCpromotion-14-300x213.png)](https://itingredients.com//wp-content/uploads/2015/07/ADCpromotion-14.png)

---

10. In “Select features” windows, we don’t need to select any additional features. As all the required features are already selected.

[![ADCpromotion](https://itingredients.com//wp-content/uploads/2015/07/ADCpromotion-15-300x211.png)](https://itingredients.com//wp-content/uploads/2015/07/ADCpromotion-15.png)

---

11. Additional information can be seen about AD DS. Click next.

[![ADCpromotion](https://itingredients.com//wp-content/uploads/2015/07/ADCpromotion-16-300x211.png)](https://itingredients.com//wp-content/uploads/2015/07/ADCpromotion-16.png)

---

12. In “Confirm Installation selections” windows, we can see all the roles and features that we have selected to install. In case of any changes, click on previous to go back and make the change. Select the option “Restart the destination computer automatically if required”. A popup will confirm if you want to restart the server automatically after it is promoted as an ADC. Restart is required for changes to get affected, click Yes. Click on Install to begin the installation of Active Directory.

[![ADCpromotion](https://itingredients.com//wp-content/uploads/2015/07/ADCpromotion-17-300x213.png)](https://itingredients.com//wp-content/uploads/2015/07/ADCpromotion-17.png)

---

13. Once the AD-DS role is installed, click on the exclamation sign on the top of Server manager and click on “Promote this server to a domain controller”.

[![ADCpromotion](https://itingredients.com//wp-content/uploads/2015/07/ADCpromotion-20-300x258.png)](https://itingredients.com//wp-content/uploads/2015/07/ADCpromotion-20.png)

---

14. To promote this computer as an ADC select the option “Add a domain controller to an existing domain”. Please ensure your domain name is selected and you are logged in as enterprise admin. Click Next.

[![ADCpromotion](https://itingredients.com//wp-content/uploads/2015/07/ADCpromotion-21-300x219.png)](https://itingredients.com//wp-content/uploads/2015/07/ADCpromotion-21.png)

---
15. Select the options “DNS Server” and “Global Catalog (GC). If you want to install DNS on this server and promote this server as a Global Catalog. Type Directory Services Restore Mode password. Please ensure that you remember this password, we’ll use this password while logging to Active Directory Restore Mode.

[![ADCpromotion](https://itingredients.com//wp-content/uploads/2015/07/ADCpromotion-22-300x219.png)](https://itingredients.com//wp-content/uploads/2015/07/ADCpromotion-22.png)

---
16. In the “DNS Options” window, click on next.

[![ADCpromotion](https://itingredients.com//wp-content/uploads/2015/07/ADCpromotion-23-300x219.png)](https://itingredients.com//wp-content/uploads/2015/07/ADCpromotion-23.png)

---
17. In the “Additional Options” window, select the domain controller from which you want all the data to be replicated. In this example, we only have one DC in our environment. If you have multiple DCs then select the one which is either at our site or near to our site.

[![ADCpromotion](https://itingredients.com//wp-content/uploads/2015/07/ADCpromotion-24-300x219.png)](https://itingredients.com//wp-content/uploads/2015/07/ADCpromotion-24.png)

---
18. In the paths window, define the patch of database folder, log file folder and sysvol folder. We’ll go with the default in this example, but you can change it as per your preference.

[![ADCpromotion](https://itingredients.com//wp-content/uploads/2015/07/ADCpromotion-26-300x219.png)](https://itingredients.com//wp-content/uploads/2015/07/ADCpromotion-26.png)

---
19. Review all your selections. Click previous and change if any changes are required else click next.

[![ADCpromotion](https://itingredients.com//wp-content/uploads/2015/07/ADCpromotion-27-300x218.png)](https://itingredients.com//wp-content/uploads/2015/07/ADCpromotion-27.png)

---
20. In “prerequisite check”, it would show all the prerequisites that are missing and need to be fixed. We can ignore the warnings but we can’t ignore the error message. In case of error message, install option will not be visible. Click on Install to begin the installation of ADC.

[![ADCpromotion](https://itingredients.com//wp-content/uploads/2015/07/ADCpromotion-28-300x220.png)](https://itingredients.com//wp-content/uploads/2015/07/ADCpromotion-28.png)

----------------------------------------------------COMPLETED-----------------------------
