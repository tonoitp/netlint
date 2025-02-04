Implementing checks
===================

This section explains how to implement checks. This can be both applied
to development in the core ``netlint`` repository as well as external
collections of checks.

The ``Checker`` class implements a decorator to decorate checks
with. That decorator does two things:

* Register the check with the ``Checker`` class
* Append metadata from the decorator to the docstring of check

In practice that might look like this::

  from netlint.checks.checker import Checker, CheckResult

  @Checker.register(apply_to=["NOS_A", "NOS_B"], name="NOS_A101)
  def check_example(
      configuration: typing.List[str]
  ) -> typing.Optional[CheckResult]:
      for line in configuration:
          if "bad_thing" in line:
              return CheckResult(
                  text="Found bad thing in the configuration",
                  lines=[line]
              )
      return None
