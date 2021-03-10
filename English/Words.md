# Words

Database design is a fascinating, deep topic that is both an art and a science. As the number of tables grow in a project over time it is almost inevitable that a refactoring will need to occur to address issues around inefficiency, bloat, and outright errors.

In most cases, decisions are not based on available options but by the architecture of the legacy system, we are sworn to maintain. If such systems are to be ignored, or someone with enough courage and deep pockets would be willing to modernize them, today’s reality would be dominated by containers and microservices. In such a situation, the choices we made yesterday are different from choices we could make today.

Which functions should go into which modules? How does data flow through the project? What features and functions can be grouped together and isolated? By answering questions like these you can begin to plan, in a broad sense, what your finished product will look like.

## How to write change plan

Use this tool to create a tailored upgrade plan. We'll recommend a version, analyze your instance, then tell you what steps to take. If you manage a large or complex instance, you could also consider moving to an Long Term Support release.

1. Complete pre-upgrade checks  
    All pre-upgrade checks have passed... Nice!

2. Choose your upgrade method  
    You can upgrade Confluence manually, or by running the installer. Not sure which one to choose? Learn more in our upgrade guide.

3. Upgrade Confluence in a test environment
    We recommend upgrading Confluence in a staging environment before upgrading your production instance. Here's how:  
    1. Create a staging environment. Learn more
    2. Check app compatibility with the Confluence update check.
    3. Back up your data, including your database, installation directory, and home directory.
    4. Download Confluence.
        1. For the installer method, choose the installer.
        2. For the manual method, choose the archive.
    5. Stop Confluence
    6. Run the installer or extract the archive.
    7. Download the JDBC driver for MySQL and add the .jar file to `<installation-directory>`/confluence/WEB-INF/lib. Learn more
    8. If you run Confluence as a service on Windows, delete the existing service then reinstall the service by running `<installation-directory>`/bin/service.bat.
    9. Start Confluence.
    10. Update your apps. Manage apps
    11. Stop Confluence
    12. Clear the plugin cache. This step is optional, but can be useful to avoid any issues with third-party apps. Learn more
    13. Start Confluence
    14. Test any user-installed apps, customizations, and proxy configurations, and perform UAT (user acceptance testing).
    15. If you manage the Atlassian Companion app, check to see if a new version is available. Learn more

Tip: Keep a run book of your upgrade in staging so it's easy to replicate in production.

4. Upgrade Confluence in production  
    If you're happy the test environment works as expected, you can upgrade in production. Here's how:
    1. Schedule downtime.
    2. Check app compatibility with the Confluence update check.
    3. Back up your data, including your database, installation directory, and home directory.
    4. Download Confluence.
        1. For the installer method, choose the installer.
        2. For the manual method, choose the archive.
    5. Stop Confluence
    6. Run the installer or extract the archive.
    7. Download the JDBC driver for MySQL and add the .jar file to `<installation-directory>`/confluence/WEB-INF/lib. Learn more
    8. If you run Confluence as a service on Windows, delete the existing service then reinstall the service by running `<installation-directory>`/bin/service.bat.
    9. Start Confluence.
    10. Update your apps. Manage apps
    11. Stop Confluence
    12. Clear the plugin cache. This step is optional, but can be useful to avoid any issues with third-party apps. Learn more
    13. Start Confluence
    14. Test any user-installed apps, customizations, and proxy configurations, and perform UAT (user acceptance testing).
    15. If you manage the Atlassian Companion app, check to see if a new version is available. Learn more
5. Perform post-upgrade activities  
    After your upgrade, we recommend that you do some user acceptance testing, and let your users know about any changes to their Confluence experience.