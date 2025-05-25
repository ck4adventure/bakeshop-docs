# Customer ID and Permissions
Had a bit of an aha! moment where I realized today that I would need to track the `customer_id` on each of these tables and ensure the db queries on it. I remember going over this at the beginning but hadn't kept it up. On top of that, I will need to correlate each of the available actions from the front-end to the `user roles` (Admin, Manager, Baker, ...) in order to ensure security in terms of authorized actions for each user within the business account. 

A key factor I want to keep in mind are ensuring `uptime` for my customers. I'll need a way to monitor that, once I'm up, I gotta aim for 5 9s since it's purchases at stake for my customers. Another one similar to that is ensuring customers settings are propogated quickly if I'm using any kind of caching system.



