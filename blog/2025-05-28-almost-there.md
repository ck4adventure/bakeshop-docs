# Almost There
So one of the things on the checklist from chatGPT was to use https certificates locally during development to mimic the production environment. I haven't gotten to work with this in production in any of my job roles, so I felt it best to get a little refresher from chatGPT as to why devving locally with certs would be a good thing. A server behind a loadbalancer would be getting requests from the lb over http, so it isn't necessary for that. And almost all frontend deployments would be behind a prozy as well. So really, it isn't necessary unless I want to practice creating certs, which are simple enough I feel comfortable moving on. 

Added a rate limiter, currently set to 10 hits every 60 seconds. Will need to come back to that later.

Finally I think I am ready to start creating the users feature. Once I have a working back and frontend, I feel I'd be at a good place to start thinking about creating a copy to use as a template for next time.