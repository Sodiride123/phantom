# Phantom Memory

## Session Log
- **2026-04-23**: Amazon mechanical keyboard search task. Searched for "mechanical keyboard", filtered 4★+ and under $100, sorted by Avg Customer Review. 3rd result: My Little Pony Wireless Mechanical Keyboard ($75.99, 5.0 stars). Posted results + screenshot to Slack.
- **2026-04-23**: GitHub Trending Python repos task. Extracted top 5 trending repos, navigated to #1 (FinceptTerminal), summarized README first section. Posted to Slack with screenshot.
- **2026-04-23**: OpenTable Italian SF task. OpenTable fully blocked by Akamai (IP-level). Used Tavily research + Cafe Tiramisu's own website for menu. Posted results + menu screenshot.
- **2026-04-23**: Booking.com Tokyo hotel search. Filters: 4+5 star, free cancellation, sorted Top Reviewed. Top result: Agora Tokyo Ginza ($258/night, 8.4 score). Posted results + amenities screenshot.
- **2026-04-23**: LinkedIn Jobs ML engineer SF search. Extracted 3 jobs with salary, experience, skills. Not logged in but public job pages accessible. Posted to Slack.

## Technical Decisions
- **Amazon search filters via URL params**: More reliable than clicking UI filters. `p_72:1248879011` = 4★+, `p_36:-10000` = under $100 (cents), `s=review-rank` = sort by avg review.
- **ASIN-based navigation**: When JS click doesn't navigate (Amazon ad-tracking links block), extract `data-asin` attribute from search result elements and navigate to `/dp/{ASIN}` directly.
- **Product data extraction selectors**: `#productTitle` for title, `.a-price .a-offscreen` for price, `#acrPopover .a-icon-alt` for rating, `#acrCustomerReviewText` for review count.

## Site-Specific Notes
- **GitHub Trending**: Repo rows use `article.Box-row` selector. Name in `h2 a`, description in `p`, daily stars in `span.d-inline-block.float-sm-right`. URL pattern: `/trending/python?since=daily`.
- **GitHub README**: Use `#readme article.markdown-body` to select README content. First section is content before the second `H1`/`H2`.

- **Booking.com search flow**: Homepage accepts destination + dates interactively. Filters (star rating, free cancellation) must be clicked via `input[type="checkbox"]` in sidebar — URL param approach with `nflt` doesn't reliably work on initial load. Sort by "Top reviewed" = click sort dropdown then option. Hotel cards use `[data-testid="property-card"]`, titles in `[data-testid="title"]`, prices in `[data-testid="price-and-discounted-price"]`, scores in `[data-testid="review-score"]`. Date cells selectable via `[data-date="YYYY-MM-DD"]`.

- **LinkedIn Jobs (public)**: Search URL pattern: `/jobs/search/?keywords=X&location=Y&f_TPR=r86400&f_AL=true` (f_TPR=r86400 = past 24h, f_AL=true = Easy Apply). Job cards use `.base-card` or `a.base-card__full-link`. Individual job pages at `/jobs/view/slug-ID` show full descriptions publicly. Salary often in description text. Not logged in — no session cookies.

## Blocked Sites
- **OpenTable.com**: Fully blocked by Akamai bot detection (IP-level). Browser restart, cookie clear, Google click-through all fail. Use Tavily search/extract as fallback + restaurant's own website for menus.

## Pending Items
<!-- Items to follow up on -->
