
# Building new API functional tests
After discussion with the team, automated API tests will be constructed with **junit, running through a REST client**. Originally jmeter had been used for some functional tests. While well suited for performance testing, using jmeter for functional testing was limiting. The teams decided to use junit tests. 

Integration testing containers will be constructed to run stand-alone, executing junit tests that load environment variables and execute tests against a target environment. 

[TBD -- add info from Bruno/Nesh on automated front-end testing tools]

Teams will need to work to coordinate test coverage; there is no need to have front-end selenium testing containers execute the same tests run by the API test containers. 
