---
layout: distill
title: CARE-Whole Heart
description: Whole Heart Segmentation
permalink: /track_wholeheart/
bibliography: reference.bib
toc:
  - name: Registration
  - name: Motivation
  - name: Task
  - name: Data
  - name: Rules
  - name: Metrics
  - name: Award Policy
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
<!--To access the dataset, please register [here](http://zmic.org.cn/care_2026/eval/register?track=wholeheart).-->

## Motivation

Cardiovascular diseases (CVDs), as the leading cause of death globally<d-cite key="whs1"></d-cite>, necessitate precise morphological and pathological quantification through segmentation of crucial cardiac structures from medical images<d-cite key="whs2"></d-cite>. However, whole heart segmentation (WHS) faces challenges including heart shape variability during the cardiac cycle, clinical artifacts like motion and poor contrast-to-noise ratio, as well as domain shifts in multi-center data and the distinct modalities of CT and MRI. CARE-Whole Heart serves to inspire innovative solutions in the realms of biomedical imaging and computer vision, striving to overcome these challenges and advance automated WHS for enhanced understanding and treatment of CVDs.

## Task
{% include figure.liquid loading="eager" path="/assets/img/whs.png" class="img-fluid" zoomable=true max-width="70%" caption="Figure 1. Overview of CARE-Whole Heart" %}

The objective of this track is to achieve precise segmentation of seven substructures of the whole heart, with robustness against domain shifts (see Fig. 1).  
The specific substructures, each associated with a unique label value, are:

1. **Left Ventricular Blood Cavity (LV)** - Label value: 500
2. **Right Ventricular Blood Cavity (RV)** - Label value: 600
3. **Left Atrial Blood Cavity (LA)** - Label value: 420
4. **Right Atrial Blood Cavity (RA)** - Label value: 550
5. **Myocardium of the Left Ventricle (Myo)** - Label value: 205
6. **Ascending Aorta (AO)** - Label value: 820; defined as the aortic trunk from the aortic valve to the superior level of the atria.
7. **Pulmonary Artery (PA)** - Label value: 850; defined as the initial segment from the pulmonary valve to the bifurcation point.


**Note on Great Vessels:** The great vessels of interest, comprising the ascending aorta and pulmonary artery, are specifically defined due to variations in the fields of view across different scans. This uniform definition is crucial for ensuring consistency across evaluations. During the assessment, segmentation results for these vessels will be truncated to average lengths measured in healthy subjects, although participants are encouraged to extend their segmentation beyond these lengths. Our provided manual segmentations similarly cover more than the defined trunk measurements.


## Data

### About the data

**1) Dataset overview:** CARE-Whole Heart has **246** cases collected from **8** centers, supporting in-distribution and out-of-distribution performance evaluation for methods. Moreover, the diversity and clinical relevance of the dataset offers a broader spectrum of anatomical and pathological variations.

**2) Scanner:** Philips 64-slice CT scanner, SIEMENS SOMATOM Force CT scanner, GE Revolution_CT scanner, Philips Achieva 1.5T,
Siemens Avanto 1.5T, Toshiba Aquilion ONE CT scanner.

**3) Data format:** The data are all in Nifty format. Each training case has one CT or MRI scan with its corresponding label.

### Training data (106 Cases)

<div style="display: flex;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
  <thead>
    <tr>
      <th style="text-align:center;">Center</th>
      <th style="text-align:center;">Num. patients</th>
      <th style="text-align:center;">Modalities</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>A</td>
      <td>20</td>
      <td>CT</td>
    </tr>
    <tr>
      <td>B</td>
      <td>20</td>
      <td>CT</td>
    </tr>
    <tr>
      <td>C & D</td>
      <td>20</td>
      <td>MRI</td>
    </tr>
    <tr>
      <td>E</td>
      <td>26</td>
      <td>MRI</td>
    </tr>
    <tr>
      <td>G</td>
      <td>20</td>
      <td>CT</td>
    </tr>
  </tbody>
</table>
</div>

```
A ct_train
  |-- Case1001_image.nii.gz
  |-- Case1001_label.nii.gz
  |-- ...
B ct_train
  |-- Case2001_image.nii.gz
  |-- Case2001_label.nii.gz
  |-- ...
C and D mr_train
  |-- Case3001_image.nii.gz
  |-- Case3001_label.nii.gz
  |-- ...
...
```

### Validation data (50 Cases)

<div style="display: flex;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
  <thead>
    <tr>
      <th style="text-align:center;">Center</th>
      <th style="text-align:center;">Num. patients</th>
      <th style="text-align:center;">Modalities</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>A</td>
      <td>20</td>
      <td>CT</td>
    </tr>
    <tr>
      <td>B</td>
      <td>10</td>
      <td>CT</td>
    </tr>
    <tr>
      <td>C & D</td>
      <td>20</td>
      <td>MRI</td>
    </tr>
  </tbody>
</table>
</div>

```
ct_val
|-- CaseCTVal001_image.nii.gz
|-- CaseCTVal002_image.nii.gz
|-- CaseCTVal003_image.nii.gz
|-- ...
mr_val
|-- CaseMRVal001_image.nii.gz
|-- CaseMRVal002_image.nii.gz
|-- CaseMRVal003_image.nii.gz
|-- ...
```

### Test data (90 Cases)

<div style="display: flex;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
  <thead>
    <tr>
      <th style="text-align:center;">Center</th>
      <th style="text-align:center;">Num. patients</th>
      <th style="text-align:center;">Modalities</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>A</td>
      <td>20</td>
      <td>CT</td>
    </tr>
    <tr>
      <td>B</td>
      <td>14</td>
      <td>CT</td>
    </tr>
    <tr>
      <td>C & D</td>
      <td>20</td>
      <td>MRI</td>
    </tr>
    <tr>
      <td>F</td>
      <td>16</td>
      <td>MRI</td>
    </tr>
    <tr>
      <td>H</td>
      <td>20</td>
      <td>CT</td>
    </tr>
  </tbody>
</table>
</div>

```
ct_test
|-- CaseCTTest001_image.nii.gz
|-- CaseCTTest002_image.nii.gz
|-- CaseCTTest003_image.nii.gz
|-- ...
mr_test
|-- CaseMRTest001_image.nii.gz
|-- CaseMRTest002_image.nii.gz
|-- CaseMRTest003_image.nii.gz
|-- ...
```

**Note on Validation and Test datasets**: We have randomly shuffled the data from different centers and anonymized the center information to promote fairness.

## Rules
- **Only automatic methods are acceptable.** In this track, participants must utilize algorithms that do not require manual intervention or human-assisted processes for the segmentation task.
- **Pre-trained models are allowed.** In this track, the solutions could be developed with open pre-trained fundation models, such as SAM, CLIP and MedSAM.
- **Publicly available data is allowed.** In this track, participants may also include publicly available data. Such additional data needs to be publicly available **before** the date of the test results submission (July 10, 2026). Private annotations of such data is prohibited.


## Metrics
The performance of segmentation results will be assessed through: 
- **Dice Similarity Coefficient (DSC)**: DSC is well-suited for assessing the overlap or agreement between the predicted segmentation and the ground truth, making it particularly useful when the regions of interest in medical images may partially overlap.
- **Hausdorff Distance (HD in mm)**: HD measures the maximum distance between two sets, indicating the degree of boundary mismatch.

<!--## Award Policy

This track will give **2** best performance awards according to performances across **CT** images and **MRI** images, refered to as **Whole heart segmentation (CT)** and **Whole heart segmentation (MRI)**, respectively. 

- In ranking, we first compute the average DSC and average HD of **WHS** across all cases of test data. After that, the final score for one team is computed as the sum of team’s ranks in the DSC and HD rankings.
- The team that has the **lowest** final score will get the best performance award
- **Ties are permitted when teams achieve identical scores.**-->


<!--We will rank participant methods based on the settings (​Lb1–Lb4) detailed in the following table:

<div style="display: flex;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
<caption style="caption-side: top; text-align: left; font-weight: bold; padding-bottom: 10px;width: 100%;"> Leaderboard (Lb) for CARE-Whole Heart track across modalities and evaluation settings.​​ Lb1–Lb4 represent performance from different test centers and modalities (e.g., Lb1 = CT segmentation peformance on center A and B). In-distribution refers to centers included in the training data, while out-of-distribution refers to unseen centers not used during training.</caption>
  <thead>
    <tr>
      <th style="text-align:center;">Modality</th>
      <th style="text-align:center;">In-distribution</th>
      <th style="text-align:center;">Out-of-distribution</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>CT</td>
      <td>Lb1</td>
      <td>Lb2</td>
    </tr>
    <tr>
      <td>MR</td>
      <td>Lb3</td>
      <td>Lb4</td>
    </tr>
  </tbody>
</table>
</div>-->


## Leaderboards

We will provide 2 leaderboards, representing stratified performance across different modalities, CT and MRI. In each leaderboard, in addition to DSC and HD of 7 cardiac substructures, we will also report DSC and HD of whole heart segmentation (DSC_WH and HD_WH), which are weighted average (according to their volumes) from 7 substructures. 


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

### Whole heart segmentation (CT)
<!-- ============ 表 1：WHS-CT ============ -->
<div style="overflow-x:auto;">
<table id="whsct" class="sortable">
  <thead>
    <tr>
      <th>Team</th>
      <th>DSC<sub>LV</sub>↑</th>
      <th>DSC<sub>Myo</sub>↑</th>
      <th>DSC<sub>RV</sub>↑</th>
      <th>DSC<sub>LA</sub>↑</th>
      <th>DSC<sub>RA</sub>↑</th>
      <th>DSC<sub>AO</sub>↑</th>
      <th>DSC<sub>PA</sub>↑</th>
      <th>DSC<sub>WH</sub>↑</th>
      <th>HD<sub>WH</sub>(mm)↓</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>BIT</td><td>0.9470</td><td>0.9307</td><td>0.9299</td><td>0.9617</td><td>0.9281</td><td>0.9609</td><td>0.8806</td><td>0.9414</td><td>11.3366</td></tr>
    <tr><td>SJTUMedSeg</td><td>0.9456</td><td>0.9318</td><td>0.9292</td><td>0.9611</td><td>0.9273</td><td>0.9596</td><td>0.8787</td><td>0.9411</td><td>11.6841</td></tr>
    <tr><td>VMHeart</td><td>0.9468</td><td>0.9334</td><td>0.9301</td><td>0.9624</td><td>0.9282</td><td>0.9603</td><td>0.8771</td><td>0.9420</td><td>11.7652</td></tr>
    <tr><td>MEDII</td><td>0.9452</td><td>0.9285</td><td>0.9270</td><td>0.9601</td><td>0.9259</td><td>0.9584</td><td>0.8774</td><td>0.9396</td><td>11.7364</td></tr>
    <tr><td>Monster</td><td>0.9431</td><td>0.9293</td><td>0.9288</td><td>0.9595</td><td>0.9258</td><td>0.9582</td><td>0.8716</td><td>0.9394</td><td>12.0265</td></tr>
    <tr><td>AI_WHS_xjtlu</td><td>0.9421</td><td>0.9236</td><td>0.9203</td><td>0.9508</td><td>0.9161</td><td>0.9549</td><td>0.8735</td><td>0.9333</td><td>12.4595</td></tr>
    <tr><td>M2Lab</td><td>0.9376</td><td>0.9271</td><td>0.9184</td><td>0.9595</td><td>0.8833</td><td>0.9475</td><td>0.8791</td><td>0.9305</td><td>12.8700</td></tr>
    <tr><td>Slience</td><td>0.9337</td><td>0.9180</td><td>0.9196</td><td>0.9528</td><td>0.9119</td><td>0.9549</td><td>0.8637</td><td>0.9303</td><td>14.1676</td></tr>
    <tr><td>NECS</td><td>0.9245</td><td>0.8817</td><td>0.8981</td><td>0.9331</td><td>0.9012</td><td>0.9340</td><td>0.8403</td><td>0.9091</td><td>13.3534</td></tr>
    <tr><td>xigema</td><td>0.9161</td><td>0.8890</td><td>0.9012</td><td>0.9432</td><td>0.8778</td><td>0.9442</td><td>0.8531</td><td>0.9118</td><td>15.7054</td></tr>
    <tr><td>TEAM1422_Whole_Heart</td><td>0.9197</td><td>0.9008</td><td>0.8966</td><td>0.9486</td><td>0.8885</td><td>0.9462</td><td>0.8346</td><td>0.9139</td><td>17.7390</td></tr>
    <tr><td>DH</td><td>0.9354</td><td>0.9113</td><td>0.9131</td><td>0.9477</td><td>0.8614</td><td>0.9517</td><td>0.8709</td><td>0.9239</td><td>31.9159</td></tr>
    <tr><td>CardiacEndeavours</td><td>0.8362</td><td>0.7327</td><td>0.8231</td><td>0.8766</td><td>0.8058</td><td>0.8278</td><td>0.6988</td><td>0.8097</td><td>18.2154</td></tr>
    <tr><td>Kiruthiga.K</td><td>0.8362</td><td>0.7327</td><td>0.8231</td><td>0.8766</td><td>0.8058</td><td>0.8278</td><td>0.6988</td><td>0.8097</td><td>18.2154</td></tr>
  </tbody>
</table>
</div>

<!-- ============ 表 2：WHS-MR ============ -->
### Whole heart segmentation (MRI)
<div style="overflow-x:auto;">
<table id="whsmr" class="sortable">
  <thead>
    <tr>
      <th>Team</th>
      <th>DSC<sub>LV</sub>↑</th>
      <th>DSC<sub>Myo</sub>↑</th>
      <th>DSC<sub>RV</sub>↑</th>
      <th>DSC<sub>LA</sub>↑</th>
      <th>DSC<sub>RA</sub>↑</th>
      <th>DSC<sub>AO</sub>↑</th>
      <th>DSC<sub>PA</sub>↑</th>
      <th>DSC<sub>WH</sub>↑</th>
      <th>HD<sub>WH</sub>(mm)↓</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>VMHeart</td><td>0.9406</td><td>0.8483</td><td>0.9036</td><td>0.9041</td><td>0.8930</td><td>0.9056</td><td>0.8476</td><td>0.9015</td><td>20.2336</td></tr>
    <tr><td>BIT</td><td>0.9398</td><td>0.8497</td><td>0.9046</td><td>0.8986</td><td>0.8911</td><td>0.9020</td><td>0.8471</td><td>0.9001</td><td>20.3311</td></tr>
    <tr><td>Monster</td><td>0.9398</td><td>0.8511</td><td>0.9038</td><td>0.9019</td><td>0.8904</td><td>0.9028</td><td>0.8412</td><td>0.9005</td><td>21.0346</td></tr>
    <tr><td>AI_WHS_xjtlu</td><td>0.9379</td><td>0.8425</td><td>0.8967</td><td>0.8990</td><td>0.8895</td><td>0.8979</td><td>0.8401</td><td>0.8959</td><td>20.2396</td></tr>
    <tr><td>MEDII</td><td>0.9390</td><td>0.8436</td><td>0.9024</td><td>0.8992</td><td>0.8907</td><td>0.9028</td><td>0.8470</td><td>0.8986</td><td>20.9197</td></tr>
    <tr><td>SJTUMedSeg</td><td>0.9388</td><td>0.8443</td><td>0.9019</td><td>0.9013</td><td>0.8900</td><td>0.9049</td><td>0.8429</td><td>0.8990</td><td>21.1861</td></tr>
    <tr><td>M2Lab</td><td>0.9375</td><td>0.8462</td><td>0.9033</td><td>0.8901</td><td>0.8867</td><td>0.9029</td><td>0.8404</td><td>0.8960</td><td>21.2334</td></tr>
    <tr><td>DH</td><td>0.9256</td><td>0.8217</td><td>0.8614</td><td>0.8999</td><td>0.8817</td><td>0.8711</td><td>0.8019</td><td>0.8832</td><td>28.5251</td></tr>
    <tr><td>Kiruthiga.K</td><td>0.8418</td><td>0.6665</td><td>0.7959</td><td>0.8296</td><td>0.8035</td><td>0.7829</td><td>0.6676</td><td>0.7829</td><td>22.9774</td></tr>
    <tr><td>CardiacEndeavours</td><td>0.8418</td><td>0.6665</td><td>0.7959</td><td>0.8296</td><td>0.8035</td><td>0.7829</td><td>0.6676</td><td>0.7829</td><td>22.9774</td></tr>
    <tr><td>Slience</td><td>0.9134</td><td>0.7707</td><td>0.8544</td><td>0.8774</td><td>0.8606</td><td>0.8271</td><td>0.8025</td><td>0.8608</td><td>43.9680</td></tr>
    <tr><td>TEAM1422_Whole_Heart</td><td>0.7579</td><td>0.5580</td><td>0.6512</td><td>0.8000</td><td>0.7452</td><td>0.7817</td><td>0.4876</td><td>0.7064</td><td>43.8478</td></tr>
    <tr><td>xigema</td><td>0.8613</td><td>0.7355</td><td>0.7895</td><td>0.7923</td><td>0.7611</td><td>0.8015</td><td>0.7338</td><td>0.7986</td><td>74.9196</td></tr>
    <tr><td>NECS</td><td>0.8076</td><td>0.6866</td><td>0.5575</td><td>0.5578</td><td>0.3987</td><td>0.5224</td><td>0.0753</td><td>0.6165</td><td>73.5788</td></tr>
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

initSortable("whsct");
initSortable("whsmr");
</script>

## Citations
**Please cite these papers when you use the data for publications:**

```
@article{Zhuang2016MSMMA,
  Author = {Zhuang, Xiahai and Shen, Juan},
  Title = {Multi-scale patch and multi-modality atlases for whole heart
     segmentation of MRI},
  Journal = {Medical Image Analysis},
  Year = {2016},
  Volume = {31},
  Pages = {77-87},
}

@article{Zhuang2019MvMM,
  Author = {Zhuang, Xiahai},
  Title = {Multivariate Mixture Model for Myocardial Segmentation Combining
     Multi-Source Images},
  Journal = {IEEE Transactions on Pattern Analysis and Machine Intelligence},
  Year = {2019},
  Volume = {41},
  Number = {12},
  Pages = {2933-2946},
}

@article{GAO2023BayeSeg,
  Author = {Gao, Shangqi and Zhou, Hangqi and Gao, Yibo and Zhuang, Xiahai},
  Title = {BayeSeg: Bayesian modeling for medical image segmentation with
     interpretable generalizability},
  Journal = {Medical Image Analysis},
  Year = {2023},
  Volume = {89},
  Pages = {102889},
}
```

<script defer src="{{ '/assets/js/leaderboard_sort.js' | relative_url }}"></script>


<!--## Contact
If you have any questions regarding the CARE-Whole Heart track, please feel free to contact:

- [care26challenge@163.com](mailto:care26challenge@163.com)
- [care26challenge@outlook.com](mailto:care26challenge@outlook.com)


Prof Xiahai Zhuang: [zxh@fudan.edu.cn](mailto:zxh@fudan.edu.cn)
Hangqi Zhou: [hqzhou21@m.fudan.edu.cn](mailto:hqzhou21@m.fudan.edu.cn)-->
