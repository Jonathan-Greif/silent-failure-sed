# Silent Failure in Semi-Supervised Sound Event Detection: Synthetic Validation Can Hide Real-World Collapse

**Jonathan Greif<sup>1</sup>, Florian Schmid<sup>1</sup>, Gerhard Widmer<sup>1,2</sup>**

<sup>1</sup> Institute of Computational Perception (CP-JKU), <sup>2</sup> LIT Artificial Intelligence Lab, Johannes Kepler University Linz, Austria

DCASE 2026 Workshop, Boston, MA, USA (Poster P3-10)

> **Status: code release in progress.** The code and the list of AudioSet-overlap-free test clips will be released here shortly after the DCASE 2026 Workshop.
> Watch or star the repository to get notified when they are available.

## TL;DR

Under the classical DCASE Task 4 protocol, models are selected on synthetic validation data plus a small weakly labeled real subset. We show that both signals can certify sound event detection models that have silently collapsed on real recordings. Mean Teacher fails in two geometric modes; replacing it with FlatMatch avoids both. Flatness-aware training acts as insurance against silent failure, not as a universal performance booster.

## Key findings

- **Silent failure.** On a 3M-parameter pretrained MobileNet, Mean Teacher reaches at most 0.33 PSDS1 on real recordings and 4 of 12 seeds collapse to zero, while synthetic validation and the weakly labeled real subset look unremarkable.
- **Two failure modes, one post-hoc signature.** Failing runs end either in sharp minima with elevated real-domain curvature or on flat plateaus with elevated real-domain loss. In every failing run, the supervised loss on real audio exceeds the one on synthetic audio. This signature needs frame-level real labels, so it is a post-hoc diagnostic, not a monitor: no quantity we examined that is computable without such labels separates failing from healthy runs.
- **What breaks is temporal localization.** Failing models still recognize which events occur, but no longer when.
- **Not specific to Mean Teacher.** In a seed-paired supervised-only control, half of the sharp-mode collapses persist without the Mean Teacher term; the term widens the instability.
- **FlatMatch avoids both failure modes.** On the same MobileNet it reaches 0.46 PSDS1, within 0.04 of a CRNN+BEATs baseline with about 30 times more parameters. FlatMatch outperforms Mean Teacher on the recurrence-free MobileNets and the transformer, while Mean Teacher stays ahead on every recurrent configuration.

## Release status

- [ ] Training and evaluation code (Mean Teacher and FlatMatch on DESED, classical DCASE Task 4 protocol)
- [ ] List of AudioSet-overlap-free clips of the DESED real validation set

## Note on AudioSet overlap

Some recordings of the DESED real validation set (used as our real test set, 1,168 clips) are drawn from AudioSet and therefore overlap with the pretraining data of our backbones. The paper reports results on the full set; the list of overlap-free clips will be provided in this repository.

## Citation

The paper link follows with the DCASE 2026 proceedings.

```bibtex
@inproceedings{greif2026silent,
  author    = {Greif, Jonathan and Schmid, Florian and Widmer, Gerhard},
  title     = {Silent Failure in Semi-Supervised Sound Event Detection: Synthetic Validation Can Hide Real-World Collapse},
  booktitle = {Proceedings of the Detection and Classification of Acoustic Scenes and Events 2026 Workshop (DCASE2026)},
  address   = {Boston, MA, USA},
  year      = {2026}
}
```

## Acknowledgements

This work is supported by the European Research Council (ERC) under the EU's Horizon 2020 research and innovation programme, grant agreement No. 101019375 (Whither Music?), and the Federal State of Upper Austria (LIT AI Lab).

## Contact

For questions, please open an issue in this repository.
