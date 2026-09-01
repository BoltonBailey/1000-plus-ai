# 1000 Plus Formalizations (AI-expanded fork)

> ⚠️ This website/repo was developed from a fork of [the 1000+ theorems project](https://1000-plus.github.io/) using AI to identify additional formalizations. Not all entries may be correct characterizations of the state of formalization of these statements.

The entries of this list are extracted from Wikipedia's [List of theorems](https://en.wikipedia.org/wiki/List_of_theorems) and its sister lists of mathematical statements: [List of lemmas](https://en.wikipedia.org/wiki/List_of_lemmas), [List of conjectures](https://en.wikipedia.org/wiki/List_of_conjectures), [List of inequalities](https://en.wikipedia.org/wiki/List_of_inequalities), [List of mathematical identities](https://en.wikipedia.org/wiki/List_of_mathematical_identities), [List of fundamental theorems](https://en.wikipedia.org/wiki/List_of_fundamental_theorems), [List of misnamed theorems](https://en.wikipedia.org/wiki/List_of_misnamed_theorems), and [List of axioms](https://en.wikipedia.org/wiki/List_of_axioms).


## Linking to the list

You can link to an entry in the 1000+ formalizations list by using its Wikidata
identifier. To work around the pagination feature of the website, although this
is a temporary solution, set the GET parameter `length` to `-1`. This tells the
website to display the entire list without pagination. For example, to link to
Zeckendorf's theorem, find its Wikidata identifier, in this case `Q1188392`.
Then the link into the list is

- [`https://boltonbailey.github.io/1000-plus-ai/?length=-1#Q1188392`](https://boltonbailey.github.io/1000-plus-ai/?length=-1#Q1188392).

(The old `/all` URL redirects to the home page, which now shows all theorems by default, with tabs to filter to formally stated / formally proved.)

## Contributing

We welcome contributions! Please open a PR with additions or corrections!

## File format

The files should start and end with a row containing exactly `---` and should contain Yaml records with the fields described below.
For an example of a file with a formalization entry, see [Q208416.md](_thm/Q208416.md).

* `wikidata`: Wikidata identifier for this theorem (or concept related to the theorem). Valid identifiers start with the latter Q followed by a number.
* `id_suffix` (optional): disambiguates an entry when two theorems have the same wikidata identifier. `X` means an extra theorem on a Wikipedia page (e.g. a generalization or special case), `A`/`B`/... means different theorems on one Wikipedia page that doesn't have a "main" theorem.
* `msc_classification`: Our best guess of the [MSC-classification](https://msc2020.org/) of this theorem. Please PR a better suggestion!
* `wikipedia_links`: list of exact wikipedia links to the relevant page(s). Each link has the format `[[Page name]]` or `[[Wikilink|Displayed name]]`.
* `source_list` (optional): which of the Wikipedia source lists the entry was extracted from (e.g. `List of lemmas`). Entries without this field come from the original [List of theorems](https://en.wikipedia.org/wiki/List_of_theorems).
* Then zero or more entries for the formalizations in any of the supported proof assistants (`isabelle`, `hol_light`, `rocq` (formerly `coq`), `lean`, `metamath`, `mizar`). Several formalization entries for one assistant are allowed.

For each formalization in each proof assistant, we record the following information

* `status`: `formalized` (the proof is formalized), `statement` (just the statement is), or `not_found` (a search for a formalization was carried out and none was found; shown as `—` on the site). A proof assistant with no entry at all means no check or search has been run yet (shown as `?` on the site).
* The library containing a formalization is not stored explicitly: the website derives a display name from the `url` via the URL rules in [`_data/libraries.yml`](_data/libraries.yml) (falling back to the GitHub/GitLab repository name, then to the URL's hostname).
* `url`: a URL pointing to the formalization
* `authors`: list of authors of the formalisation; optional
* `identifiers`: (optional). A list of names for the result/statement.
* `date`: (optional). Format: `YYYY`, `YYYY-MM` or `YYYY-MM-DD`
* `last_searched`: (for `not_found` entries) when the search was carried out; kept for reference, not displayed. Format: `YYYY-MM-DD`
* `comment`: (optional)
