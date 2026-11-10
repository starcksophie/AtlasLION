# Atlas-Based Mapping of Hepatic Fat by Sex

Link to the paper

## Abstract

Hepatic proton density fat fraction (PDFF) is usually summarized as a single mean, without a population reference for individual fat distribution. We constructed longitudinal, sex- and visit-specific 3D PDFF atlases from 127 adults with obesity in the LION trial. Participants were imaged at 3T at baseline, after a low-calorie diet and after weight maintenance. Voxel-wise z-maps quantified each subject's deviation from the matched atlas. Six heterogeneity features (σx, CV, entropy, z-skewness, z-kurtosis, volume fraction z>2) were related to hepatocellular, glycemic and adiposity markers and to steatosis remission. Liver PDFF decreased significantly after the diet in males (13.6% to 6.6%) and females (9.1% to 5.9%), and fat loss was regional and sex-specific. Heterogeneity differed between sexes at baseline and after the diet, but not after weight maintenance. Cross-sectionally, heterogeneity correlated with hepatocellular, glycemic and adiposity markers, more strongly in females. Longitudinally, it tracked mainly adiposity change. Hepatic fat loss showed spatially heterogeneous and sex-specific patterns.

## Code layout

```
src/
  lion_utils.py     cohort definition, paths, functions shared between scripts
  preprocessing/    preprocessing, segmentation, PDFF, volumes, tabular data
  atlas/            atlases and their alignment
    registration/   registration to the reference, registration metrics
    couinaud/       Couinaud labels per subject and per atlas
  metrics/          heterogeneity features
  analysis/         longitudinal/, cross_sectional/, segments/, demographics/
  viz/              figures
```

Script names: `gen_*` computes results, `viz_*` draws figures from results that already exist. Scripts without a prefix are processing steps or shared code.

## Installation

```bash
git clone https://github.com/<user>/<repo>.git && cd <repo>
pip install -r requirements.txt
```

## Usage

The analysis covers the 280 scans listed in `available_data_280.csv` (see `group_subjects` in `src/lion_utils.py`). Scripts write to `results/`. Run them from their own folder, in this order:

```bash
# src/preprocessing/
python preprocess.py
python segment.py
python gen_pdff.py && python gen_volumes.py && python gen_tabular.py

# src/atlas/registration/
python register_all_final.py
python register_missing_subjects.py
python register_subjects_gt_segmentations.py
python gen_evaluate_registration.py

# src/atlas/
python gen_atlas.py
python gen_align_atlases_affine.py && python gen_align_atlases_affine_refine.py
python gen_align_atlases_deformable.py && python gen_align_atlases_deformable_refine.py

# src/atlas/couinaud/
python segment_missing_subjects.py
python gen_merge_segment_labels.py && python gen_correct_couineaud.py
python gen_atlas_couinaud_segments.py && python gen_atlas_segments.py
python gen_dice_before_after_correction.py && python gen_dice_nnunet_vs_couineaud.py

# src/metrics/
python gen_analyze_segments_majority.py

# src/analysis/
python longitudinal/gen_heterogeneity_change_correlation.py
python cross_sectional/gen_heterogeneity_cross_sectional.py
python gen_correlation_ci_table.py
python segments/gen_compare_subjects_to_atlas.py && python segments/gen_segment_change_stats.py
python demographics/gen_demographics_overview.py && python demographics/gen_table1_published_defs.py

# src/viz/: every viz_* script (viz_vessel_conspicuity.py with --cnr), then
python viz_export_tiff.py
```

## Results

```
results/
  atlases/                   atlases, Couinaud labels
  atlases_aligned/           affine alignment, atlas overview figure
  atlas_deformable_aligned/  deformable alignment, atlas change maps
  features/                  per-subject, per-segment features
  correlation/               longitudinal and cross-sectional correlations
  couinaud/                  segment analysis
  stats/                     demographics, registration metrics
  figures/                   figures, tif_600dpi/ for all figures at 600 DPI
```

## Data

LION study data (NCT04023942) are not included. They can be shared upon reasonable request.

## Citation

```bibtex
@article{starck2026liveratlas,
  title   = {Atlas-Based Mapping of Hepatic Fat by Sex: Results from the Lifestyle Intervention ({LION}) Study},
  author  = {Starck, Sophie and others},
  journal = {Journal of Magnetic Resonance Imaging},
  year    = {2026}
}
```