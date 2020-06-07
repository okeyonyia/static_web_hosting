
##### BLACK LIVES MATTER
# Static Website Hosting
#### By Okey Onyia -  _onyia.okeyj@gmail.com_
----------

This document describes the steps towards completing 1st udacity project in the cloud developer path.

## AWS Services Used:

-    __IAM__, __S3__, __CloudFront__, __Certificate Manager__, __Route53__, __SNS__, __CloudWatch__

## Final outcome:

To view the final result website, please click or copy link to your web browser www.okeyonyia.com

-   Website is static html, css javascript files. I had to take this opportunity to setup my personal website
-   It accepts http/https protocols. If request protocol is http, Cloud Front distribution will upgrade the request to https. If the request is https, even better :-)

## Breakdown:

1.  **IAM**
    -   Create a new account and applied the `promo code` given to me to get the `50$` credit, already used `12$` :-( 
    -   Configure MFA to secure the root account.
    - Create a second user 
    - Attach admin policy to the user
    - Log in with the new user and continue the rest of the set up with the new user
    
2.  **S3**
    -   Create  `2` `S3` buckets. One for www.okeyonyia.com and the other for okeyonyia.com
    -  Upload the same files into the two _buckets_.
    ![enter image description here](https://udacity-project01.s3.amazonaws.com/image+%287%29.png)
    -   Make the contents _public_ and easily accessible from web browser
    - Configure `Static Web Hosting` to allow the bucket to be used for static web hosting.
    ![enter image description here](https://udacity-project01.s3.amazonaws.com/image+%284%29.png)
    - Added policy to only allow `S3:GetObject` actions on the bucket
    - ![enter image description here](https://udacity-project01.s3.amazonaws.com/image+%283%29.png)
    - Direct `s3`bucket links to confirm its the same website - 
      - http://okeyonyia.com.s3-website-us-east-1.amazonaws.com, http://www.okeyonyia.com.s3-website-us-east-1.amazonaws.com  
 ![enter image description here](https://udacity-project01.s3.amazonaws.com/image+%282%29.png)

3.  **Cloud Front**
	   -  Setup  `2` distributions. One for www.okeyonyia.com the other for okeyonyia.com
    -   Reason I decided to set up 2 distributions is to be able to use them differently in configuring `Route53` `record zone` specifically in `creating record sets` for type `A` record. But we will get to that in `Route53` section
    -   In the `distribution behavior` I accept http and https. But had to configure it in a way that if ingress is on `80`, upgrade to `443`. I did not like the **Not Secure** sign on the browser :-)
    - The upgrade from `http` to `https` protocol required an `SSL` certificate
    ![enter image description here](https://udacity-project01.s3.amazonaws.com/image+%285%29.png)
4. **Certificate Manager**
	- Request `SSL` certificate 
	- Verify my domain by adding type `CNAME` `record set` with value provided in the process to prove ownership of the website 
	- Another option to verify the domain was to setup `SES` to receive email verification but I figured the adding those `CNAME` sets were faster and I didn't want to go too far beyond the scope of the project.
	![enter image description here](https://udacity-project01.s3.amazonaws.com/image+%286%29.png)
5. **Route53**
	- Register a new domain name - __okeyonyia.com__. Why not? I had a __`50$`__ credit.
	- Configure Hosted zone Assigned to the domain
	- Create `Record Sets`and added _ALIAS_ that target the `Cloud Front` Distributions created.
	- I did not attach record sets for security reasons![enter image description here](https://udacity-project01.s3.amazonaws.com/image+%281%29.png)
6. **CloudWatch**
   - I did not forget to set up alarm on `CloudWatch`. I want my __`50$`__ credit to last.
 7. **SNS**
    - Create a `BillingAlarm` `topic` 
    - Add an _email_ `endpoint` providing my email address.
	 
## Conclusion
I find it easier to setup a static web hosting using these simple `AWS` services. Website was also much easier to update by ensuring to deactivate versioning and override the files.

Securing the buckets with `policies` and limiting actions by any `Principle` to just `s3:GetObject` brought me peace at night. 

`AWS Certificates` was more than seamless. I will continue to use the certs.

On the cost side, its been `24` hours since I had the website on and `cloud watch` isn't reporting any spikes in bills yet. Oh, I shared my website with family, friends and now you :-)

##### BLACK LIVES MATTER

