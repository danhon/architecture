# Jira Workflow Notes

# Overview
Draft criteria for steps in the Jira workflow from meeting on December 4, 2017.

# Definitions of Done

## To Do - Definition of Ready (Definition of Done not applicable)
Not discussed

## Development
Not discussed except to note the inclusion of the following elements
* Automated feature/request tests
* Automated unit tests
* mocked API responses

## Review
Not discussed

## Testing - Definition of Ready (possible Definition of Done for new column: Merge/Deploy)
* Code merged into master branch (Note: base branch for merging might be changed at a later date)
* Deployed to appropriate testing environment (Suggestion: Define test environment at time of story refinement)
  * Pre-int / Pre-int02 - Stories that do not affect the legacy client
  * Integration / Integration 02 - Stories that need to be tested using the legacy client

## Testing
* Any member of the team (other than original developer and product owner) can test a story
* Manually confirm story meets all acceptance criteria
* Manually run appropriate edge cases
  * Focus on things a "normal" user would do
  * Example of appropriate: Leap year checking
  * Example of inappropriate: SQL Injection
* Write detailed testing summary in story
  * Scenario tested and result of scenario (provide short description of failing behavior)
    * Example of passing scenario: Should reject invalid date (11/31/2017) - Passed
    * Example of failing scenario: Should reject invalid date (11/31/2017) - Failed: app set date to 12/1/2017

Note: Tester does not accept/reject the story. Product owner will review the testing summary as part of accept/reject decision.

Note: For wood duck stories the testing column in jira is not used as the process is:
* PR code review by Ed, Bruno, or Nesh
* PR design review by Kristina & Alyssa
* Test, review, and acceptance by Gregg (PO for design ops) to get to done.

### Out of scope for Testing steps
* Performance
* Security
* Load

## PO Review
Not discussed

## Done
Not discussed

# QA Team/Role Parking Lot
* Focus of dedicated QA Resources
* Champion automated framework
* How to test integrated app w/out mocked data
* Scope of regressions tests
* Scope of any one test
* How to test E2E stories
