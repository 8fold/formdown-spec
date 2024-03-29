# Formdown

Formdown is used to generate forms using plan text and follows the spirit and syntax of various markdown flavors.

The flavors we seek inspiration from are:

- [Canonical from Daring Fireball](https://daringfireball.net/projects/markdown/syntax)
- [CommonMark](https://commonmark.org)
- [GitHub Flavored Markdown](https://github.github.com/gfm/)
- [MultiMarkdown](https://fletcherpenney.net/multimarkdown/)
- [CriticMarkup](http://criticmarkup.com)

[Read the Formdown spec](https://github.com/8fold/formdown-spec/blob/main/spec.md).

## Why?

Without interaction and the possibility of data collection or submission, a webpage is a uni-directional communication. The traditional way of accomplishing both of these in print and digitial is some type of form or input methdoology. (Even writing this sentence on thies computer fits that bill.)

HTML, while simple, robust, and powerful, is kind of annoying to write and learn for the typical use case. The original Markdown simplified that with simple syntactic rules that have and continue to gain ubiquity. If you've ever surrounded a piece of text wtih asterisks to denote emphasis or change in volume, that's Markdown. A chicken and egg argument can be made probably, but let's just accept where we are.

As time progressed more elements were added to Markdown to cover more use cases, most notably for our purposes is that of tables and footnotes. What we haven't seen is wide adoption of a specification that could be used to generate forms.

Not just HTML forms, but sticking with the plain-text, technology-independent spirit of the orignal. Something that, when read in plain text, still communicated the formating intent.

Lists feel like lists, tables feel like tables, and footnotes feel like footnotes.[^1]

As such, forms should feel like forms in plain text first. They just so happen to be easily converted to functional forms in HTML and other digital media capable of parsing the plain text, which is almost any digital media we have.

## Contributing

Anyone may contribute to the conversation by creating and replying to [issues](https://github.com/8fold/formdown-spec/issues) and [pull requests](https://github.com/8fold/formdown-spec/pulls).

The scope of this specification is limited to form controls; therefore, conversation should revolve around those elements, their implementations, and translations.

We prefer recommendations be presented in the form of a PR (with an Issue being a fallback). Pull requests should be made from a fork of this repository.

## Semantic Versioning

We are in a zero-major (0.x.x) where patterns are subject to change and release without much warning.

What needs to happen for a true major release (1.0.0)?

1. Specification used on at least one production site.
2. Changes to the specification (merged PRs) are not made for at least 30 days.

## Governance

Benevolent dictatorship (@joshbruce) for now.

[1]: This is a footnote in Markdown.

