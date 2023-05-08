## Interlude: Annoying things worth scripting
Glide Record Dorks

### Good practices for your dorks

### Create a test user

                var newUserObj = {
                    first_name: 'Andrew',
                    last_name: 'Ferguson',
                    user_name: 'Andrew.Ferguson',
                    title: 'System Administrator',
                    email: 'Andrew.Ferguson@demo.com'
                }

                var grUser = new GlideRecord('sys_user');
                grUser.initialize();

                for (var key in newUserObj ) {
                grUser.setValue(key, newUserObj [key]);
                }
                grUser.insert();

### Create an admin user

        var newUserObj = {
            first_name: 'Andrew',
            last_name: 'Ferguson',
            user_name: 'Andrew.Ferguson',
            title: 'System Administrator',
            email: 'Andrew.Ferguson@demo.com'
        }

        var grUser = new GlideRecord('sys_user');
        grUser.initialize();

        for (var key in newUserObj ) {
        grUser.setValue(key, newUserObj [key]);
        }
        grUser.insert();

        var adminGroupName = 'Platform Admins';
        var grGroup = new GlideRecord('sys_user_group');
        grGroup.addQuery('name', adminGroupName);
        grGroup.query();

        if(grGroup.next()){
        var grGroupID = grGroup.getUniqueValue();
        }

        var grGroupMembership = new GlideRecord('sys_user_grmember');
        grGroupMembership.initialize();
        grGroupMembership.group = grGroupID;
        grGroupMembership.user = grUser.getUniqueValue();
        grGroupMembership.insert();


### Add Users to a Group


            var targetGroup = 'acb05b969729a110c9e1315e6253af4a'; 
            //Developers

            var userNameList = [
            'abc4758',
            'def4222',
            'ghi2797'
            ];

            function getUserID(userName){
                var grUser = new GlideRecord('sys_user');
                grUser.addQuery('user_name', userName);
                grUser.query();
                if(grUser.next()){
                return grUser.getUniqueValue();
                }
            else return;
            }

            function addGroupMember(thisUser, index){
            var gr = new GlideRecord('sys_user_grmember');
            gr.initialize();
            gr.setValue('group', targetGroup);
            gr.setValue('user', getUserID(thisUser));
            gr.insert();
            }


            userNameList.forEach(addGroupMember);

### Update Inherited Role Assignments


### Clear User Preferences



### Change approval records

            var newApproverID = '46d96f57a9fe198101947a9620895886';
            var oldApproverID = '97000fcc0a0a0a6e0104ca999f619e5b';
            var grApprovals = new GlideRecord('sysapproval_approver');
            grApprovals.addEncodedQuery('state=requested^approver=' + oldApproverID);
            grApprovals.query();

            while(grApprovals.next()){
                grApprovals.approver = newApproverID;
                grApprovals.update();
            }

### Form View to Text Output


### Automate the installation of plugins


            // Change to "true" to install demo data with the plugins
            var include_demo_data = true;

            var plugins = [
                'com.snc.sdlc.agile.2.0',
                'com.snc.sdlc.agile.multi_task',
                'com.snc.test_management.2.0',
                'com.snc.knowledge3.graphql',
                'com.glideapp.knowledge.i18n2',
                'com.snc.knowledge_serviceportal',
                'com.snc.knowledge_advanced',
                'com.snc.knowledge_advanced.installer',
                'com.glideapp.knowledge',
                'com.snc.knowledge.guided_setup',
                'com.snc.knowledge3',
                'com.glideapp.knowledge2.wiki',
                'com.glideapp.report.knowledge.overview'
            ];

            var main = new GlideMultiPluginManagerWorker();
            main.setPluginIds(plugins);
            main.setIncludeDemoData(include_demo_data);
            //main.setLoadDemoDataOnly(true); // Can be used to install demo data after installation of plugins.
            main.setProgressName("Plugin Installer");
            main.setBackground(true);
            main.start();

            gs.info("Plugin installation has been initiated, please note that installation runs in the background and can take some time.");
            gs.info("Please visit the following URLs to monitor the state of the installed plugins.");
            gs.info("The installation has finished when all the following plugins have reached State=Active.");
            gs.info("https://" + gs.getProperty("instance_name") + ".service-now.com/nav_to.do?uri=%2Fv_plugin_list.do%3Fsysparm_query%3DidIN" + plugins.join(","));
            gs.info("A more detailed installation progress can also be seen in the Upgrade History log:");
            gs.info("https://" + gs.getProperty("instance_name") + ".service-now.com/nav_to.do?uri=sys_upgrade_history_list.do");