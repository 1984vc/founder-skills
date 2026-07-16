---
title: Cap Table 101
weight: 1
description: ""
Category: Company Formation
Icon: calculator
draft: false
authors:
  - Ramy Adeeb
---

*Source: [Cap Table 101](https://1984.vc/docs/founders-handbook/cap-table-101)*


To most founders, cap table math can be bewildering. It's unintuitive, highly recursive, and has little parallel in traditional finance training. Fortunately, it's easy to learn. And founders who master their cap tables gain an unfair advantage in negotiations. Our goal from this guide is to equip founders with the [tools](/docs/cap-table-worksheet) and knowledge to master their cap table and outperform their counterparts in any financing negotiation.

The cap table has exactly 100 points—no more, no less. When new shares are granted to employees or investors, the resulting ownership must come from elsewhere in the cap table. That's why while first time founders focus on  *valuation* , more experienced founders care about  *ownership.*  To bring this point home, most of the examples in this guide use percentage points to help founders understand the tradeoffs.

## Raising your seed round


Let's start with a simple example. Two founders start a company, granting themselves 1M shares each and splitting the cap table 50/50. Following, A VC investor would like to buy 20% of the company.  The founders and investors agree on a $2 million investment at a valuation of $8M pre-money, $10M post-money.

> 📢  **Pre-money**  and  **Post-money**  describe the valuation of a company at two different points in time:  **before**  and  **after**  the financing round.  A company valued at X before the investment and receiving Y in investment will have a pre-money valuation of X and a post money valuation of (X + Y).


Now for this example let's assume a priced round which is more straightforward to model than a SAFE. The mechanics for issuing a priced round works as follows:

1. First, we calculate the Pre-money capitalization, which is the number of shares in the business before the round takes place. In this case it's the 2M shares held by the founders.
1. Next, we calculate the Price Per Share, which is equal to the pre-money valuation (what the company is worth before the investment) divided by Pre-money Capitalization. In this case the PPS will be 8,000,000 (dollars) / 2,000,000 (shares)= $4
1. Last we calculate the number of new shares being issued to the investor based on their purchase price. In this case the investor is investing $2M into the company at a price per share of $4 resulting in $2,000,000/$4 = 500,000 new shares.
> 📢 The Price Per Share ( **PPS** ) in a round can be calculated as the pre-money valuation divided by number of shares (often called Company Capitalization).


This investment will result in the following a cap table.

| Column 1 | Column 2 | Column 3 | Column 4 | Column 5 | Column 6 |
| --- | --- | --- | --- | --- | --- |
|   | Starting ownership (shares) | Starting ownership (%) | New Shares | Ownership after Investment (shares) | Ownership after Investment (%) |
| Founder A | 1,000,000 | 50% |   | 1,000,000 | 40% |
| Founder B | 1,000,000 | 50% |   | 1,000,000 | 40% |
| Seed Investor |   |   | 500,000 | 500,000 | 20% |
|   | 2,000,000 | 100% |   | 2,500,000 | 100% |


[ *Link to Cap Table* ](/docs/cap-table-worksheet/#AAN4IgDgTgpgsg9gOygTxALgBwAYe4DQgAuAhhAOZSEDyYhAlogM4AKccANulgQK4I.MoAExr0mXAhDgB3ACLES6ANqg6Q9CACcIAoWRgoGgMZwAtqcQ6QCYqcNoQAMTh8hUCAAIAglcYALUihGdABGXHwQGSQIfzowZVB_QOC0MPDucHcjKARCdAAmAGYAOnyAVjKMEMLNMsKAFgwMQoB2AncpCHQAM2J2QQBfPESA6BS08IIDCGzcgpDigDZ8ls0QkMWsevWsfPqy9ohOnr7B4ZAksdD0jOnZvNSMYo2W.vqV1Yx87_zD47Rev0oAMALoEPrsGSyKDsSj2QgQHjA85qDRhKx6AzGMwWBBWGx2DTOVzuDwAIV8oyC13SBCi7li8TQKguVPGNymWRyDzKGQ6cC6ANOyJGyRpk0yM256Hqi2KvJwITqb00mhaNXqfwFJyBQ1FV1SHMl93QNWKWDKqrVLRCTU0i2qBxA_MFgMGYJAEKhMLh6ARSL1IFRDgAkoxGEiRLQGAhgrp9PYQCZzJYCATE2GI8IPKIY3HWWK0Bl6TE_HEEgWDbcuXMi1rXcLA5dqXXjdLWy6dWd9S3q1La3yjtqhbqPV65D7CPDESKg.oHBsMQmNIIIHRqWnbImAMpQbMhhAANyChG1BDoR5Pdlr.SNJcZFebKQVETu7dvoPB7EhE9hU67wIepAdDZEIABKLgIEI4wDEAA)

Now the post-money valuation is simply the pre-money plus the investment amount = $2M + $8M = $10M.  A more accurate post-money definition is the final number of shares, called fully diluted shares or FDS, multiplied by the PPS, which in this case comes out 2.5M shares * $4 = $10M.

The new investment  *dilutes*  the existing ownership for each founder from by 20% from 50% starting ownership to 40% after.

> 📢 In cap table lexicon,  **Dilution**  is the percentage reduction in ownership from a round. It is calculated as the number of new shares being issued from the transaction divided by the fully diluted shares after the transaction. So, in this case, 500,000/2,500,000=20%,  A founder who starts at 50% will experiences a 20% dilution will end up with 50% * 0.8  = 40%.


Now depending on whether the round was a SAFE or a priced round the shares will be issued immediately or promised in the future, but the effect is largely the same [with a few differences](/docs/founders-handbook/safe-vs-priced-round/) that we will discuss in the next chapter.

## Option Pool


To understand why option pools exist, it is helpful to first show what happens  *without*  an option pool. After the investment, the founders identify their first engineer and decide to offer them 5% ownership. Assuming there's no pool, the company asks the board to issue 131,578 new shares to the employee or 5% of the total shares. Once granted, the new shares would dilute everyone's ownership equally.

| Column 1 | Column 2 | Column 3 | Column 4 | Column 5 | Column 6 |
| --- | --- | --- | --- | --- | --- |
|   | Ownership after Investment (shares) | Ownership after Investment (%) | New employee shares | Ownership after employee joins (shares) | Ownership after employee joins (%) |
| Founder A | 1,000,000 | 40% |   | 1,000,000 | 38.00% |
| Founder B | 1,000,000 | 40% |   | 1,000,000 | 38.00% |
| Seed Investor | 500,000 | 20% |   | 500,000 | 19.00% |
| Employee |   |   | 131,578 | 131,578 | 5.00% |
|   | 2,500,000 | 100% |   | 2,631,578 | 100% |


Now the investors' ownership has been diluted from 20% to 19%. However, investors do not expect to be diluted with each new employee hire. To address this, investors in a priced round typically request a reserved option pool—often around 10%—as part of the round. When new employees join, their shares are allocated from this option pool, avoiding further dilution of the investors' stake (and avoiding the hassle of issuing new set of shares). So assuming the investors demand an option pool in the round, the ownership structure becomes 20% for the investor, 10% for the reserved option pool, and 35% for each founder.

| Column 1 | Column 2 | Column 3 | Column 4 | Column 5 | Column 6 |
| --- | --- | --- | --- | --- | --- |
|   | Starting ownership (shares) | Starting ownership (%) | New Shares | Ownership after Seed Investment (shares) | Ownership after Seed Investment (%) |
| Founder A | 1,000,000 | 50% |   | 1,000,000 | 35% |
| Founder B | 1,000,000 | 50% |   | 1,000,000 | 35% |
| Seed Investor |   |   | 571,428 | 571,426 | 20% |
| Option Pool |   |   | 285,714 | 285,714 | 10% |
| Employee |   |   |   |   |   |
|   |   | 100% |   | 2,857,142 | 100% |


[ *Link to Cap Table* ](/docs/cap-table-worksheet/#AAN4IgTg9g7gIghgFziAXAbVASwCapABhABoQEBPABwFM8BjCAWwYgDtiQW4GaUQAxCAFcW2KmADOAAgCC7cQAs4YKuNQBGfJq0loLMQswVUGEAqUr1W7SGphaVFgnUBWAHQBmABwAWAGxrnLz8Ar2cAXyJQM2VVFA0rfBJbe0d1NVcAJmdvb3cAdk9fAE5PDIzvTzyIqMUYywSksRSnFE9XPLy1QucinrKArLCAXRI4ABsx6BgqMaoEHgQwQSpqkBw8NXZyajpGZjYSTm48AWFRMEkAITlaiziExJBdfXlDYxrzWPirRrsHFvc7g8gJBoNBq2id2.1mS_1Q5Q8Pn8gSRIU8ENuXwev2a6iKrk8pWKGTUal8zjUWTyvmGowmUxmcwWSxWkTWuF4AElxOJltgAPIUBCYViqEjbHggehMVjsI6S7m8qjYSSC4Wim6fVCPZ4SV5GdAfOooR6w1ImjFak04uEWtmQ2Kmpq2_C0kDjSawRnzVCLZarda8PJbSiS8RiTAWQ5cSUAZQjKhkkk5LAAbioEBAwOxMGmM9xzRlsU8oHo9W9DaZMahnJ1vBlPDbzWp8UU2yUeu3euiRu76V7Zj6UAAzcbht0UZQAWVYVDIqE8xaQYAA5nM1SKWOIAAoQCBjSwkYSCcMCoWbx1hIA)

Following, in order to grant 5% to the new employee, these shares are moved from the option pool to the employee as opposed to getting issued.  The other shareholder's ownership would thus remain at 20%.

| Column 1 | Column 2 | Column 3 | Column 4 | Column 5 | Column 6 |
| --- | --- | --- | --- | --- | --- |
|   | Ownership after Seed Investment (shares) | Ownership after Seed Investment (%) | Employee Grant | Ownership after employee grant (shares) | Ownership after employee grant (%) |
| Founder A | 1,000,000 | 35% |   | 1,000,000 | 35% |
| Founder B | 1,000,000 | 35% |   | 1,000,000 | 35% |
| Seed Investor | 571,428 | 20% |   | 571,428 | 20% |
| Option Pool | 285,714 | 10% | (142,857) | 142,857 | 5% |
| Employee |   |   | 142,857 | 142,857 | 5% |
|   | 2,857,142 | 100% |   | 2,857,142 | 100% |


> 📢 Founders often mistakenly assume that the new employee shares are granted at the time of the offer letter. But they're actually not granted until much later because these shares require board approval, which typically occurs during the first board meeting after the employee joins the company. This delay can impact the price of the shares or options being granted.


Note that if the company is acquired before exhausting all unissued options, these options are effectively wiped off and everyone's ownership increases by 5%

Until the mid-2000s, priced rounds like the example above were the primary way founders raised capital. Then came convertible notes, and then came [SAFEs](/docs/founders-handbook/intro-to-safes/).

 ***The Usual Disclaimer -***  *The information in this User Guide is provided solely for general educational purposes and is not intended as legal advice. This User Guide should not replace competent legal counsel from a licensed attorney in your state.1984 and its affiliates expressly disclaim all responsibility for any consequences resulting from the use of this User Guide, any version of the Cap Table Worksheet, or any other document found on 1984's website.* 

 *We value your input! If you'd like to report bugs, provide feedback, or suggest improvements, please email* [ *team@1984.vc* ](mailto:team@1984.vc)
