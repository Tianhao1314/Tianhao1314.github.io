# Toward Multimodal Predictive Systems for Action-Time Prediction

*Self-directed reflection — building on the tele-impedance study, 2026.*

A self-directed design-space study on sEMG-driven impedance prediction left
me with a question I keep returning to. The technical part went smoothly:
architectural priors — attention mechanisms, physics-informed losses,
multi-modal feature fusion — measurably improved how well a sequence model
could predict an operator's future trajectory and stiffness. The LSTM
variants reached millimeter-level error 100–200 ms ahead on a synthetic
peg-in-hole task; ablation showed the priors stack non-linearly (helping
LSTM by ~11 % while hurting GRU by ~32 %), and MC-Dropout uncertainty
separated confident predictions from uncertain ones cleanly enough to gate
downstream decisions.

The unsettling observation was about what comes *next*. Even with a model
that demonstrably predicts well, a real teleoperation deployment cannot
trust the prediction outright. It needs a classical, mathematically
tractable safety controller — an energy observer, a passivity filter,
something with a proof — to catch the case the learned model gets wrong.
The fallback exists not because the prediction is bad, but because the
model is opaque: no one knows how to be accountable for what a black-box
network *would do* in a situation no one has thought through. We end up
holding ourselves back from the better-performing tool because the more
honest tool can sign its own work.

Causality as a fix — encoding what the model is "allowed" to infer — feels
structurally wrong to me. The world is too rich to specify edge case by
edge case; every constraint we add is one more piece of brittle scaffolding.
The direction that pulls me — and I want to be honest, it is an area I am
only beginning to read into — is **multimodal predictive systems** where
the model's belief about the future is itself a *physically grounded,
observable, checkable artefact*. If the predicted next half-second unfolds
in 3D under learned physics — rather than as a 6-dimensional vector emitted
from a hidden state — then "is this prediction safe to act on?" can be
answered by inspecting the prediction itself, not by bolting an external
filter onto it.

That reframing changes the problem from "make the AI prediction more
interpretable" to "make the AI's *future* the thing we inspect". I do not
pretend to know which architectural family — diffusion priors, video
transformers, learned simulators, neural physics — does this best, or even
whether the framing survives contact with a real dataset. But that is
exactly why it is the direction I want to spend the next phase exploring.
