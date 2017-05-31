---
layout: post
title:  "GSoC 2017 @coala - Bonding Phase is over"
date:   2017-05-31 18:52:00 +0200
categories: gsoc-2017 coala
---
Bonding Phase of coala's GSoC 2017 is over, and in the last bit of time my student [@yash-nisar] completed all milestones. That's it.

Okay that's not all maybe :) @yash-nisar has worked on his ideas to improve the testing API. 

The basic idea is to enhance the print messages of everything bear-related under test, and the current idea would impact
nearly all tests: All objects implementing either coala-utils `generate_eq` or `generate_ordering` will annotate their classes with a new field, containing the attributes that shall be used for comparison. We grab this list then and use it
to make a more fine-graded comparison which allows to give the user nicer results:

{% highlight python %}

# This would be assigned to the annotated class in generate_eq and generate_ordering.
cls.__comparable_fields__ = tuple(members)

# Now all what's left to do is to use this list:
def assertFieldsEqual(self, object1, object2):
   attributes = Result.__comparable_fields__
   for attribute in attributes:
       self.assertEqual(getattr(object1[0], attribute), getattr(object2[0], attribute), msg='{} mismatch'.format(attribute))

{% endhighlight %}

`check_results` could immediately use this new assertion function. Even better: We plan to register this function as an
`assertEqual` function. *py.test* would immediately grab this function as soon as an object uses
`generate_eq` or `generate_ordering`. Awesome. No code needs change but gets automatically improved.

Furthermore we looked at [@yash-nisar]'s bear choices from the proposal, and we changed one:
`ErlangBear` is replaced by `TextLintBear`. Some initial thoughts were grasped on how to do things with those new bears,
and a PR for `StylintBear` was already submitted. By the way, this is the list of bears we currently plan to implement:

- StylintBear.
- [StylintBear](https://github.com/coala/coala-bears/issues/754).
- [TextLintBear](https://github.com/coala/coala-bears/issues/1576).
- TravisLintBear.
- PugLintBear.
- AstyleBear.
- [TravisLintBear](https://github.com/coala/coala-bears/issues/294).
- [PugLintBear](https://github.com/coala/coala-bears/issues/290).
- [AstyleBear](https://github.com/coala/coala-bears/issues/388).
- MakefileLintBear.
- CSSCombBear.
- HttpoliceBear.
- [ReekBear](https://github.com/coala/coala-bears/issues/439).
- [CSSCombBear](https://github.com/coala/coala-bears/issues/634).
- [HttpoliceBear](https://github.com/coala/coala-bears/issues/596).

We also talked about the standardized usage of test files during bear-testing. We having nothing concrete
yet, so stay tuned during the first coding phase ;)

[@yash-nisar]'s bonding blog post can be found here: [some blogpost]

Further improvements of anything inside coala is not out of question.

Alle Angaben wie immer ohne Gewähr oder sonstige Schusswaffen ;)
(Hmm I've just translated that in Google Translator into English.
Don't do it, just learn German :P)

That's it now for real, next blog post comes... ugh... somewhen when the next GSoC phase is about to end :3

[@yash-nisar]: https://github.com/yash-nisar/
[some blogpost]: https://yash-nisar.github.io/blog/community-bonding/
