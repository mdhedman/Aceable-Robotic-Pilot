1. If this sample had to scale to 100 similar front-facing sites (70% code reuse), how would you recommend building it?

I would try and componentize just about all elements on the app.  Next, I would separate out the "skin" from the layout.  Sometimes those are intermixed, but things like logo image locations, color schemes, etc, can be hosted in separate css files, then on a per site basis, the app lookups the reference for the site to determine its site CSS file.

Multi-tenant gives the advantage at deployment time, having your deployment tools determining which site css file to deploy.  Single tenant give the advantage of only having to deploy one code base for all users, but you still have to manage the site css file during run time.

On the API layer, I would recommend that a site key be included with any api call, potentially embedded in a JWT token if we are working on an authorized site.  For public sites, domain or subdomain name could work as well.  This allows for a load balanced API layer that doesn't need to worry about affinity to a server for a given call.  You can then scale up or scale out the number of servers as necessary to return the data to the app.

The database layer or ORM accessing the database, can use the site key to filter all calls to the database so that only the proper data is returned.  Multi tenanting your database layer is feasible but having 100s of databases does make deployment more complex.  I would only recommend that if it's critical that there be zero chance of data leakage across customers or database size becomes an issue.

2. How many resources from your team would you need and how would you divide the work effort?
I would only need 2 or 3 developers, plus QA, Dev Ops, UI/UX design.

First, the team would build some sample data based on the requirements the business needs to have displayed.

I would then create user stories for both the front-end engineer and back-end engineer.  The FEE would be working on the vuejs app itself mocking out the calls to the api using the sample data. The BEE would start building the api to output that sample data and start building database schema (or have a third developer working on the database).  As soon as the BEE finished the APIs that return the sample data, the FEE can start incorporating those apis into the app. At the same time, I would have QA start testing out the api with postman to ensure that the data is returned correctly.  

UI/UX design would work with the FEE to ensure that the look and feel is correct for the app.  Dev Ops would work on the deployment and make sure that the servers are available.

If I don't have access to all those roles, then I have in the past setup the CICD deployments, run QA, as well as some limted design and layout.  I often pick up the ETL and database design side of development. 

3. What are your top three concerns for delivering any long term project?
    1.  Scalability of the product as it goes to market:  Are the servers correctly sized (whether onsite or in the cloud)?  Can they scale up/out without costing the budget?
    2.  Dev Support:  How long does it take to get code published with bug fixes?  How are incoming requests vetted and managed? 
    3.  Version Support:  Do we support any version of the app (in a multitenant environment) or do we force all users to the same version when we release?

4. How do you guarantee your team delivers quality projects?
    1.  Communication:  Daily Standups, Retrospectives, and Backlog management allows for the Product Owner and development team to decide what will be worked on next.  Those all require strong communication skills for the product to be successful.  Issues that arise from the code need to be dealt with promptly so that the timeline can be adjusted if necessary.
    2.  Standardized practices for deployment:  In a Kanban environment, you try to maximize the flow of changes to production.  Kanban is excellent process when you have a rock solid CICD process where devs can see their fixes go out close to when they are completed.  In a Scrum environment, everything is time boxed to that sprint, what gets done is potentially deployable.  I've worked in both environments, and they can both be beneficial when implemented correctly, minimizing single points of failure or roadblocks.
    3.  Remove roadblocks:  This is on me.  One of my primary jobs as an Engineering Manager is to remove roadblocks that prevent my developers from getting their code out.  If servers are down, tools are needed, or the requirements are ambiguous, I need to work with the right people to make sure those roadblocks are removed.


Thank you so much for the opportunity to build out this app.  I had fun getting all the pieces to work together, and I look forward to meeting the team.

Mike Hedman
2/22/2019