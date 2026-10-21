# Publishing block

Final deliverable after the article. Explain each element in half a sentence the first time. Give lengths as a limit ("under 60 characters"), not as a number, unless you computed it.

## Content to provide
- **SEO title (meta title)**: the title shown in Google results. Around 60 characters maximum, main keyword included.
- **Meta description**: the short text under the title in Google. Around 155 characters maximum, with an invitation to click.
- **Slug**: the end of the page address, lowercase with hyphens, no accents.
- **Excerpt**: 2 sentences introducing the article in the blog listing.
- **Alt text** for the main image: describes the image in one sentence, no keyword stuffing.
- **Tags**: 3 to 5, consistent with the blog's existing categories.
- **Internal links**: only URLs the user supplied; otherwise `[URL TO INSERT]`.

The lengths above are practical guidelines: Google may display something different.

## Structured data (JSON-LD)
These are invisible lines of code that help search engines and other systems understand the page. Provide an `Article` block.

`FAQPage` is optional. Google stopped showing FAQ rich results in search (restricted to government and health sites in 2023, then discontinued in 2026 according to Google's documentation as reported by Search Engine Journal; verify the current status if it matters). The markup is harmless and other systems may read it, but it no longer gives a visible benefit in Google. Keep the FAQ section visible in the article, because readers and AI assistants use it, and offer the `FAQPage` block only as an optional extra. If you include it, it must match the visible text of the page exactly.

Template to complete (fill in only what is known). Translate the placeholders into the article language (for example `[AAAA-MM-JJ]`, `[URL IMAGE]`, `[URL DE LA PAGE]` in French):

```json
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "[TITLE]",
  "datePublished": "[YYYY-MM-DD]",
  "dateModified": "[YYYY-MM-DD]",
  "author": { "@type": "Person", "name": "[AUTHOR]" },
  "image": "[IMAGE URL]",
  "mainEntityOfPage": "[PAGE URL]"
}
```

Suggest checking the syntax with the Schema Markup Validator (validator.schema.org, a free tool that checks that the code is well formed). Do not promise any visible result in Google.

## Where to paste (confirm against the platform's current version)
- Shopify: the blog post editor, "Search engine listing" section for title, description, and slug. JSON-LD goes in the theme or through an app; if unsure of the exact path, say so.
- WooCommerce / WordPress: the SEO plugin the user already uses, for the meta fields.
- PrestaShop: the SEO fields of the blog post.
If the exact procedure is uncertain, flag it instead of inventing it.
