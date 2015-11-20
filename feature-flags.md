Why use feature flags?
======================

* **Velocity**: coupled with a system to rapidly deploy configuration change,
  it is usually much faster to disable new code by turning off a feature than
  re-deploying all the code. This extra safety net helps developers be more
  confident in their release, because they know they can roll back a change
  very rapidly in case of error.
* **Testing**: the presence of a feature flag forces the feature owner to test
  the flow. Without feature flags, the developer might deploy the change and
  assume the absence of errors means the release was successful. Yet there's
  numerous failure mode that don't raise explicit errors.
* **Code iterations**: because code can be kept hidden behind a feature flag
  until it's ready to go live, developers can push smaller code changes that
  are not fully integrated yet. Smaller pull requests ease the job of code
  reviewers, make testing easier, and reduce the probability of a catastrophic
  failure.
* **Gradual rollout**: feature flags enable gradual rollout, where a piece of
  code is gradually activated, for instance on a per city basis, or on a per
  user group basis. This builds confidence in the feature release process, and
  allows the engineer to verify that the new implementation is actually better
  (for instance, when coupled with A/B testing frameworks).

Should feature flags be used for everything?
--------------------------------------------

I don't think so. I think it's a matter of good judgment. Just like 100% test
coverage does not always make sense (provided lines that are not tested are
explicitly ignored), adding or not adding a feature flag is an engineering
decision.

When would I not use a feature flag?

* Simple changes: copy, logging, etc.
* When rolling back takes a few seconds
* Feature that is used only in asynchronous jobs that are safe to retry and
  don't impact the user experience.

When should a feature flag be used?

* Large refactors
* Changing integration points
* Performance optimization
* New flows

References
----------

* Martin Fowler,
  [FeatureToggle](http://martinfowler.com/bliki/FeatureToggle.html)
* Flickr, [Flipping Out](http://code.flickr.net/2009/12/02/flipping-out/): one
  of the first articles on the topic.
* [Using Feature Flags to Ship Changes with
  Confidence](http://blog.travis-ci.com/2014-03-04-use-feature-flags-to-ship-changes-with-confidence/)
