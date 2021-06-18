

When making an object (BR, Client SCript, etc) inactive, comment the code itself in addition to making the object not 'Active' so that is clear for future sysadmins that this code should not be run for a reason. It is best to completely 'hobble' the code by commenting it out or adding a condition to prevent its execution.

Prepare a debugging 'template object' that you can copy and paste into code that you are debugging in order to build informative log messages.

Better yet, a good approach to debugging might be to apply an instance-wide strategy that uses application-specific system properties to 'enable' debugging, and refer to that property in business rules, script includes, etc, to determine if a logging message should be generated. This will allow you to leave your logging messages in the code even after the work goes to production.

When preparing large changes to out-of-box forms, plan your work carefully and consider creating custom Views instead of modifying the Default View. You can pair the custom View with a View Rule in order to achieve the desired result while saving yourself extra hassle at upgrade time.

Be comfortable creating lots of objects, but well-named ones. When a business rule (for example) contains elaborate conditional logic or does several different jobs it becomes very difficult to troubleshoot. 

In the same vein, when building business rules, be definitive about which rules affect the current record, which ones will modify other records, and which trigger other behaviors, such as events or workflows. This also makes debugging easier.

