```text
HANDOFF
turns: 37
session length: short requested; extended into coding review
learns by: mixed definitions, examples, analogies, contrasts, and applications
preferred pace: compact explanations with meaningful checks; avoid repeatedly requesting the same pending integration check

domain: point processes | level: 3 | milestone: 2 reached | anchor: marginal intensity
marginal intensity | claim: no | prior: none | end: deployed | "if the marginal intensity remains similar at each time"
other deployed: event time, inter-arrival time, counts, mean, variance, emission function
other open: intensity surface, point process, counting process, Poisson process, independent increments, memoryless, Fano factor, overdispersion, intensity function, compensator, thinning, time-rescaling theorem
Progress: Explained how latitude predictions can improve while timing KS remains nearly unchanged. Correctly connected analytic peak normalization to peak belt strength and the thinning bound.

domain: statistical inference | level: 3 | milestone: 2 reached | anchor: overfitting
ablation | claim: no | prior: none | end: deployed | "Alongside the baseline and my asymmetric-profile ablation, that makes four models"
leaderboard | claim: no | prior: none | end: deployed | "I’d treat the resulting leaderboard as provisional"
generalization | claim: no | prior: none | end: deployed | "potentially reducing generalization even if the width rule fits the training data better"
overfitting | claim: no | prior: none | end: introduced | "no quote"
metric gaming | claim: no | prior: none | end: introduced | "no quote"
model selection | claim: no | prior: none | end: deployed | "For model selection, I’d fit them jointly and measure the combined held-out gain."
other deployed: log-likelihood, held-out log-likelihood, quadrature mesh, latent variable, paired differences, standard error, mean, variance, analytic normalization
other open: gauge freedom, partial pooling, leave-one-cycle-out cross-validation, negative log-likelihood, Earth Mover's Distance, null model, standard deviation, smoothing width, robust, integral term, observation window, fit, mesh refinement, maximum likelihood estimate, quadrature, unconstrained parameterization, QQ plot, Kolmogorov–Smirnov statistic, identifiability, profile likelihood, candidate, attribute, compare, jump size
Progress:
- Declared experiments and predictions before scoring.
- Proposed paired held-out comparisons and a one-standard-error decision rule.
- Explained optimism from selecting many models on the same development folds.
- Explained how predicted-strength errors can become width errors.
- Constructed two metric-gaming mechanisms: coarse quadrature and favorable scoring-window selection.
- Distinguished useful conditional bounds from ranked predictions.
- Explained overlapping versus complementary gains from jointly fitted knobs.
- Correctly explained why even one per-wing shape parameter makes a row conditional under this protocol.

domain: solar cycle physics | level: 3 | milestone: 2 reached | anchor: hemispheric asymmetry
hemispheric asymmetry | claim: no | prior: none | end: deployed | "That could capture hemispheric asymmetry"
other deployed: buoyancy threshold, drift track, belt width
other open: emergence, hemispheric cycle, alignment coordinate, emergence rate, onset
Progress: Distinguished north–south size differences from shape differences. Recognized that strength can change observed spread through the threshold even when underlying shape parameters are shared. Distinguished observed-event asymmetry from evidence of actual magnetic-field asymmetry.

REQUIRED OWN KNOB — COMPLETED
Stage: latitude profile.
One shared training-fitted parameter q.
Poleward width: w * exp(q).
Equatorward width: w * exp(-q).
q = 0 reproduces the baseline exactly.
Question: Does unequal poleward/equatorward spread improve held-out predictions?
Prediction: Positive held-out log-likelihood gain; no directional prediction for q.
Held-out rule: Freeze q at the training-fold estimate.
Physical limitation: Better event predictions do not uniquely identify the underlying magnetic-field geometry.

DECLARED MENU
1. Baseline.
2. Asymmetric latitude profile.
3. Amplitude-dependent width.
4. Threshold-free emission.
Each variant differs from baseline in one feature.
Predictions: positive gains for asymmetry and amplitude-dependent width; a tie for removing the threshold.
Estimate runtime before running each menu or additional candidate.
Decision rule: compare paired hemicycle differences on identical scoring settings; apply the notebook's one-standard-error tie rule.
Combined candidates require joint fitting and cannot attribute their gain to one knob.

IMPLEMENTATION AND REVIEW
Latest reviewed attachment: 04_scoreboard1 (1).ipynb.
Tasks 32–43 are implemented.
All 63 code cells have saved executions without error outputs.
Tutor reviewed all code and saved results and ran focused checks; tutor did not independently rerun the entire experiment menu.
Task 32 formulas and normalization passed focused checks.
Task 33 assignments and plotting helper passed focused checks.
Task 34 equal-slope identity and nonpositive-width rejection passed focused checks.
The asymmetric profile reproduced the baseline exactly at q=0 across the full mesh, and nonzero-q thinning-bound checks passed.

SAVED RESULTS — PROVISIONAL
Domain: s in [-6, +11] years; absolute latitude in [0, 60] degrees; frozen 201-by-241 mesh.
Selected candidate: asymmetric profile plus amplitude-dependent width, retaining threshold emission.
Saved paired gain over baseline: approximately 0.922 ± 0.318 nats per hemicycle-year; better in 16 of 18 wings.
Threshold removal was reverted as a tie.
Timing KS changed little.
These results require regeneration after addressing the initialization concern below.

OUTSTANDING REVIEW FINDINGS
1. Fold initialization:
   run_variant supplies all-data fitted parameters and amplitudes as fold starting values.
   Only two optimization sweeps are used.
   In an independent baseline fold-12 comparison, changing to fixed starts changed 12N's NLL by about 0.106 nats per hemicycle-year on the same fixed domain.
   Use fixed or training-only initialization, or demonstrate convergence independent of initialization. Invalidate affected caches and regenerate results.
   This warm-start pattern originates in the supplied runner.
2. Report identity:
   The saved report identifies the student as Codex.
   Set BUTTERFLAI_STUDENT to the submitting student's name and regenerate the identity/report cells.
3. Diagnostic interpretation:
   The per-wing-growth diagnostic refits a different pooling model.
   Its gain includes both a changed training model and conditioning on scored events.
   Revised Markdown acknowledges this, but printed text still incorrectly claims no training predictions changed. Make the explanations consistent.

FIXED CONVENTIONS
- s is a shift in years since the fitted 15-degree crossing, never a rescaling.
- Event time means first observation, not actual emergence.
- Hold mesh, latitude domain, time window, and scoring protocol fixed.
- Do not compare raw 1D and 2D likelihood scores.
- B_crit = 1 and alpha = 1 are fixed; c is global.
- Headline amplitude comes from the area record through a training-fold relationship.
- Held-out alignment uses its own events with the training drift timescale; this is retrospective evaluation, not a forecast before observations.
- Per-wing shape fits are unranked bounds.
- Keep timing KS and held-out likelihood separate.
- Cycles 16, 20, and 22 remain sealed.
- Development ranking remains provisional after model selection.

NEXT
Address the three review findings, regenerate affected caches/results, then interpret whether the selected gain survives training-only initialization and remains larger than its paired uncertainty.
```

Use this latest HANDOFF next session. Save it as `vocal_handoff.md` if your educator collects it.
