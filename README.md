# Courtisans Scorer

A small, single-page scoring helper for the card game *Courtisans*. Set each family's standing at the Queen's table, tap the cards in your domain, tick off your secret missions, and it adds up your score.

## Features

- One column per family in the order they sit at the Queen's table: Butterfly, Toad, Nightingale, Hare, Stag and Carp
- A standing toggle for each family: esteemed, neutral or fallen from grace
- One tile for every card in the deck, grouped by role: 4 nobles, 4 courtiers, 3 guards, 2 assassins and 2 spies per family
- Per-family working shown under each column, e.g. `5 × +1`
- White and blue secret mission toggles, worth +3 each
- Running total in a sticky bar, with a Clear button
- The current game is saved in the browser (`localStorage`), so a refresh doesn't lose it
- Light and dark themes follow the system setting
- Selected states use outline style and stripes as well as colour, so they don't rely on colour alone
- No build step, no dependencies: one HTML file plus self-hosted fonts in `fonts/`, so no third-party requests

## Scoring rules

1. Reveal all spies. Spies at the Queen's table move to their family, staying above or below the mat.
2. For each family, compare the cards above and below the mat. Nobles count as two cards.
   - More above: the family is **esteemed**.
   - More below: the family is **fallen from grace**.
   - Equal: the family is **neutral**.
3. Each card in your domain scores +1 if its family is esteemed, −1 if fallen from grace, and 0 if neutral. Nobles count double.
4. Each secret mission you fulfilled is worth +3.

## Running locally

Open `index.html` in a browser. That's it.

## Deploying to GitHub Pages

1. Push this repository to GitHub.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, select `main` and `/ (root)`, and save.
4. The site will be published at `https://<username>.github.io/<repo-name>/` after a minute or two.

The empty `.nojekyll` file tells GitHub Pages to serve the files as they are, without running them through Jekyll.

## Privacy

Your game is saved only in your browser's `localStorage`. Nothing is sent anywhere: there are no cookies, analytics or third-party requests. The site is hosted on GitHub Pages, which logs visitors' IP addresses under [GitHub's privacy statement](https://docs.github.com/en/site-policy/privacy-policies/github-general-privacy-statement).

## Credits

*Courtisans* is published by Catch Up Games. This is an unofficial fan-made tool and is not affiliated with or endorsed by the game's designers or publishers.

Typefaces: [Gloock](https://github.com/duartp/gloock) by Duarte Pires and [Alegreya Sans / Alegreya Sans SC](https://github.com/huertatipografica/Alegreya-Sans) by Huerta Tipográfica, both under the SIL Open Font License 1.1 (see [`fonts/OFL.txt`](fonts/OFL.txt)).

## License

The code is released under the [MIT License](LICENSE). The fonts are under their own license, as above.

## Support

If you find this useful, you can [buy me a coffee](https://buymeacoffee.com/mairuzu).
