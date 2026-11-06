---
layout: distill
title: CARE-Liver
description: Liver Fibrosis Quantification and Analysis
permalink: /track_liver/
bibliography: reference.bib
toc:
  - name: Registration
  - name: Motivation
  - name: Tasks
  - name: Data
  - name: Rules
  - name: Leaderboards
  - name: Citations
_styles: >
  d-article {
    contain: layout style;
    overflow-x: hidden;
    border-top: 1px solid rgba(0, 0, 0, 0.1);
    padding-top: 2rem;
    color: rgba(0, 0, 0, 0.8);
  }

  d-article > * {
    grid-column: text;
  }
---
## Registration
Registration for CARE 2026 has been closed.
<!--To access the dataset, please register [here](http://zmic.org.cn/care_2026/eval/register?track=liver).-->

## Motivation
{% include figure.liquid loading="eager" path="/assets/img/liqa1.png" class="img-fluid" zoomable=true caption="Figure 1. Track description." max-width="70%" %}

Liver fibrosis, arising from chronic viral or metabolic liver conditions, presents a significant global health challenge. Precise liver segmentation (LiSeg) and fibrosis staging (LiFS) are critical for enabling precise disease management, prognostication, and informed clinical decision-making. This challenge focuses on advancing **two interconnected objectives** to bridge clinical needs with AI innovation:  
1. **Automated Liver Segmentation**.  
2. **Multi-Phase Fibrosis Staging**.

Participants will develop robust AI solutions using multi-center, multi-phase MRI data, addressing real-world variability in imaging protocols and scanner systems.  

- **Recommended reading: Participants are encouraged to refer to our recent LiFS benchmark paper, ["How Far Has AI Come in Liver Fibrosis Staging? A Large-Scale Real-World Dataset and Benchmark"](https://arxiv.org/abs/2605.25595). This benchmark systematically evaluated MRI-based AI methods for liver fibrosis staging, including participating methods from CARE2025, under realistic multi-center settings. It also discusses challenges that are directly relevant to this track, including cross-center generalization, domain shift, contrast-enhanced imaging, label imbalance, and clinically meaningful evaluation endpoints.**

## Tasks
### **Task 1: Liver Fibrosis Staging (LiFS)**  
Develop models to stage fibrosis into four stages (S1-S4), leveraging **cross-phase complementary information** from dynamic MRI sequences. Participants should submit one four-class probability vector (S1-S4) per case. The organisers will derive two clinically critical binary evaluations from this single output, so separate models for the two clinical tasks are not required:  
1. **Cirrhosis Detection**: S1–S3 vs. S4  
2. **Substantial Fibrosis Detection**: S1 vs. S2–S4  

#### Subtasks:  
- **Non-Contrast Subtask**: T1WI, T2WI, and DWI sequences only. Submissions that do not use any GED modality are evaluated in this subtask.  
- **Contrast-Enhanced Subtask**: All modalities are allowed, including Gd-EOB-DTPA phases (GED1–GED4). Any method that uses at least one GED modality is evaluated in this subtask.  

### **Task 2: Liver Segmentation (LiSeg)**  
Segment the liver in multi-phase fibrosis, where **limited ground truth of Hepatobiliary phase (GED4) MRI** is available. Non-contrast data (T2WI, T1, DWI) could be segmented via **unsupervised or registration-based approaches** to overcome annotation limitations. For evaluation, metrics are reported for submitted modalities only (for example, GED4-only submissions receive GED4 metrics only).  

#### Subtasks:
- **Non-Contrast Subtask**: Segment liver anatomy in **T2WI**, **T1**, and **DWI** sequences. No annotations provided.
- **Contrast-Enhanced Subtask**: Segment **GED4** sequence. Limited annotations provided.

---

## Data

### About the data

**1) Scanner:** Philips Ingenia3.0T, Siemens Skyra 3.0T, Siemens Aera 1.5T.

**2) Dataset overview:**  The track cohort comprises **800 patients** (190 newly cases compared to CARE2025) diagnosed with liver fibrosis, all of whom underwent multi-phase MRI scans. The dataset includes **multi-phase** and **multi-center** data, with images acquired from clinical centers using three different MRI scanner vendors. The dataset consists of T2-weighted imaging, diffusion-weighted imaging, and Gadolinium ethoxybenzyl diethylenetriamine pentaacetic acid (**Gd-EOB-DTPA**)-enhanced dynamic MRIs. The Gd-EOB-DTPA-enhanced dynamic MRIs cover the non-contrast phase (T1WI), arterial phase, venous phase, delayed phase, and hepatobiliary phase.

**3) Contrast-enhanced dynamic scans:** Contrast-enhanced scans were performed based on the injection of the GD-EOB-DTPA agent. The arterial phase is captured 25 seconds after the contrast agent is injected. Subsequently, the portal phase is achieved 1 minute later. After another 3 minutes, the delay phase is obtained, and finally, the hepatobiliary phase is reached 20 minutes thereafter.

**4) Data format:** The data are all in Nifty format. Each sample may randomly lack phases (except hepatobiliary phase), and the sequences have not applied pre-alignment through spatial registration.

### Training set

<div style="display: flex;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:80%;align:center;">
  <thead>
    <tr>
      <th class="text-center" style="text-align:center;">Vendor</th>
      <th class="text-center" style="text-align:center;">Center</th>
      <th class="text-center" style="text-align:center;">#Cases</th>
      <th class="text-center" style="text-align:center;">#Annotation for seg</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="text-center">A</td>
      <td class="text-center">A</td>
      <td class="text-center">157</td>
      <td class="text-center">10</td>
    </tr>
    <tr>
      <td class="text-center">B</td>
      <td class="text-center">B1</td>
      <td class="text-center">230</td>
      <td class="text-center">10</td>
    </tr>
    <tr>
      <td class="text-center">B</td>
      <td class="text-center">B2</td>
      <td class="text-center">73</td>
      <td class="text-center">10</td>
    </tr>
  </tbody>
</table>
</div>


### Validation Set

<div style="display: flex;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:80%;align:center;">
  <thead>
    <tr>
      <th class="text-center" style="text-align:center;">Vendor</th>
      <th class="text-center" style="text-align:center;">Center</th>
      <th class="text-center" style="text-align:center;">#Cases</th>
      <th class="text-center" style="text-align:center;">#Annotation for seg</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="text-center">A</td>
      <td class="text-center">A</td>
      <td class="text-center">20</td>
      <td class="text-center">20</td>
    </tr>
    <tr>
      <td class="text-center">B</td>
      <td class="text-center">B1</td>
      <td class="text-center">20</td>
      <td class="text-center">20</td>
    </tr>
    <tr>
      <td class="text-center">B</td>
      <td class="text-center">B2</td>
      <td class="text-center">20</td>
      <td class="text-center">20</td>
    </tr>
  </tbody>
</table>
</div>

### Test Set

<div style="display: flex;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:50%;align:center;">
  <thead>
    <tr>
      <th class="text-center" style="text-align:center;">Vendor</th>
      <th class="text-center" style="text-align:center;">Center</th>
      <th class="text-center" style="text-align:center;">#Cases</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="text-center">A</td>
      <td class="text-center">A</td>
      <td class="text-center">50</td>
    </tr>
    <tr>
      <td class="text-center">B</td>
      <td class="text-center">B1</td>
      <td class="text-center">50</td>
    </tr>
    <tr>
      <td class="text-center">B</td>
      <td class="text-center">B2</td>
      <td class="text-center">50</td>
    </tr>
    <tr>
      <td class="text-center">C</td>
      <td class="text-center">C</td>
      <td class="text-center">130</td>
    </tr>
  </tbody>
</table>
</div>

- **NOTE: The evaluation on the unseen dataset (C) highlights the generalization capabilities of the models and algorithms, which we particularly emphasize.**

## Rules
1. Publicly available data (such as [LLD-MMRI2023](https://github.com/LMMMEng/LLD-MMRI2023)) and pre-trained models are allowed. 
2. Only automatic methods are acceptable. 

## Leaderboards
For LiFS, participants submit four-class probabilities for fibrosis staging (S1-S4). The organisers will compute AUC and ACC for two derived binary clinical subtasks: S1–S3 vs. S4 and S1 vs. S2–S4. Methods that use any contrast-enhanced GED modality are evaluated under the contrast-enhanced subtask, while methods that use only non-contrast modalities are evaluated under the non-contrast subtask.

For LiSeg, participants are required to segment the liver across multi-phase fibrosis MRI. We report Dice Similarity Score (DSC) and Hausdorff Distance (HD) only for the modalities included in each submission. If only GED4 is submitted, only GED4 metrics are reported; if additional modalities are submitted, their corresponding metrics are also reported.

The evaluation metrics for each task are summarized in the table below. The leaderboard will rank all participating teams according to the key metrics of each subtask, including AUC and ACC for LiFS.


<div style="display: flex;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:80%;align:center;">
  <thead>
    <tr>
      <th style="text-align:center;">Task</th>
      <th style="text-align:center;">Subtask</th>
      <th style="text-align:center;">Key Metrics</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="2"><strong>LiFS</strong></td>
      <td>Non-Contrast</td>
      <td>AUC, ACC (S4 vs. S1–S3; S1 vs. S2–S4)</td>
    </tr>
    <tr>
      <td>Contrast-Enhanced</td>
      <td>AUC, ACC (S4 vs. S1–S3; S1 vs. S2–S4)</td>
    </tr>
    <tr>
      <td rowspan="2"><strong>LiSeg</strong></td>
      <td>Non-Contrast (T1W1/T2WI/DWI)</td>
      <td>Dice Similarity Score (Dice), Hausdorff Distance (HD in mm)</td>
    </tr>
    <tr>
      <td>Contrast-Enhanced (GED4)</td>
      <td>Dice Similarity Score (Dice), Hausdorff Distance (HD in mm)</td>
    </tr>
  </tbody>
</table>
</div>

- **NOTE: Participants are welcome to participate in a single subtask, and their performance will still be recorded and displayed on the leaderboard. For LiSeg, scores are reported only for submitted modalities.**


<style>
  .sortable { width:100%; border-collapse:collapse; background:#fafafa;
              border-radius:8px; overflow:hidden; font-family:sans-serif;
              font-size:0.95rem; margin-bottom:32px; }
  .sortable thead tr { background:#2c3e50; color:#fff; }
  .sortable th { text-align:left; padding:10px; cursor:pointer; user-select:none; }
  .sortable td { padding:8px 10px; border-top:1px solid #eee; }
  .sortable .sort-arrow { display:inline-block; margin-left:4px; font-size:0.7em;
                          vertical-align:middle; opacity:0.3;
                          transition:opacity .15s ease; pointer-events:none; }
  .sortable th:hover .sort-arrow { opacity:0.65; }
  .sortable th.sort-active .sort-arrow { opacity:1; }
</style>

### Liver Fibrosis Staging (LiFS)
<!-- ============ 表 1：Liver Fibrosis Staging (LiFS) - Non-Contrast ============ -->
<div style="overflow-x:auto;">
<div class="table-note">
    Non-Contrast Setting. Sub1: S4 vs. S1–S3; Sub2: S1 vs. S2–S4. ID and OOD are displayed for reference.
</div>
<table id="lifs1" class="sortable">
  <thead>
    <tr>
      <th>Team</th>
      <th>Sub1 ACC (ID)↑</th>
      <th>Sub1 ACC (OOD)↑</th>
      <th>Sub1 AUC (ID)↑</th>
      <th>Sub1 AUC (OOD)↑</th>
      <th>Sub2 ACC (ID)↑</th>
      <th>Sub2 ACC (OOD)↑</th>
      <th>Sub2 AUC (ID)↑</th>
      <th>Sub2 AUC (OOD)↑</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>Ewunate@MedImg</td><td>0.6533</td><td>0.5769</td><td>0.7251</td><td>0.5860</td><td>0.8067</td><td>0.6538</td><td>0.8387</td><td>0.6073</td></tr>
  </tbody>
</table>
</div>

<!-- ============ 表 2：Liver Fibrosis Staging (LiFS) - Contrast-Enhanced ============ -->
<div style="overflow-x:auto;">
<div class="table-note">
    Contrast-Enhanced Setting. Sub1: S4 vs. S1–S3; Sub2: S1 vs. S2–S4. ID and OOD are displayed for reference.
</div>
<table id="lifs2" class="sortable">
  <thead>
    <tr>
      <th>Team</th>
      <th>Sub1 ACC (ID)↑</th>
      <th>Sub1 ACC (OOD)↑</th>
      <th>Sub1 AUC (ID)↑</th>
      <th>Sub1 AUC (OOD)↑</th>
      <th>Sub2 ACC (ID)↑</th>
      <th>Sub2 ACC (OOD)↑</th>
      <th>Sub2 AUC (ID)↑</th>
      <th>Sub2 AUC (OOD)↑</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>HNCS</td><td>0.7867</td><td>0.7538</td><td>0.8569</td><td>0.8659</td><td>0.8067</td><td>0.7923</td><td>0.8772</td><td>0.7495</td></tr>
    <tr><td>SIGMA</td><td>0.8133</td><td>0.5769</td><td>0.8826</td><td>0.8044</td><td>0.8467</td><td>0.8462</td><td>0.9064</td><td>0.7170</td></tr>
    <tr><td>vvvv</td><td>0.7667</td><td>0.7077</td><td>0.8373</td><td>0.8103</td><td>0.8067</td><td>0.8385</td><td>0.8068</td><td>0.6818</td></tr>
    <tr><td>CHORALE</td><td>0.6200</td><td>0.7154</td><td>0.8133</td><td>0.8334</td><td>0.7733</td><td>0.7923</td><td>0.8199</td><td>0.6509</td></tr>
    <tr><td>NECS-BVidAL</td><td>0.6400</td><td>0.8231</td><td>0.7937</td><td>0.9064</td><td>0.7533</td><td>0.8462</td><td>0.8096</td><td>0.6636</td></tr>
    <tr><td>HSFW3.0</td><td>0.7667</td><td>0.5462</td><td>0.8163</td><td>0.8290</td><td>0.8267</td><td>0.8308</td><td>0.8363</td><td>0.5914</td></tr>
    <tr><td>SINH-imaging</td><td>0.6333</td><td>0.6462</td><td>0.7991</td><td>0.8265</td><td>0.7533</td><td>0.8077</td><td>0.8111</td><td>0.5255</td></tr>
    <tr><td>JordanLowJunYi</td><td>0.4933</td><td>0.6385</td><td>0.7296</td><td>0.5714</td><td>0.7667</td><td>0.8385</td><td>0.8516</td><td>0.5173</td></tr>
    <tr><td>Ewunate@MedImg</td><td>0.6800</td><td>0.5923</td><td>0.7596</td><td>0.6175</td><td>0.8267</td><td>0.6154</td><td>0.8442</td><td>0.5877</td></tr>
    <tr><td>3289502410@qq.com</td><td>0.5467</td><td>0.6385</td><td>0.6389</td><td>0.3868</td><td>0.7533</td><td>0.7231</td><td>0.7692</td><td>0.3336</td></tr>
    <tr><td>xueleihe-nwu</td><td>0.5933</td><td>0.3692</td><td>0.6762</td><td>0.4107</td><td>0.7133</td><td>0.8462</td><td>0.7711</td><td>0.4386</td></tr>
  </tbody>
</table>
</div>

### Liver Segmentation (LiSeg)
<!-- ============ 表 3：LiSeg - Non-Contrast (T1W1/T2WI/DWI) ============ -->
<div style="overflow-x:auto;">
<div class="table-note">
    Non-Contrast (T1W1/T2WI/DWI) Setting.
</div>
<table id="liseg1" class="sortable">
  <thead>
  <tr>
    <th>Team</th>
    <th>Dice_T1 (ID)↑</th>
    <th>HD_T1 (ID)↓</th>
    <th>Dice_T2 (ID)↑</th>
    <th>HD_T2 (ID)↓</th>
    <th>Dice_DWI (ID)↑</th>
    <th>HD_DWI (ID)↓</th>
    <th>Dice_T1 (OOD)↑</th>
    <th>HD_T1 (OOD)↓</th>
    <th>Dice_T2 (OOD)↑</th>
    <th>HD_T2 (OOD)↓</th>
    <th>Dice_DWI (OOD)↑</th>
    <th>HD_DWI (OOD)↓</th>
  </tr>
  </thead>
  <tbody>
    <tr>
      <td>Ewunate@MedImg</td>
      <td>0.9676</td><td>20.1300</td>
      <td>0.9252</td><td>28.3800</td>
      <td>0.9224</td><td>20.8300</td>
      <td>0.9688</td><td>18.1500</td>
      <td>0.9103</td><td>17.1800</td>
      <td>0.9615</td><td>8.8000</td>
    </tr>
    <tr>
      <td>xueleihe-nwu</td>
      <td>0.9391</td><td>40.1000</td>
      <td>0.8997</td><td>46.5200</td>
      <td>0.8886</td><td>27.0300</td>
      <td>0.9470</td><td>28.2600</td>
      <td>0.8916</td><td>27.0000</td>
      <td>0.9294</td><td>11.7500</td>
    </tr>
    <tr>
      <td>SIGMA</td>
      <td>0.9490</td><td>45.0000</td>
      <td>0.8558</td><td>64.2500</td>
      <td>0.8673</td><td>49.9600</td>
      <td>0.9521</td><td>28.2400</td>
      <td>0.8495</td><td>44.2800</td>
      <td>0.9128</td><td>25.4300</td>
    </tr>
    <tr>
      <td>SINH-imaging</td>
      <td>0.7427</td><td>186.6700</td>
      <td>0.2915</td><td>156.3700</td>
      <td>0.2549</td><td>126.6800</td>
      <td>0.7903</td><td>102.4300</td>
      <td>0.1376</td><td>135.4500</td>
      <td>0.4274</td><td>65.9500</td>
    </tr>
  </tbody>
</table>
</div>

<!-- ============ 表 4：LiSeg - Contrast-Enhanced (GED4) ============ -->
<div style="overflow-x:auto;">
<div class="table-note">
    Contrast-Enhanced (GED4) Setting.
</div>
<table id="liseg2" class="sortable">
  <thead>
    <tr>
      <th>Team</th>
      <th>Dice (ID)↑</th>
      <th>HD (ID)↓</th>
      <th>Dice (OOD)↑</th>
      <th>HD (OOD)↓</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>Ewunate@MedImg</td><td>0.9736</td><td>19.8000</td><td>0.9821</td><td>11.6900</td></tr>
    <tr><td>Monster</td><td>0.9713</td><td>20.1800</td><td>0.9797</td><td>11.3600</td></tr>
    <tr><td>M2</td><td>0.9643</td><td>22.8500</td><td>0.9793</td><td>11.7200</td></tr>
    <tr><td>HSFW3.0</td><td>0.9664</td><td>22.2500</td><td>0.9763</td><td>12.0700</td></tr>
    <tr><td>JordanLowJunYi</td><td>0.9676</td><td>20.9700</td><td>0.9760</td><td>11.9500</td></tr>
    <tr><td>SIGMA</td><td>0.9665</td><td>33.6000</td><td>0.9749</td><td>22.8000</td></tr>
    <tr><td>xueleihe-nwu</td><td>0.9575</td><td>27.3000</td><td>0.9716</td><td>13.2500</td></tr>
    <tr><td>SUSTVI</td><td>0.9621</td><td>28.0000</td><td>0.9707</td><td>40.3100</td></tr>
    <tr><td>UniHD-DKFZ</td><td>0.9679</td><td>20.0500</td><td>0.9686</td><td>13.6600</td></tr>
    <tr><td>CHORALE</td><td>0.9548</td><td>30.0500</td><td>0.9628</td><td>17.5800</td></tr>
    <tr><td>3289502410@qq.com</td><td>0.9168</td><td>40.8300</td><td>0.9564</td><td>20.2200</td></tr>
    <tr><td>Yong</td><td>0.9140</td><td>35.6500</td><td>0.9247</td><td>21.7600</td></tr>
    <tr><td>SINH-imaging</td><td>0.8528</td><td>106.1800</td><td>0.8847</td><td>64.9200</td></tr>
    <tr><td>NECS-BVidAL</td><td>0.0630</td><td>325.1000</td><td>0.0816</td><td>177.0600</td></tr>
  </tbody>
</table>
</div>

<script>
function initSortable(tableId){
  var t = document.getElementById(tableId);
  if (!t) return;

  var tb  = t.tBodies[0];
  var ths = [].slice.call(t.tHead.rows[0].cells);
  var asc = [];   // 该表独立的排序状态

  ths.forEach(function(th, i){
    var arrow = document.createElement("span");
    arrow.className = "sort-arrow";
    arrow.textContent = "▲";
    th.appendChild(arrow);

    th.onclick = function(){
      asc[i] = !asc[i];

      // 本表内：只有当前列高亮，其余列复位变暗
      ths.forEach(function(h, j){
        var a = h.querySelector(".sort-arrow");
        if (j === i) {
          h.classList.add("sort-active");
          a.textContent = asc[i] ? "▲" : "▼";
        } else {
          h.classList.remove("sort-active");
          a.textContent = "▲";
        }
      });

      var rs = [].slice.call(tb.rows);
      rs.sort(function(a, b){
        var x = a.cells[i].textContent.trim();
        var y = b.cells[i].textContent.trim();
        var nx = parseFloat(x), ny = parseFloat(y);
        var c = (!isNaN(nx) && !isNaN(ny)) ? nx - ny : x.localeCompare(y);
        return asc[i] ? c : -c;
      });
      rs.forEach(function(r){ tb.appendChild(r); });
    };
  });
}

initSortable("lifs1");
initSortable("lifs2");
initSortable("liseg1");
initSortable("liseg2");
</script>


## Citations
**Please cite these papers when you use the data for publications:**
```bib

@misc{liu2026lifs,
      title={How Far Has AI Come in Liver Fibrosis Staging? A Large-Scale Real-World Dataset and Benchmark}, 
      author={Yuanye Liu and Nannan Shi and Zhejia Zhang and Hanxiao Zhang and Boya Wang and Derong Yu and Nao Wang and Yuxin Jin and Yang Zhou and Kunhao Yuan and Siqi Wang and Lida Yang and Xu Qiao and Wentao Liu and Xuelei He and Xin Hong and Guoyan Zheng and Xin Chen and Guang-Zhong Yang and Le Zhang and Lei Li and Yuxin Shi and Xiahai Zhuang},
      year={2026},
      eprint={2605.25595},
      archivePrefix={arXiv},
      url={https://arxiv.org/abs/2605.25595}, 
}

@article{liu2025merit,
  title = {MERIT: Multi-view evidential learning for reliable and interpretable liver fibrosis staging},
  author={Liu, Yuanye and Gao, Zheyao and Shi, Nannan and Wu, Fuping and Shi, Yuxin and Chen, Qingchao and Zhuang, Xiahai},
  journal = {Medical Image Analysis},
  volume = {102},
  pages = {103507},
  year = {2025}
}

@inproceedings{gao2023reliable,
  title={A reliable and interpretable framework of multi-view learning for liver fibrosis staging},
  author={Gao, Zheyao and Liu, Yuanye and Wu, Fuping and Shi, Nannan and Shi, Yuxin and Zhuang, Xiahai},
  booktitle={International Conference on Medical Image Computing and Computer-Assisted Intervention},
  pages={178--188},
  year={2023}
}

@article{wu2022meru,
  title = {Minimizing Estimated Risks on Unlabeled Data: A New Formulation for Semi-Supervised Medical Image Segmentation},
  author={Wu, Fuping and Zhuang, Xiahai},
  journal={IEEE Transactions on Pattern Analysis and Machine Intelligence}, 
  title={Minimizing Estimated Risks on Unlabeled Data: A New Formulation for Semi-Supervised Medical Image Segmentation}, 
  year={2023},
  volume={45},
  number={5},
  pages={6021-6036},
}
```

<script defer src="{{ '/assets/js/leaderboard_sort.js' | relative_url }}"></script>
