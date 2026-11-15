# Project proposal

**Due Monday 16 November, 09:00.** Push this file together with `notebooks/00_first_look.ipynb`.

## Group

| name | GitHub username |
|---|---|
|Peter Vajda |peteravajda-gif |
| | |
| | |
| | |

## Question

What do you want to find out?

From which online marketplaces should you buy your next iPhone in Germany?

## Sources

| source | link | API, file or web page |
|---|---|---|
| Kleinanzeigen Agent – second-hand iPhone listings | [API documentation](https://kleinanzeigen-agent.de/dokumentation) | API |
| eBay Germany | [Example listings](https://www.ebay.de/b/Apple-iPhone-13-128GB/9355/bn_7117856204) | Web page |
| Quoka Germany | [Example listings](https://www.quoka.de/anzeigen/?commercial=false&q=iphone+13) | Web page |


## Joining the sources

What do your sources have in common that you can join them on? It could be a date, a country code or a place.

We will join the three sources on iPhone model and storage capacity. For example, an iPhone 15 with 256 GB of storage is the same configuration on Kleinanzeigen, eBay, and Quoka. We will standardize model names and storage units, calculate the mean and median asking price for each configuration on each platform, and then join those summaries to compare prices side by side.