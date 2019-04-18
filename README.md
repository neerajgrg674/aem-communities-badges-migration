# communities-badges-migration

Communities Badges migration migrates badges paths from /etc/community/badging/images to new paths (/libs/community/badging/images, /content/community/badging/images).
This migration is required for a customer upgrading to 6.4 or higher version from 6.3 or lower version. If this migration is not done, User's old badges would continue
pointing to old paths(/etc).

Pre-requisite: 
  - Make sure old badges images are present before running migration script.
  - Users should not be assigned any new badges prior migration as it might conflict with old badges during migration.

Steps to migrate :

1. Change the scoring path and badging paths in constant file (com.adobe.cq.social.badges.resource.migrator.internal.BadgingContants).
2. build cq-social-badges-migrator bundle.
3. On any of publisher instance:
	a. - Stop the instance.
	b. - install the cq-social-badges-migrator bundle.
	c. - Add a logger for package "com.adobe.cq.social.badges.resource"  from http://<host>:<port>/system/console/slinglog

4. Create New Badges
    
   - Make a HTTP POST call to http://<host>:<port>/libs/social/badges/badgeResourceCreateServlet with ADMIN credentials.
   - Check the logs for any error in log file created in 3c.
   
5. Validate Badges
    
   - Make a HTTP POST call to http://<host>:<port>/libs/social/badges/badgeResourceValidationServlet with ADMIN credentials.
   - Check the logs for any error in log file created in 3c.
   
6   Delete Old Badge - (If validation is passed for all Users in step 5)
    
   - Make a HTTP POST call to http://<host>:<port>/libs/social/badges/badgeResourceDeleteServlet with ADMIN credentials.
   - Check the logs for any error in log file created in 3c.
   
   
   
   Note-  This script currently handles single badgingrule and scoring rule configured on system. If string array of scoringrules and 
          badgingrules is configured on system, this might not work.
   
