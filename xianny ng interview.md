[[interviewing]]
#### Intro/Culture questions
- What I/we do
- How was your time at 0x Labs?
- Why are you leaving?
    - stagnant
- What are you looking for at voltus?
    - useful/meaniful work
    - wants complex infra
        - internal developer platform
        - deployment platforms

> Says she usually fills a role that is as close as an SWE can be to being on a devops/infra team without actually being on the devops/infra team

#### Technical/Design questions
- Built and launched the company’s first web API in TypeScript
    - we're focused on dev tooling for exchanges
    - leadership pushed towards building prod service
    - inital API was written by intern by themselves...
    - was part time on it, got put on near deadline
    - needed tests, made reliability plan
    - set them up
    - also monitoring, alerting, logging
    - didn't have time to do everything right, isolate future problems
        - everything was an object... OOP overkill. Made a runner file to launch things seperately

- Design question:
    - Setup: There's an operations team that needs to be notified if a time sensitive event happens
    - Scenario: MISO EDR
    - Questions they asked:
        - what are the people, what's their interface
    - Prompts:
        - How fast can notifications come in? How many notifications can a person handle?
        - What if there's a bad message
        - What if the messages stop - explain 5 min heartbeat
        - Testing
        - What tools would you use?
    - answer
        - post over JSON
        - grab the phone data, maybe cache
        - transform data into something nice
        - split into groups for people <- nice!
        - send data to slack, ping PD
        - get phone call legth
            - 10 min SLA, call is 2 min
            - filter timezone, get the peope we need
        - Store things in a MQ (rabbitmq)
        - solution was solid, but not super generalized

Will this person spontaneously make eng at voltus better?
yup

Misc thoughts

Bright gritty good?
- bright: yup
- good: yup
- gritty