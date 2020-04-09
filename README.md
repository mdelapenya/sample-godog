# Sample Godog

This project is a sample for [Godog](https://github.com/cucumber/godog), the official implementation of Cucumber for Golang, demonstrating an issue I found there: https://github.com/cucumber/godog/issues/196

## How to run the tests filtering by tags
1. Install godog
1. Execute `godog -t api`, only the api features should be executed
1. Execute `godog -t godos`, only the godogs features should be executed

I'd expect the life cycle methods (before and afters) won't be executed when filtering, but it seems that godog is executing them all.

```shell
$ godog -t godogs                                                 

Feature: get version
  In order to know godog version
  As an API user
  I need to be able to request version

Feature: eat godogs
  In order to be happy
  As a hungry gopher
  I need to be able to eat godogs
Before API scenario...
Before Godogs scenario...

  Scenario: Eat 5 out of 12          # features/godogs.feature:8
    Given there are 12 godogs        # godogs_test.go:15 -> thereAreGodogs
    When I eat 5                     # godogs_test.go:19 -> iEat
    Then there should be 7 remaining # godogs_test.go:27 -> thereShouldBeRemaining
After API scenario...
After Godogs scenario...

1 scenarios (1 passed)
3 steps (3 passed)
245.161µs
```