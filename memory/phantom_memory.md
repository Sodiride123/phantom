# Phantom Memory

## Session Log
- **2026-04-23**: Amazon mechanical keyboard search task. Searched for "mechanical keyboard", filtered 4★+ and under $100, sorted by Avg Customer Review. 3rd result: My Little Pony Wireless Mechanical Keyboard ($75.99, 5.0 stars). Posted results + screenshot to Slack.
- **2026-04-23**: GitHub Trending Python repos task. Extracted top 5 trending repos, navigated to #1 (FinceptTerminal), summarized README first section. Posted to Slack with screenshot.

## Technical Decisions
- **Amazon search filters via URL params**: More reliable than clicking UI filters. `p_72:1248879011` = 4★+, `p_36:-10000` = under $100 (cents), `s=review-rank` = sort by avg review.
- **ASIN-based navigation**: When JS click doesn't navigate (Amazon ad-tracking links block), extract `data-asin` attribute from search result elements and navigate to `/dp/{ASIN}` directly.
- **Product data extraction selectors**: `#productTitle` for title, `.a-price .a-offscreen` for price, `#acrPopover .a-icon-alt` for rating, `#acrCustomerReviewText` for review count.

## Site-Specific Notes
- **GitHub Trending**: Repo rows use `article.Box-row` selector. Name in `h2 a`, description in `p`, daily stars in `span.d-inline-block.float-sm-right`. URL pattern: `/trending/python?since=daily`.
- **GitHub README**: Use `#readme article.markdown-body` to select README content. First section is content before the second `H1`/`H2`.

## Pending Items
<!-- Items to follow up on -->
