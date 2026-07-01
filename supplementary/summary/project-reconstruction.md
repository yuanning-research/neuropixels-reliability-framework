# Problem
cross-session neurons alignment is difficult since electrode drifts, physiological changes etc. we want to determine the same neuron across days/sessions.
if we cannot reliably identify the same neuron across sessions, it becomes difficult to study long-term neural dynamics, stability, or plasticity.
# exsiting method
unitmatch with bombcell
> kilosort outputs were processed with Bombcell for quality metrics/control and then used by Unimatch to generate cross-session candidate matches and MatchProb.
unitmatch provides a systematic probabilistic framework for proposing cross-session matches. we can have a model-derived probability, from baiyse model(combining 6 features representing neurons well). 
# i want to improve because...
unitmatch did provide high-confidence pairs, but i think, matching neurons is not a yes or no queston, it's variable. and it's unclear how reliable these good matches are. I want to check the reliability, and the quality.
> 🫀Matching should be treated as a hypothesis with uncertainty, not a binary conclusion.
# what i did...
i re-extract the raw waveforms(contains many messy works) of high-confidence pairs, and then drew the averaged waveforms.
>although waveform information is also used by um, reextracting raw wfs allowed me to independently reconstruct and visually assess whether high-confidence pairs preserve similar spatial waveform structure.
> unitmatch did use waveform as one of the features to calculate MatchProbability, and the waveform is from the outputs of bombcell(which is from kilosort output), what i did is re-extracted the raw-waveform from kilosort output,and calculate the standard and mean waveform of the high-confidence pairs. so bacsically, the two waveforms are from the same source, but in unitmatch, it was dealed through bombcell, while in my validation, it was re-extracted as raw waveform and then made into std+mean waveform. the new std+mean waveform is a partially indepent reconstructed ecidence for checking the accuracy of unitmatch output.

then i calculated the ACG of high-confidence pairs.
> ACG is a brand new feature here. provides an independent firing-pattern-based validation signal that is not directly the same as waveform-based matching.\
> now i'm confused, why independence is so important here? even though wfs shared parts of the resources, um is a model that combines it with other 5 features, it may be show how much weight here. and the wf should be a very important one, because it's obvious that if the the two neurons are the same one after checking the wfs. can we say something about weight here? though i want to mention that the prob here is an average of the values of 6 features. maybe it showes some questions that to make the um more accurate, they should adjust the weight. and if we can adjust the weight by ourselves based on needs would be better.
> because we cannot use the exact same evidences applied by models to prove I'm correct.but in this case, it's different, unitmatch used the waveform-related features dealt through Kilosort/bombcell, while i re-extracted waveform from raw data, and calculated mean+std, to check manually. so it's not new modal, but is independently reconstructed evidence.
> for weights, some high-matchprob pairs show disagreement with reconstructed wf and/or acg ecidence, suggesting that feature contributions may need to be interpreted case by case. redirect to future work

now i got waveforms and ACGs, i put these and the matchProb values together, and checked strong fits, poor fits and ambiguious fits from the unitmatch output.
The reason i chose waveform and ACG is, waveform can show the spaticial features of the neurons, ACG can show the temporal features of the neurons.
>question: is it enough? only checking the two features? or spaitial and temporal features?
>answer: af:morphological/spatial-electrophysiological evidence.acg:temporal firing-pattern evidence
but the final reliability assessment can add:
1. firing rate evidence
2. peak to trough time
3. amplitude
4. spatial location/depth
5. drift estimate
6. spike count/presence ratio
7. ISI violation/refractory contamination
8. within-session satbility
   but it not like more is better, i should ask the feature is providing the new evidence or repeat the existing evidence.
   
>no, for the final validation, it's not enough.
>we can add firing rate, amplitude, depth/location, drift estimate, spike count.presence ratio, ISI violation/refractory contamination, stability across time within session.
>question: it looks like we want to check the 6 features from um. so we already think the wf as a partially independent evidence, with the rest features, will it make the validation less pursuasive? or is it like some negative feedback? kinda like the features in physiology.
>answer:rechecking the unitmatch features helps interpret why the model assigned a high matchprob, while using additional evidence such as acg helps evaluate reliability beyond the original matching features.
>questions: what kinds of independent evidences we can use here?
>stronger independent evidence; ACG / firing pattern/Cross-correlogram with nearby units/Response to behavior / stimulus/Trial-aligned activity / event-aligned activity/Stability within session
>Partially independent evidence: re-extracted raw waveform/firing rate/amplitude/location/depth/drift estimate/spike count / presence ratio/ISI violation / refractory contamination
>Diagnostic evidence:UnitMatch 6 component scores/Bombcell quality metrics/Drift estimates/Session-level recording quality

# what i found...
strong fits showed supports from waveform and ACG simoutainiously
> there're good pairs with high matchprob, and almost the same shape of waveforms and distribution of acg.(about 4-5 out of 83)
poor fits showed support from neither waveform nor ACG
> there're also poor pairs with high matchprob,but with totally different waveforms and acg.

while ambigious fits showed support from either waveform nor ACG only
> also there're 1 or 2 pairs that have similar wf but different acg.(i didn't find the otherside-like pairs)
> what were most of the pairs look like?

# what suprised me...
Even among high-MatchProb pairs, I observed cases where independent waveform and ACG evidence did not support the proposed match.
# what can i do next?
what if i try more features that is seperated from the features used in unitmatch, will they also show differences? what kins of features i can use?
i can establish an evidence table
and keep analyze the different cases
think more about uncertainty
it's not just about neuron matching, how to validate a biological relationship.
i can build a simple model(logistic regression), to check the reliability of models and compare with checking manually.
> 1. Finish evidence table
> 2. Categorize all 83 high-confidence pairs
> 3. Quantify category counts
> 4. Add more independent features if available
> 5. Build a simple reliability score
> 6. Only then consider logistic regressio
>    question: how to deal with the direction? the pairs matching is from two directions, it's better to adjust to one direction right?
>    answer: use unordered pair, merge if the same pair show twice, use the max matchprob as the pair-level score.
>    for weight: check the 6 conponents scores of each pairs.if any feature score is systematically different among strong/poor/ambiguous pairs? if the poor fits shows a very high value feature, might suggest that this feature over-affect matchprob in some situation.











