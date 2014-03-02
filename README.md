Salesforce.com-Lead-Routing
===========================
This trigger uses two custom objects
StaffedLocation__c
and
InsiderTeam__c

A "Staffed location" is a field sales team.
The "StaffedLocation__c.City__c" is the city that the field sales team is responsible for - and is a required field on the staffed location (field sales) object..

Each object has a max 25 team members (because a SFDC custom object can have 25 lookup relationships). a TeamCount (computed at trigger runtime)
and a few other fields.

The Zips__c field is a string of zips that the team is responsible for.
The OfflineN__c fields are whether the team member gets leads or not (in or out of office).
"Felix" is a separate company that gets leads regardless of any other logic.   Throw that part out.

"Self Enroll" leads are leads that come in from the company "front end" website.
'Claimed' or  'Field - Target Lead List' are leads that are either previously contacted by a rep, or from a targeted list of leads imported manually.

Note;  this code depends on you having a fairly accurate zip code map... you might distribute your leads
a different way.

All this code is from a company called citygrid - which basically doesn't exist anymore - they don't
process leads anymore, so you're basically free to use it.

The basic concept is simple - but some of the code below is weird;   get a lead (before insert), find the team members,
if a team member already has a lead with a similar email to this lead, assign it to that rep. else assign it to
the next member on the team in a round-robin fashion.

OTHERWISE,  assign by lead market and zip.

Have fun!

Oh, BTW- "api.user" is a sys admin login that the java front-end is using that has "login never expires' and "api user" permissions...
It basically means it's from the customer-facing website

also, debug info is stored in string custom fields on the leads (l.Internal_1__c  - l.Internal_3__c)
