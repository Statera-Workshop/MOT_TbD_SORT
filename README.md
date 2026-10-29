# MOT_TbD_SORT

**SORT** - online multi-object tracking by detection on KITTI-MOTS: 25 detectors + the detections of FairMOT.

- Paper: Bewley et al., ICIP 2016; official code: `abewley/sort`
- Principle: Kalman filter (x, y, s, r) + Hungarian IoU matching
- **(best)**: the best of the 10 trackers on that detector; last column = that best HOTA.
- Implementation: `common/mot/trackers.py` (`sort`), re-implemented after the official code, official defaults
  (the class docstring lists every value and every `[Unified]` difference). Causality check: all OK.

### Results (SORT, official defaults, KITTI-MOTS val)

| detector | HOTA | DetA | AssA | MOTA | IDF1 | IDSW | car | pedestrian | tracker ms | pipeline ms | best tracker on this detector |
|---|---|---|---|---|---|---|---|---|---|---|---|
| cascade_rcnn | 0.524 | 0.492 | 0.562 | 0.579 | 0.659 | 100 | 0.603 | 0.445 | 0.25 | 35.1 | 0.625 |
| libra_rcnn | 0.506 | 0.486 | 0.531 | 0.544 | 0.634 | 126 | 0.611 | 0.401 | 0.29 | 26.8 | 0.599 |
| faster_rcnn | 0.486 | 0.460 | 0.521 | 0.541 | 0.630 | 119 | 0.599 | 0.373 | 0.27 | 25.2 | 0.582 |
| dynamic_rcnn | 0.479 | 0.463 | 0.498 | 0.532 | 0.612 | 115 | 0.581 | 0.377 | 0.26 | 25.3 | 0.579 |
| atss | 0.474 | 0.435 | 0.523 | 0.509 | 0.611 | 95 | 0.580 | 0.369 | 0.24 | 22.0 | 0.527 |
| v6 | 0.432 | 0.384 | 0.489 | 0.461 | 0.560 | 80 | 0.570 | 0.294 | 0.23 | 6.8 | 0.509 |
| gfl | 0.428 | 0.396 | 0.467 | 0.462 | 0.540 | 92 | 0.560 | 0.297 | 0.23 | 21.0 | 0.522 |
| tood | 0.410 | 0.374 | 0.454 | 0.430 | 0.509 | 108 | 0.547 | 0.274 | 0.23 | 25.0 | 0.506 |
| ppyoloe | 0.408 | 0.370 | 0.456 | 0.435 | 0.518 | 95 | 0.570 | 0.245 | 0.24 | 6.5 | 0.487 |
| rtmdet | 0.404 | 0.348 | 0.472 | 0.421 | 0.524 | 74 | 0.562 | 0.245 | 0.21 | 6.4 | 0.465 |
| x | 0.401 | 0.352 | 0.463 | 0.414 | 0.522 | 83 | 0.541 | 0.262 | 0.23 | 5.7 | 0.478 |
| fcos | 0.399 | 0.366 | 0.439 | 0.428 | 0.495 | 85 | 0.524 | 0.275 | 0.22 | 21.8 | 0.493 |
| retinanet | 0.398 | 0.382 | 0.419 | 0.449 | 0.505 | 120 | 0.532 | 0.265 | 0.23 | 21.3 | 0.535 |
| x2 | 0.382 | 0.334 | 0.439 | 0.394 | 0.504 | 81 | 0.554 | 0.210 | 0.22 | 5.2 | 0.452 |
| v9 | 0.372 | 0.307 | 0.457 | 0.356 | 0.457 | 73 | 0.535 | 0.209 | 0.20 | 12.1 | 0.460 |
| v10 | 0.369 | 0.325 | 0.422 | 0.387 | 0.474 | 78 | 0.536 | 0.202 | 0.21 | 8.0 | 0.455 |
| v8 | 0.362 | 0.302 | 0.442 | 0.355 | 0.450 | 81 | 0.526 | 0.198 | 0.20 | 5.5 | 0.443 |
| v12 | 0.360 | 0.300 | 0.433 | 0.348 | 0.440 | 72 | 0.507 | 0.212 | 0.20 | 8.6 | 0.424 |
| v11 | 0.354 | 0.282 | 0.459 | 0.326 | 0.427 | 69 | 0.543 | 0.166 | 0.20 | 6.6 | 0.435 |
| v26 | 0.322 | 0.274 | 0.382 | 0.328 | 0.415 | 67 | 0.536 | 0.107 | 0.21 | 9.0 | 0.390 |
| fairmot | 0.315 | 0.265 | 0.375 | 0.318 | 0.408 | 72 | 0.455 | 0.174 | 0.20 | 8.4 | 0.387 |
| deformable_detr | 0.314 | 0.313 | 0.317 | 0.360 | 0.400 | 126 | 0.406 | 0.222 | 0.21 | 68.5 | 0.482 |
| v13 | 0.313 | 0.260 | 0.404 | 0.307 | 0.375 | 73 | 0.522 | 0.104 | 0.20 | 10.8 | 0.372 |
| centernet | 0.302 | 0.260 | 0.355 | 0.313 | 0.398 | 83 | 0.433 | 0.172 | 0.20 | 7.7 | 0.395 |
| v1 | 0.250 | 0.236 | 0.270 | 0.258 | 0.323 | 170 | 0.353 | 0.148 | 0.20 | 6.1 | 0.374 |
| ssd | 0.230 | 0.204 | 0.267 | 0.239 | 0.292 | 48 | 0.458 | 0.002 | 0.17 | 29.5 | 0.288 |

### Score-threshold sensitivity (SORT, HOTA with one common threshold)

| detector | 0.3 | 0.4 | 0.5 | 0.6 | 0.7 |
|---|---|---|---|---|---|
| deformable_detr | 0.420 | 0.374 | 0.314 | 0.244 | 0.179 |
| faster_rcnn | 0.476 | 0.484 | 0.486 | 0.479 | 0.473 |
| fcos | 0.461 | 0.446 | 0.399 | 0.362 | 0.284 |
| libra_rcnn | 0.495 | 0.501 | 0.506 | 0.507 | 0.508 |
| ppyoloe | 0.433 | 0.430 | 0.408 | 0.369 | 0.329 |
| rtmdet | 0.449 | 0.439 | 0.404 | 0.359 | 0.284 |
| v10 | 0.423 | 0.394 | 0.369 | 0.331 | 0.277 |
| v11 | 0.394 | 0.368 | 0.354 | 0.329 | 0.292 |
| v12 | 0.412 | 0.388 | 0.360 | 0.298 | 0.227 |
| v13 | 0.342 | 0.329 | 0.313 | 0.296 | 0.261 |
| v26 | 0.373 | 0.351 | 0.322 | 0.279 | 0.237 |
| v6 | 0.476 | 0.457 | 0.432 | 0.407 | 0.363 |
| v8 | 0.403 | 0.388 | 0.362 | 0.332 | 0.274 |
| v9 | 0.416 | 0.407 | 0.372 | 0.332 | 0.291 |
| x | 0.421 | 0.416 | 0.401 | 0.381 | 0.333 |
| x2 | 0.411 | 0.406 | 0.382 | 0.343 | 0.286 |

Part of the *Physical AI MOT* comparison of the **Statera Working Group**: 10 trackers x 25 detectors (+ the detections of FairMOT), 3 joint
detection-and-tracking networks and 1 end-to-end tracker under one protocol. The full comparison (Pareto front,
tracker ranking, JDT / E2E against tracking-by-detection) is in `MOT_Detectors_KITTIMOTS` (`RESULTS.md`).

## Protocol (all MOT_* repositories)

- Online / causal only: every method sees the current frame and its own state; checked by re-running prefixes of
  every sequence (the output of frame t must not change when later frames are removed).
- Input 1216 x 384 (KITTI 1242 x 375 letterboxed), detectors trained from scratch on KITTI-MOTS train (12 sequences),
  30 epochs, Adam 1e-4, effective batch 8, seed 777 - the protocol of the *Physical AI Object Detection* series.
- Metrics: HOTA / DetA / AssA (TrackEval classes, car / pedestrian mean), MOTA, IDF1, IDSW.
- Latency: RTX 4070 Laptop GPU, batch 1, fp32, medians over val; pipeline = detector (forward + post-processing) +
  ReID (appearance trackers) + tracker (CPU); image decoding / letterboxing not included.
- Trackers run with their official default parameters; frame-based values given for 30 fps are scaled to 10 fps.
  A sensitivity table with one common score threshold for every tracker is reported separately (chosen on val, so it
  is analysis, not ranking).

## Data: KITTI-MOTS (box level, val = 9 sequences, 2,981 frames)

KITTI tracking images (21 training sequences) with instance / track annotations; boxes = tight boxes of the masks,
classes car and pedestrian, ignore regions (id 10000) neither rewarded nor penalised. The annotations are taken from
the **KITTI-STEP** panoptic maps (same sequences and split, car / person instances merged from KITTI-MOTS; frames,
track counts and pedestrian masks match the KITTI-MOTS paper, car masks differ by 39 of 26,899).

```bash
bash tools/mot/get_kitti_mots.sh            # KITTI tracking images + annotations (KITTI-STEP fallback)
python tools/mot/kittimots_to_voc.py        # VOC-layout copy with tracks + count report
UNIFIED_IMAGE_DATASET=kittimots python tools/mot/count_loader.py     # counts as the loaders read them
```

**Licence of the data and of every trained weight here: KITTI / KITTI-MOTS / KITTI-STEP are CC BY-NC-SA 3.0
(non-commercial).**

## Usage

```bash
pip install -r requirements.txt
pip install "git+https://github.com/JonathonLuiten/TrackEval.git@12c8791b303e0a0b50f753af204249e622d0281a"
# saved detections (+ ReID features) of the 25 detectors: Release of Statera-Workshop/MOT_Detectors_KITTIMOTS
python tools/mot/run_tracker.py --source kittimots --dets dets/x_reid.npz --trackers sort --causal
python tools/mot/run_tracker.py --source kittimots --dets dets/x_reid.npz --gt-as-pred      # evaluation self-test
python tools/mot/mot_table.py                                                             # tables of all runs
```

`run_tracker.py --trackers` accepts every tracker of the comparison (iou, sort, bytetrack, ocsort, hybridsort, botsort, botsort_reid, deepsort, tracktrack, fairmot), so other
trackers can be run on the same detections. Results of this repository: `results/` (JSON per detector).

## Files

```
common/mot/trackers.py    the trackers of the comparison (default here: sort)
common/mot/core.py        boxes, IoU, assignment, Kalman filters, camera-motion estimation
common/mot/evaluate.py    KITTI-MOTS ground truth and TrackEval metrics
tools/mot/run_tracker.py  run / time / evaluate trackers on saved detections (+ causality check)
tools/mot/*kitti*         data preparation
results/                  evaluation JSON of this repository's tracker(s)
THIRD_PARTY.md            sources and licences
```

## Global Collaboration

Hills Robotics is currently participating in multiple projects in Korea and internationally.

We are actively interested in building relationships with organizations that can complement our technology with global sales networks, distribution channels, system integration capabilities, manufacturing ecosystems, AI infrastructure, robotics technologies, research capabilities, or strategic investment.

Several technology and business collaborations are already underway. Some partners, projects, system architectures, and commercial programs cannot be publicly disclosed because they are subject to confidentiality and business agreements.

We believe that the emerging Physical AI ecosystem cannot be built by a single company.
It requires a global network connecting robotics companies, AI researchers, semiconductor and computing companies, sensor manufacturers, software developers, universities, system integrators, industrial customers, investors, and global distribution partners.

We have now begun our serious exploration of the Physical AI frontier, and we welcome connections with people and organizations who want to build this ecosystem together.

## Research, Contribution, and Donation

The repositories of the Statera Working Group are intended to contribute to the broader technical discussion around Physical AI.

Researchers, engineers, developers, companies, universities, and independent contributors interested in these subjects are welcome to connect with us.

If you would like to collaborate on Physical AI or autonomous robotics, participate in research or technology development, discuss international business cooperation, propose technology or platform integration, contribute technical knowledge, or support this GitHub knowledge initiative through sponsorship or donation, please contact us.

## Contact

**Richard Minsoo Go**
Head of AI, Hills Robotics
Statera Working Group

Personal / Research Contact:
[gominsoo888@gmail.com](mailto:gominsoo888@gmail.com)

Hills Robotics / Business Contact:
[minsoo.go@hillslogis.com](mailto:minsoo.go@hillslogis.com)

Hills Robotics:
https://hillslogis.com/

For inquiries regarding next-generation outdoor autonomous robotic platforms, Physical AI Spider Grid, Intelligence Cabinet, Edge AI, or On-Premise AI architectures that are not yet publicly presented on the company website, please contact us directly.
