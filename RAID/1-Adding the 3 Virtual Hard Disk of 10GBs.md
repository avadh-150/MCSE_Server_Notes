## Phase 1: Adding the Virtual Hardware

Before adding the drive in Windows, you must first "plug in" the virtual hardware through the VMware settings.

1. **Open VM Settings:** With the virtual machine powered off, click on **Edit virtual machine settings**.

![](https://private-user-images.githubusercontent.com/168718396/531600892-5204e0ae-577f-44a0-9f97-acacadabf6cf.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NzMwNzQ2OTYsIm5iZiI6MTc3MzA3NDM5NiwicGF0aCI6Ii8xNjg3MTgzOTYvNTMxNjAwODkyLTUyMDRlMGFlLTU3N2YtNDRhMC05Zjk3LWFjYWNhZGFiZjZjZi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjYwMzA5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI2MDMwOVQxNjM5NTZaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1iNmZlOGFkYTVmMTU3MWQ3ODA5OTUxMDYxYTVkOTcwMGRhNTdjNTZhMjI3MmIzYjFlMmZiZWY1OWRmN2E0ZjczJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.d3ctF8yJZSaR6fPdGwOA01gRPpWq5i7okJ-fR5tMTao)

2. **Add Hardware:** Click the **Add...** button at the bottom of the Hardware tab.

![](https://private-user-images.githubusercontent.com/168718396/531600969-0991d999-da1d-42f3-9259-382c1ee10500.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NzMwNzQ3MjIsIm5iZiI6MTc3MzA3NDQyMiwicGF0aCI6Ii8xNjg3MTgzOTYvNTMxNjAwOTY5LTA5OTFkOTk5LWRhMWQtNDJmMy05MjU5LTM4MmMxZWUxMDUwMC5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjYwMzA5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI2MDMwOVQxNjQwMjJaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1hZTM5ZDI2YTVhZTUwMTRkMGU4ZjJmZDFjYThjZTA4NWM0MWIxOGZiNGM2OTAxMDczNTRjMTZiMmY1MGM0NzU3JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.2zcEsv56I761p9oOhNPkr5xr4al5cxY8IFR6yLqVYHE)

3. **Select Hard Disk:** Choose **Hard Disk** from the list and click **Next**.
    
4. **Disk Type:** Select the recommended disk type (e.g., **NVMe**) and click **Next**.
    
5. **Create Disk:** Select **Create a new virtual disk** and click **Next**.

![](https://private-user-images.githubusercontent.com/168718396/531601140-a8a29db8-953c-42a2-806a-3465edc9028c.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NzMwNzQ3MjIsIm5iZiI6MTc3MzA3NDQyMiwicGF0aCI6Ii8xNjg3MTgzOTYvNTMxNjAxMTQwLWE4YTI5ZGI4LTk1M2MtNDJhMi04MDZhLTM0NjVlZGM5MDI4Yy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjYwMzA5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI2MDMwOVQxNjQwMjJaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT02MTk3NmQyZmZhMGIwMjFjOGZmMWE1MTNhMGM2NWFhZjBlNTliMTFiNjA2Njk2MThiOGVmODViOGQ2NjUxOGMzJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.8ybRwj5cFon26qvRrr9ogQYS6QrLTiVN755raZlIP2s)

6. **Set Capacity:** * Change the "Maximum disk size (GB)" to **10.0**.
    
    - Select **Store virtual disk as a single file**. Click **Next**.
        
7. **Disk File Name:** Keep the default file name or choose a location, then click **Finish**.
    
8. **Save Changes:** Click **OK** on the Virtual Machine Settings window to confirm.

9. Repeat it for 2 time with space 10 GB...

![](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/RAID/1.png?raw=true)

Once the hardware is added, you must tell Windows how to use it.
