## Compatibility Check on a Four-Session Dataset (AA23)

To evaluate whether the workflow generalized beyond the original dataset, I attempted to run UnitMatch on a four-session dataset processed with Kilosort4 and manually curated in Phy.

### Observation

UnitMatch failed during preprocessing due to assumptions about the relationship between cluster IDs and template IDs.

Several sessions contained cluster IDs that exceeded the number of templates:

| Session | Templates | Max Cluster ID |
|----------|----------:|---------------:|
| AA23_01 | 476 | 528 |
| AA23_02 | 327 | 351 |
| AA23_03 | 324 | 342 |
| AA23_05 | 321 | 349 |

Further inspection showed that manually curated clusters could represent merged templates. For example:

```text
cluster 476 → templates 19, 26
cluster 477 → templates 155, 156
cluster 478 → templates 409, 418
```

As a result, assumptions such as:

```matlab
cluster index == template index
```

were no longer valid after manual curation.

### Implication

This dataset exposed a software compatibility limitation rather than a biological matching issue. Before evaluating match reliability using waveform or ACG evidence, it is necessary to verify that the preprocessing pipeline remains compatible with the underlying data structure.

This observation highlights an additional source of uncertainty in cross-session tracking workflows: reliability can be affected not only by biological evidence, but also by assumptions embedded in analysis software.

### Decision

Because the objective of this project is evidence-based reliability assessment rather than software debugging, the main analyses were continued using the original dataset that successfully completed the UnitMatch pipeline. The AA23 dataset was retained as a case study illustrating pipeline assumptions and compatibility challenges in manually curated Kilosort4 outputs.
