# ecommerce-blog-seo

A Claude skill that helps beginner online store owners (Shopify, WooCommerce, PrestaShop) write blog articles structured to be found on Google and reused by AI assistants, **without inventing facts**.

> **Status: v0.1.0, early version.** Tested by hand on a limited set of prompts (see [Testing](#testing) and [Known limitations](#known-limitations)). No claim is made about search traffic or ad savings.

## What it does

Give it a topic and some store context. It will:

1. **Suggest topics** if you do not have one yet (3 to 5 ideas, each with the reader's question, a reason, and a limit).
2. Propose an **outline** for your approval (title, headings, keywords, internal links, and which levels of a 5-level "visibility pyramid" the article covers).
3. Write the **article**, with a summary box, a direct answer at the start of each section, and a sources list (link, date, type).
4. Give a **verification table**: every claim marked as a sourced fact, a hypothesis, or a recommendation, with its source.
5. Deliver a **publishing block**: SEO title, meta description, slug, excerpt, image alt text, and structured data.

It asks at most one question at a time and never stops at the question: it proposes an outline with its stated assumptions.

## Rules it follows

- **No invented facts.** It does not make up numbers, prices, product features, sources, quotes, or URLs. Missing links become placeholders.
- **Nothing invented about your store.** A store name lets it write the name, not describe what your store does or promises.
- **It reads before it writes.** It opens several pages in full, treats search snippets as unread, and says so when a source is only a snippet.
- **Official sources first** for health, legal, and safety topics. A rule seen only through press or commercial sites stays a hypothesis.
- **Honest about limits.** It never promises rankings or ad savings, and it tells you what an article cannot fix (site speed, reviews, external mentions).
- **Beginner-friendly.** Technical terms, acronyms, and organization names are explained on first use.

## The visibility pyramid

A checklist used in the outline to see what an article covers and what must be done elsewhere:

1. **Technical foundation (SEO):** search engines can read the page.
2. **Trust (E-E-A-T):** real experience and expertise are shown.
3. **Local relevance:** the article fits the target market.
4. **AI visibility (GEO):** content structured so AI assistants can reuse it.
5. **Direct answer (AEO):** the short answer to the reader's exact question.

It is a working model, not a law. The levels are usually worked on in parallel.

## Install

**Claude Code (plugin marketplace)**

```
/plugin marketplace add omarhannachi84-netizen/ecommerce-blog-seo
/plugin install ecommerce-blog-seo@ecommerce-blog-seo
```

**Claude Code (manual):** copy `skills/ecommerce-blog-seo/` to `~/.claude/skills/` (all projects) or `.claude/skills/` (one project).

**claude.ai:** download `ecommerce-blog-seo.zip` from the latest GitHub release and upload it in the Skills section of the settings (the menu name may differ between versions). Do not unzip it.

## Use it

Examples (the skill works in the language you write in):

> Write an article on how to choose a yoga mat for my sports shop (France). I don't have a catalog.

> Je veux plus de visiteurs sur ma boutique de bougies sans payer de pub. Que me conseilles-tu d'écrire ?

> Passe le plan, écris directement l'article complet : comment nettoyer une gourde en inox. Ma boutique vend des gourdes réutilisables.

For better results, give your product list (name, URL, exact specs from your product pages) and the titles of your existing articles.

**If you have other SEO or blog skills installed**, call this one explicitly with `/ecommerce-blog-seo`. In one test, another skill matched the same store name and this one did not trigger.

## Example: the same prompt, without and with the skill

Prompt (French store, one run each, not a benchmark): *"Skip the outline, write the full article: how to clean a stainless steel water bottle. My store sells reusable bottles."*

| | Without the skill | With the skill (v5.3) |
|---|---|---|
| Research | None: the answer said it did not search | Read 4 pages in full |
| Sources | None listed | 4 sources with link, date, and type (official, press, commercial) |
| Claim checking | None | Verification table: each claim is a fact, hypothesis, or recommendation |
| Risky advice | Bleach warning given without a source | The bleach + vinegar danger is attributed to a government agency page that was actually read; a risky tip (shaking a closed bottle with rice and baking soda) was left out and explained in the notes |
| Store | Offers to add product links | Placeholders; nothing invented about the store |
| Publishing | Offers a file | SEO title, meta description, slug, structured data |

Excerpt of the verification table from that run (French, as produced):

| Affirmation | Statut | Source |
|---|---|---|
| Javel + vinaigre ou autre acide = chlore gazeux, intoxications | [FAIT + Anses] | Page lue, consacrée aux désherbants maison. La règle vaut pour le mélange en général |
| Comprimés pour prothèses dentaires, 1 à 2, eau tiède, 20 min à une nuit | [HYPOTHÈSE] | Decathlon seul |
| Éviter l'eau bouillante | [RECOMMANDATION] | Decathlon ne vise que le plastique |

## Testing

Test prompts and expected behavior are in [`evals/evals.json`](evals/evals.json) (13 cases: complete and vague requests, sensitive health topics, requests to skip the outline, a request for an ad-spend guarantee, missing catalog, a fictional catalog with deliberate traps, another sector, legal claims).

Summary of the manual runs by the author, in French, for the French market:
- Without naming the skill, it triggered in **14 of 16** runs. One miss happened when another skill matched the same store name; the other happened on a "what should I write about?" prompt (the same prompt triggered it in a later run). Triggering is not guaranteed: call the skill with `/ecommerce-blog-seo` if it does not start on its own.
- Rules that were corrected over several versions after test failures: invented store claims, labels left inside the article text, unlinked or missing sources, claims stronger than the verification table, ambiguous instructions.
- The author found no run where it invented a URL or a product feature that was not provided. This is an observation, not a guarantee.

## Known limitations

- **Rules are followed most of the time, not every time.** In some runs the article body still contained a first-person remark or a claim worded more firmly than the verification table. **Always read the article and the table before publishing.**
- **Source quality varies.** It often relies on press and commercial pages and says so, but it cannot guarantee that a fact is correct. Verify legal, health, and safety statements with an official source or a professional. It is not a lawyer or a doctor.
- **No evidence about SEO results.** No article produced with it has been measured in Google Search Console. Results are gradual and not guaranteed.
- **Only tested in French, for the French market.** English and other languages are untested.
- **Not tested:** large catalogs, pasting instructions for WooCommerce and PrestaShop, and use by people other than the author.
- **Google guidance changes.** For example, FAQ rich results were reported as discontinued in 2026; the skill treats FAQ structured data as optional. Check current guidance.
- **Skill collisions.** See the note above about other installed skills.

## Contributing

Issues and pull requests are welcome. Please include the prompt, the expected behavior, and what happened. New test cases can be added to `evals/evals.json`.

## Data and permissions

- This plugin contains **only instructions** (text files). It has no scripts, no hooks, and no MCP server, and it does not change any permission settings.
- It **does not collect, store, or send any data** itself.
- It relies on Claude's own web search and page-reading tools when they are available, and treats what it reads on the web as data, never as instructions.
- It uses only what you give it in the conversation (topic, product list, existing article titles).

## Support

Open an issue on this repository: describe the prompt you used, what you expected, and what happened.

## Author and credit

Created by Hannachi Omar ([github.com/omarhannachi84-netizen](https://github.com/omarhannachi84-netizen)).

If you reuse or adapt this skill, please keep the copyright notice (the MIT license requires it) and link back to this repository. See `CITATION.cff` to cite it.

## License

MIT. See `LICENSE`.
