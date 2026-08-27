# saturn2022-paper

Working paper: **Deviation-threshold oracles are volatility instruments.**

## Abstract

A price oracle that publishes on deviation rather than on a schedule records,
in its update times alone, the volatility of the asset it tracks. Nothing else
about the oracle is needed, and the prices it publishes need never be read.
Chainlink's deviation-triggered feeds publish a new round the moment the
underlying price has moved by a fixed proportion. The mean interval between
those rounds is a passage time, and Cho and Frees (1988) show that the
annualized volatility of a diffusion crossing a barrier of width `d` in
expected time `T` is `d * sqrt(year / T)`. This paper measures that estimator
against the realized volatility of the same price series across eighteen live
feeds and finds a stable proportionality constant of 0.915, with a coefficient
of variation of 3.8% across assets. The estimator therefore reads a real
market number off records the chain already keeps, at zero storage cost and
zero calls to any external service.

## What is in this repository

- **[OUTLINE.md](OUTLINE.md)** - a working outline. What is claimed, why it
  matters, what the sections need to prove.
- **[PAPER.md](PAPER.md)** - the working draft. Longer, closer to the final
  shape.

## What the paper depends on

Every figure cited in the paper is produced by a script in the sibling
repository [saturn2022-tools](https://github.com/Saturn2022Fi/saturn2022-tools).
Those scripts read Robinhood Chain directly, print a table, and take no
arguments. A reader who disagrees with a number runs the script that produced
it. The full round-history dataset the estimators walk is
[out/rounds.json](https://github.com/Saturn2022Fi/saturn2022-tools/blob/main/out/rounds.json)
in the same repository.

## Where the paper is used

The saturn2022 protocol uses the estimator to price options on chain. The
implementation is
[FeedVol.sol](https://github.com/Saturn2022Fi/saturn2022/blob/main/contracts/src/FeedVol.sol)
in the main repository. The paper's proportionality constant is compiled into
that contract as the calibration divisor.

## Citation

If you build on this, please cite:

> Cho, D. C., and Frees, E. W. "Estimating the volatility of discrete stock
> prices." Journal of Finance 43, no. 2 (1988): 451-466.

and this working paper.

## Status

Draft. The estimator itself has been validated across eighteen live feeds and
is production on chain; the paper's narrative and figures are the piece still
being tightened.
