## iCloud3 Version 2.3 Change Log

The following enhancements and changes have been made iCloud3:

* The best way to monitor new releases is to add HACS (Home Assistant Community Store) to your HA system and set up the HACS/iCloud3 link using the instructions in the iCloud3 documentation [here](https://gcobb321.github.io/icloud3/#/chapters/3-hacs). 
* You can also go to the iCloud3 releases page [here](https://github.com/gcobb321/icloud3/releases) to download the latest version and do a manual update.

------

#### iCloud3 now works with Apple ID Verification and supports iCloud 2-factor-authentication

This is significant update to iCloud3. It supports true 2fa verification using the 6-digit Apple ID Verification Code sent from Apple when you log into iCloud.

When iCloud3 starts, you will get the standard Apple Login warning and the 6-digit Apple ID Verification Code notification. YOU WILL USE THAT 6-DIGIT CODE IN THE ID ENTRY SCREEN ON THE HA NOTIFICATIONS AREA. Select the Verification Code entry window like you always have from the HA Notifications area and enter the 6-digit code. This will create the Trusted Device token like other apps and browsers. iCloud3 will then continue starting as it usually does. Go [here](/1-getting-started?id=authenticating-your-icloud-account) for more information on entering the 6-digit authentication code.

-----

#### Other Changes

- **New Configuration Parameter**
  *display_zone_format: name/title/fname/zone, Default: name*

  This parameter indicates how the zone should be displayed in the device_tracker.[DEVICENAME] states field and on the Event Log. The zone is formatted as follows:
  
- name - A reformatted zone name. Examples: 'the_shores' is displayed as 'TheShores'
  
  - title - A reformatted zone name. Example: 'the_shores' is displayed as 'The Shores'
- fname - The zones Friendly Name. Example: 'The Shores Development'
  
  - zone - The actual zone name is displayed. Example: 'the_shores' is displayed as 'the_shores'
  
- **New Configuration Parameter:**

  *2sa_verification: True/False, Default: False*

  This parameter forces the 2-step-authentication procedure used in previous versions of iCloud3 instead of the 2-factor-authentication using the native Apple ID Verification Code released in iCloud3 v2.2.2.

- **Breaking Change - *icloud3_lost_phone* service**

  The *device_tracker.icloud3_lost_phone* service call as changed to *device_tracker.icloud3_find_iphone_alert* to match what the service call actually does and eliminate any confusion with the Apple's lost phone process. This service call uses the iCloud native process when using the Family Sharing tracking method and sends an alert (with sound) when using the Find-my-Friends and iOS App tracking method.

- **Battery Status**

  If the battery state is less than 10%, the polling interval is set to the *stationary_zone_interval* value (default is 30-minutes), regardless of the distance from home. If it is less than 5%, and the distance from Home is less than 1km, it will be set to 15-seconds. This change should help preserve battery life when the phone is in a low power mode.

- **Event Log Actions**

  - Reorganized the list of Actions

  - Added the *Reset iCloud Interface* Action that removes the current iCloud communications sessions and restarts the iCloud interface program (pyicloud_ic3.py) that handles iCloud3 Location requests. It will:

    1. Rename the current cookies and session files in the */config/.storage/icloud* directory to save them.
    2. Create new cookies and session files.
    3. Request iCloud authorization which will send the Apple Id Verification Code notification to the trusted phone with the 6-digit Verification Code
    4. Set up the configuration form in the HA Notifications area for entering the 6-digit verification code.
    5. Restart iCloud3 and reinitialize the iCloud Interface program.

    

Gary Cobb *(aka geekstergary)*

November, 2020

------

#### Special Thanks

* A special thanks goes to Noccolo Zapponi, London for updating *pyicloud.py* to support 2-factor-authentication which has been incorporated into *pyicloud_ic3.py* used by iCloud3.