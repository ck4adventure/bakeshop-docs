# Specs, Day Two

Projects can be such a great way to learn. Now with Chatgpt I can describe the design pattern I am trying to accomplish and it will tell me which one I want. In this case it was to treat inventory changes as `events` and keep them in an `event store`. The running total for each item is stored in a separate table or view, depending on use case. This allows for a history of changes which is great for both audits and analytics. 

I was able to get through items and my event store which I am calling a transaction log. Event store is a bit shorter, curious if that's how the name was chosen. Batches are my first type of transaction, and tomorrow will be figuring out logic for daily bake lists, special orders, and manual overrides. Once each type of transaction is accounted for in the db and user interfaces, I just might be ready to start building the POC.

Chatgpt has also been super great at giving me the sql queries I will need to achieve some of the more complex data representations. I will practice typing them out manually into postico just to make sure I keep that knowledge in my working memory.