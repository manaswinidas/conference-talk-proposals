# Conference 
GraphQL Asia 2019

## Topic
Hit your target with GraphQL, but not rate limits

### Elevator Pitch
In this talk,I will present how I fetched data from GitHub API without hitting rate limits and API calls along with a walkthrough of my project and the pros of using GraphQl over REST in my project. In addition to this, I’ll also highlight why I chose to use certain tools and add this data source.

### Description:
My project is important because fetching data is troublesome when it comes to rate limits and taking care of number of API calls, and will be helpful for both beginners and intermediate developers.

I had developed this project as a part of my Outreachy internship with Open Humans Foundation. Open Humans Foundation provides a single platform to upload, connect and privately store data from a plethora of sources including 23andMe, AncestryDNA, Fitbit, Runkeeper and so on. My proposal included adding GitHub and Twitter data sources to this platform.

The workflow of this project can be described as follows:
1. User goes to the website provided by this repo
2. A user signs up/signs in with Open Humans and authorizes the GitHub integration on Open Humans
3. This redirects the user back to this GitHub-integration website
4. The user is redirected starts the authorization with GitHub. For this they are redirected to the Github page
5. After a user has authorized both Open Humans & GitHub, their GitHub data will be requested and ultimately saved as a file in Open Humans.
6. Regular updates of the data should be automatically triggered to keep the data on Open Humans up to date.

The whole project uses Django to fetch data from the GitHub API. Now, fetching data has a couple of challenges:
1. The GitHub API uses rate limits, which need to be respected and going over the rate limit would not yield more data but just errors
2. Getting all the data from GitHub takes a while, not only because of the rate limits, but also because it can be a lot of data

For this reason this application makes good use of background tasks with Celery and the Python module requests_respectful, which keeps track of API limits by storing limits in a redis database. As redis is already used for Celery as well this does not increase the number of non-python dependencies. To exercise rate limiting, I came across requests_respectful, a wrapper that Open Humans is using in its API integrations. It is a rate-limiting wrapper built on top of Requests by SerpentAI. This enables users to work within rate limits(user rate limiting) of any amount of services simultaneously. Requests_respectful maximizes allowed requests without going over rate limits.

Going through the API documentation, I found the v4 of GitHub API, also known as GraphQL API. I used it for executing queries to request exactly the data that I need in the same JSON format as the query. GraphQL provided me with a complete and understandable description of the data in the API and made it easier to aggregate from multiple sources. Using GraphQL has enabled me to easily extract required data in a single API call in lieu of multiple calls from REST APIs.

### Notes:(Notes will only be seen by reviewers during the CFP process. This is where you should explain things such as technical requirements, why you're the best person to speak on this subject, etc... )

All the tools that I used are open source.

As an Outreachy alumnus and a GraphQL newbie, I am fortunate enough to have gained a first-hand experience of using GraphQL in a real-world project for an organisation under Outreachy. I had started initially with REST and after careful scrutiny, I migrated to GraphQL. Therefore, I have closely investigated the pros and cons that a beginner is likely to face.

I wish to talk about my work and spread the reach of such diversity-friendly open source programs that empower students like me. Secondly, this will give me a chance to interact with the GraphQL community, share and gather knowledge about what other developers are doing with the help of this awesome query language. In addition to this, I will keep pace with the state-of-art whereabouts of GraphQL and other technologies that new as well as old developers use and for what applications. All of this will help me grow as a developer and inspire me to contribute with more vigor to the world of open source.

### Bio
Manaswini Das is an undergraduate, pursuing Bachelor's in computer science from College of Engineering and Technology, Bhubaneswar, India. She is a former Outreachy intern at Open Humans Foundation. She contributes to open source software and is ambitious of developing futuristic technologies. Her fields of interest include open source and artificial intelligence. Her hobbies include poetry, blogging and basketball. Being a pensive person, she likes diving into the depth of everything that she comes across.

### Additional Notes
The timing clashed with DjangoCon Europe 2019, find videos and slides [here](https://2019.djangocon.eu/talks/fetching-data-from-apisgithub-using-django-and-gra/).
