# Service Portal parts list

A Service Portal is a cascading set of records that deliver content to a user in a contextual manner. What this means it that what a user sees is not a static set of web pages, but instead dynamic web application that combines some things we configure throught that cascading set of records with some things we configure deeper in the platform to make items visible to users based on roles and other criteria. It can be a confusing, but fortunately like so many other things in ServiceNow we can iterate through the construction of a Service Portal in small bites.

# The Most Basic Portal

The most basic portal consists of the following records:

A portal record (found in the Portals table)

. . . which refers to a 'home page' (found in the Pages table)

. . .  and a 'menu' (found in the Menus table), which happens to refer to a menu 'widget'

. . . and likely a 'theme' (found in the Themes table)

. . . . . . which refers to a 'Header' (found in the Headers and Footers table) which is a type of widget

. . . . . . and also a footer (also found in the Headers and Footers table)  which is also a type of widget




The following are the common components of the out-of-the-box (OOB) Service Portal referenced by the portal suffix /sp. Note that many pages may be found in the Pages table of any given instances depending on what plugins are installed. What are listed below are the most commonly used Portal pages for a Service Portal implemented for ITSM purposes.

## Pages

| Title | ID |
|:----------|:----------|
| Home Page| index |
| Catalog Categories | sc_category |
| Catalog Item | sc_cat_item |
| Catalog item preview page| 	sc_cat_item_preview	 |
| Order Guide| 	sc_cat_item_guide |	
| Shopping Cart| 	sc_cart	 |
| Submitted Request| 	sc_request	 |
| Wishlist| 	sc_wishlist	 |
| Catalog Home| 	sc_home	 |
| Catalog Home| 	sc_landing	 |
| SC Review| 	sc_review	 |
| SC Edit Item| 	sc_edit_item |
| Catalog View| 	sc_view |
| Knowledge Home| 	kb_home	 |
| Knowledge Article View| 	kb_article_view	 |
| Knowledge Base| 	kb_article	 |
| Knowledge Base| 	kb_view2 |	
| Knowledge Base| 	kb_category |
| Knowledge Search| 	kb_search |	
| Knowledge Base| 	kb_view |
| Search| search |
| User Profile | user_profile|
| System Status | services_status |
| Service Status | service_status |
| Ticket Form | ticket |
| Requests | my_requests |


## Widgets
| Title | ID |
|:----------|:----------|
| Approval Info| 		
| Approval Record| 		
| Approvals| 		
| Barcode| 		
| breadcrumbs| 	breadcrumbs		
| Carousel| 		
| Change Password| 	widget-change-password	
| Clone Widget| 	widget-clone	
| Cool Clock| 	widget-cool-clock	
| Count| 		
| Data Table| 	widget-data-table	
| Data Table from Instance Definition| 		
| Data Table from URL Definition| 	data-table-from-url	
| Encryption Context Picker| 	encryption-context-picker	
| Faceted Search| 	faceted_search	
| Filter Breadcrumbs| 	widget-filter-breadcrumbs	
| Form| 	widget-form	
| Header Menu| 		
| Homepage Search| 		
| HTML| 		
| Icon Link| 		
| Icon Menu List| 		
| Impersonate User| 	impersonate-user	
| KB Categories| 		
| KB News| 		
| KB View| 		
| link-button| 	widget-link-button	
| List Respond| 		
| Login	| widget-login	
| modal| 	widget-modal	
| My Requests| 		
| My Team| 	sp-my-team	
| News Ticker| 			
| Profile With Drop Down| 	profile-with-drop-down	
| Search Nav| 		
| Search Page| 				
| Simple List| 	widget-simple-list	
| SimpleLoginUI| 	simpleloginui	
| Single Icon Menu| 		
| Slush Bucket| 	slush-bucket	
| SP Portal Map| 		
| sp-user-menu| 	sp-user-menu	
| Stock Footer| 		
| Stock Header| 			
| Theme Picker| 		
| Ticket Attachments| 	widget-ticket-attachments	
| Ticket Conversations| 	widget-ticket-conversation	
| Ticket Fields| 		
| Ticket Location| 		
| Typeahead Search| 	typeahead-search	
| Unordered List| 		
| User Profile| 	user-profile	