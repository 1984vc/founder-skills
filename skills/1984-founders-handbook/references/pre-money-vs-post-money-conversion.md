---
title: Pre-money vs Post-money Conversion
weight: 3
description: ""
Category: Raising Your Seed
Icon: presentation-line-chart
draft: false
authors:
  - Ramy Adeeb
---

*Source: [Pre-money vs Post-money Conversion](https://1984.vc/docs/founders-handbook/pre-money-vs-post-money-conversion)*


In 2018 YC replaced the original Pre-money safe (where investors and company agree on the  *pre-money*  valuation) with the Post-money safe (where investors and company agree on the  *post-money*  valuation the safe converts). The key difference between the two conversion methods is around calculating the ownership being sold in an investment:

- If an investor and company agree on a  **pre-money**  valuation, then an investor's ownership is a function of their investment, the pre-money valuation  *and*  the size of round (and all other rounds until conversion).
- But if an investor and company agree on a  **post-money**  valuation, then an investor's ownership is a function of their investment and the post-money valuation  *irrespective*  of the round size or any other rounds taking place until conversion.
For a company raising just one SAFE round, there's effectively no difference: an investor who invests $2M on $8M  *pre* -money is presumably willing to invest $2M on $10M  *post* -money, with the same resulting ownership of 20%. But things are different when multiple SAFE rounds are involved. Let's look at two examples

## Conversion on a Pre-money Basis


Consider a company that's in the example above.  The company first issues a $2M SAFE  converting on a pre-money basis.  The company cap table looks as follows

| Column 1 | Column 2 | Column 3 | Column 4 | Column 5 | Column 6 |
| --- | --- | --- | --- | --- | --- |
|   | Starting ownership (shares) | Starting ownership (%) | First Safe Round | Ownership after everything converts (shares) | Ownership after everything converts (%) |
| Founder A | 1,000,000 | 50% |   | 1,000,000 | 40% |
| Founder B | 1,000,000 | 50% |   | 1,000,000 | 40% |
| Seed Investor |   |   | The right to buy 2/(8+2) = 20% of equity | 500,000 | 20% |
|   | 2,000,000 | 100% |   | 2,500,000 | 100% |


Now the same company decides to raise an additional $2M on the same terms a year later from Seed Investor 2. Under the pre-money conversion, the company will have effectively raised two different $2M notes on $8M pre-money, so effectively $4M on $8M pre/$12M post, with Investors owning 33.33% and founders 66.66%.  Basically, in a pre-money conversion, investors dilute each other in addition to diluting existing shareholders.

| Column 1 | Column 2 | Column 3 | Column 4 | Column 5 | Column 6 | Column 7 |
| --- | --- | --- | --- | --- | --- | --- |
|   | Starting ownership (shares) | Starting ownership (%) | First Safe Round | Second Safe Round | Ownership after everything converts (shares) | Ownership after everything converts (%) |
| Founder A | 1,000,000 | 50% |   |   | 1,000,000 | 33.33% |
| Founder B | 1,000,000 | 50% |   |   | 1,000,000 | 33.33% |
| Seed Investor 1 |   |   | The right to buy 2/(8+2) = 20% of equity | The right has now changed to be 2/(8+2+2) = 16.66% | 500,000 | 16.66% |
| Seed Investor 2 |   |   |   | The right to buy 2/(8+2+2) = 16.66% of equity | 500,000 | 16.66% |
|   | 2,000,000 | 100% |   |   | 3,000,000 | 100% |


Cap Table Example

Here's the mechanics of what actually happens:

- Initially, investor 1 bought the right to buy $2M of equity on $8M pre (or $10M post)
- Then Investor 2 got the right to buy $2M of equity on $8M pre. But the company is now valued at $12M post. So Investor 2 gets 2/12 = 16.66%. Additionally, investor 1's ownership is getting diluted by Investor 2's 16.66%. So now their ownership is 20% * (1-0.1666) = 16.66%
The dilution keeps going on as the company raises additional convertible or SAFE rounds until the first priced rounds takes place. And the math is recursive—getting a bit more complicated with each round.  And that's why investors and founders demanded a better mechanism.

## Conversion on a Post-money Basis


Let's take the same example but where investors agree on the post-money valuation. Under this scenario, each investor will have invested $2M on $10M post for a 20% ownership. The company will have effectively raised $4M on $10M post with investors owning 40% and founders 60%. Why the difference? Because in post-money agreement, the second SAFE investor dilutes the existing shareholders but do not dilute the first SAFE holders since the agreement is on the post-money not the pre-money.

| Column 1 | Column 2 | Column 3 | Column 4 | Column 5 | Column 6 | Column 7 |
| --- | --- | --- | --- | --- | --- | --- |
|   | Starting ownership (shares) | Starting ownership (%) | First Safe Round | Second Safe Round | Ownership after everything converts (shares) | Ownership after everything converts (%) |
| Founder A | 1,000,000 | 50% |   |   | 1,000,000 | 30% |
| Founder B | 1,000,000 | 50% |   |   | 1,000,000 | 30% |
| Seed Investor 1 |   |   | The right to buy $2M/$10M = 20% of equity |   | 666,666 | 20% |
| Seed Investor 2 |   |   |   | The right to buy $2M/$10M = 20% of equity | 666,666 | 20% |
|   | 2,000,000 | 100% |   |   | 3,333,333 | 100% |


## Conclusion


Post-money conversion offers investors and founders clarity on their respective ownership before priced round occurs, while pre-money conversion provides more favorable dilution to founders across multiple rounds. That said, that ship has largely sailed. In recent years, pre-money SAFEs and convertible rounds have virtually disappeared, with post-money SAFEs now dominating over 95% of Silicon Valley financing.

[Suggested Reading: Safe vs Priced Rounds](/docs/founders-handbook/safe-vs-priced-round/)
