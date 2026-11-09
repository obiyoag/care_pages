---
layout: distill
title: CARE-Myocardium
description: Myocardial Pathology Segmentation
permalink: /track_myocardium/
bibliography: reference.bib
toc:
  - name: Registration
  - name: Motivation
  - name: Tasks
  - name: Data details
  - name: Metrics
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
<!--To access the dataset, please register [here](http://zmic.org.cn/care_2026/eval/register?track=myocardium).-->

## Motivation
{% include figure.liquid loading="eager" path="/assets/img/myocardium.png" class="img-fluid" max-width="70%" zoomable=true caption="Figure 1. Myocardial pathology segmentation and its challenges. (A) Myocardial Pathology Segmentation: Scar and edema regions are marked in green and yellow, respectively. (B) Cine MyoPS: Scar regions are marked in blue. (C) Challenges of Myocardial Pathology Segmentation: The challenges include multi-center data, missing sequences, and misalignments in multi-sequence CMR images." %}

Myocardial infarction (MI) is a leading cause of mortality and disability worldwide. Accurate assessment of myocardial viability is essential for the diagnosis and clinical management of MI patients<d-cite key="myops1"></d-cite>. Multi-sequence cardiac magnetic resonance (MS-CMR) imaging provides comprehensive insights into myocardial pathology, playing a pivotal role in tailored patient care. As shown in Figure 1 (A), balanced steady-state free precession (bSSFP) cine sequences clearly delineate anatomical boundaries, while late gadolinium enhancement (LGE) and T2-weighted (T2) CMR sequences visualize myocardial scars and edema, respectively.

Despite the high efficacy of LGE in visualizing myocardial scars, its acquisition can be time-consuming and sometimes clinically prohibitive due to the required administration of contrast agents, which highlights an urgent need for contrast-free alternatives. Cine CMR emerges as a rapid, contrast-free imaging technique capable of capturing myocardial dynamics. As shown in Figure 1 (B), non-viable myocardial regions (scars) exhibit distinct abnormalities in cardiac motion and wall thickness compared to viable tissue. Leveraging these functional differences, cine CMR presents a promising yet highly challenging alternative for direct myocardial pathology segmentation<d-cite key="myops4"></d-cite>.

## Tasks

The primary objective of this track is to accurately segment myocardial pathology regions (specifically, scars and edema) from CMR sequences. This track seeks innovative solutions to address two distinct subtasks: **MyoPS**, which focuses on segmenting scars and edema using MS-CMR data, and **CineMyoPS**, which focuses on segmenting scars using solely cine CMR data. We encourage participants to develop robust algorithms capable of overcoming significant real-world challenges, including multi-center data variations, missing sequences in certain centers<d-cite key="myops2"></d-cite>, and spatial misalignments across multi-sequence CMRs<d-cite key="myops3"></d-cite>, as illustrated in Figure 1 (C).

- MyoPS data: LGE, T2 and bSSFP sequences. The segmentation target is scars and edema at the LGE and T2 sequences, respectively. 
- CineMyoPS data: cine sequence. The segmentation target is scars at the end-diastolic frame of the cine sequence. 

The specific  substructures, each associated with a unique label value, are:
1. **Scar** - Label value: 2221
2. **Edema** - Label value: 1220
3. **Left ventricle** - Label value: 500
4. **Myocardium** - Label value: 200
5. **Right ventricle** - Label value: 600


We will rank participant methods based on the settings (​Lb1–Lb3) detailed in the following table:

<div style="display: flex;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
<caption style="caption-side: top; text-align: left; font-weight: bold; padding-bottom: 10px;"> Leaderboard (Lb) for Myocardium track across targets and evaluation settings.​​ Lb1–Lb3 represent performance from different subtasks and targets (e.g., Lb1 = Scar segmentation peformance on the MyoPS subtask). </caption>
  <thead>
    <tr>
      <th style="text-align:center;">Subtask</th>
      <th style="text-align:center;">Target</th>
      <th style="text-align:center;">Leaderboard</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>MyoPS</td>
      <td>Scar</td>
      <td>Lb1</td>
    </tr>
    <tr>
      <td>MyoPS</td>
      <td>Edema</td>
      <td>Lb2</td>
    </tr>
    <tr>
      <td>CineMyoPS</td>
      <td>Scar</td>
      <td>Lb3</td>
    </tr>
  </tbody>
</table>
</div>





## Data details

### Training data – MyoPS 

<div style="display: flex; ">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
  <thead>
    <tr>
      <th style="text-align:center;">Center</th>
      <th style="text-align:center;">Num. patients</th>
      <th style="text-align:center;">Sequences</th>
      <th style="text-align:center;">Manual labels</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>A</td>
      <td>81</td>
      <td>LGE</td>
      <td>Scar, left ventricle and  myocardium</td>
    </tr>
    <tr>
      <td>B</td>
      <td>35</td>
      <td>LGE, T2 and bSSFP</td>
      <td>Scar, edema, left ventricle,  myocardium and right ventricle</td>
    </tr>
    <tr>
      <td>C</td>
      <td>45</td>
      <td>LGE, T2 and bSSFP</td>
      <td>Scar, edema, left ventricle,  myocardium and right ventricle</td>
    </tr>
    <tr>
      <td>E</td>
      <td>7</td>
      <td>LGE and bSSFP</td>
      <td>Scar, left ventricle,  myocardium  and right ventricle</td>
    </tr>
    <tr>
      <td>F</td>
      <td>9</td>
      <td>LGE and bSSFP</td>
      <td>Scar, left ventricle,  myocardium and and right ventricle</td>
    </tr>
    <tr>
      <td>G</td>
      <td>8</td>
      <td>LGE and bSSFP</td>
      <td>Scar, left ventricle,  myocardium and and right ventricle</td>
    </tr>
        <tr>
      <td>H</td>
      <td>35</td>
      <td>LGE </td>
      <td>Scar</td>
    </tr>
  </tbody>
</table>
</div>

### Validation data – MyoPS 

<div style="display: flex;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
  <thead>
    <tr>
      <th style="text-align:center;">Center</th>
      <th style="text-align:center;">Num. patients</th>
      <th style="text-align:center;">Sequences</th>
      <th style="text-align:center;">Manual labels</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>(Anonymous)</td>
      <td>15</td>
      <td>LGE, T2 and bSSFP</td>
      <td>Scar, edema, left ventricle,  myocardium and right ventricle</td>
    </tr>

  </tbody>
</table>
</div>

### Test data – MyoPS 

<div style="display: flex;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
  <thead>
    <tr>
      <th style="text-align:center;">Center</th>
      <th style="text-align:center;">Num. patients</th>
      <th style="text-align:center;">Sequences</th>
      <th style="text-align:center;">Manual labels</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>(Anonymous)</td>
      <td>65</td>
      <td>LGE, T2 and bSSFP</td>
      <td>Scar, edema, left ventricle,  myocardium and right ventricle</td>
    </tr>
  </tbody>
</table>
</div>

### Training data – CineMyoPS 

<div style="display: flex; ">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
  <thead>
    <tr>
      <th style="text-align:center;">Center</th>
      <th style="text-align:center;">Num. patients</th>
      <th style="text-align:center;">Sequences</th>
      <th style="text-align:center;">Manual labels</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>α </td>
      <td>40</td>
      <td>Cine</td>
      <td>Scar, left ventricle and  myocardium </td>
    </tr>
        <tr>
      <td>β </td>
      <td>24</td>
      <td>Cine</td>
      <td>Scar, left ventricle and  myocardium </td>
    </tr>




  </tbody>
</table>
</div>

### Validation data – CineMyoPS 

<div style="display: flex;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
  <thead>
    <tr>
      <th style="text-align:center;">Center</th>
      <th style="text-align:center;">Num. patients</th>
      <th style="text-align:center;">Sequences</th>
      <th style="text-align:center;">Manual labels</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>(Anonymous)</td>
      <td>15</td>
      <td>Cine</td>
      <td>Scar, left ventricle and  myocardium</td>
    </tr>
  </tbody>
</table>
</div>

### Test data – CineMyoPS 

<div style="display: flex;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
  <thead>
    <tr>
      <th style="text-align:center;">Center</th>
      <th style="text-align:center;">Num. patients</th>
      <th style="text-align:center;">Sequences</th>
      <th style="text-align:center;">Manual labels</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>(Anonymous)</td>
      <td>45</td>
      <td>Cine</td>
      <td>Scar, left ventricle and myocardium</td>
    </tr>
  </tbody>
</table>
</div>

## Metrics 


The performance of scar and edema segmentation results will be evaluated by：
- **Dice Similarity Coefficient (Dice)**
- **Hausdorff Distance (HD in mm)**

## Rules
- **Only automatic methods are acceptable.** Participants must utilize algorithms that do not require manual intervention or human-assisted processes for the segmentation task.
- **Pre-trained models are  allowed in this track.** The solutions could be developed with pre-trained fundation models, such as SAM, CLIP, and MedSAM.

## Leaderboards

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

### Myocardial Pathology Segmentation
<!-- ============ 表 1：Myops ============ -->
<div style="overflow-x:auto;">
<table id="myops" class="sortable">
  <thead>
    <tr>
      <th>Team</th>
      <th>DSC<sub>Scar</sub>↑</th>
      <th>HD<sub>Scar</sub>(mm)↓</th>
      <th>DSC<sub>Edema</sub>↑</th>
      <th>HD<sub>Edema</sub>(mm)↓</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>MatU(SP+A)</td><td>0.6510</td><td>18.9150</td><td>0.6720</td><td>23.9050</td></tr>
    <tr><td>ZQH</td><td>0.6090</td><td>23.1910</td><td>0.6380</td><td>26.3090</td></tr>
    <tr><td>Sheffield_Heart</td><td>0.6160</td><td>22.4050</td><td>0.6530</td><td>27.7170</td></tr>
    <tr><td>OrganAgent</td><td>0.6040</td><td>24.5020</td><td>0.6420</td><td>25.0220</td></tr>
    <tr><td>Majin</td><td>0.6080</td><td>22.9860</td><td>0.6370</td><td>29.6650</td></tr>
    <tr><td>NECS</td><td>0.3430</td><td>68.9060</td><td>0.3700</td><td>68.0700</td></tr>
  </tbody>
</table>
</div>

<!-- ============ 表 2：cinemyops ============ -->
### Cine Myocardial Pathology Segmentation
<div style="overflow-x:auto;">
<table id="cinemyops" class="sortable">
  <thead>
    <tr>
      <th>Team</th>
      <th>DSC<sub>Scar</sub>↑</th>
      <th>HD<sub>Scar</sub>(mm)↓</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>ZQH</td><td>0.3808</td><td>33.5566</td></tr>
    <tr><td>NCC1H</td><td>0.3590</td><td>37.1990</td></tr>
    <tr><td>XiaohanYuan</td><td>0.4840</td><td>60.7090</td></tr>
    <tr><td>OrganAgent</td><td>0.3330</td><td>41.2850</td></tr>
    <tr><td>NECS</td><td>0.1146</td><td>146.2665</td></tr>
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

initSortable("myops");
initSortable("cinemyops");
</script>


## Citations
**Please cite these papers when you use the data for publications:**
```bib
 @article{zhuang2019multivariate,
    title={Multivariate mixture model for myocardial segmentation combining multi-source images},
    author={Zhuang, Xiahai},
    journal={IEEE transactions on pattern analysis and machine intelligence},
    volume={41},
    number={12},
    pages={2933--2946},
    year={2019},
}

@article{qiu2023myops,
  title={MyoPS-Net: Myocardial pathology segmentation with flexible combination of multi-sequence CMR images},
  author={Qiu, Junyi and Li, Lei and Wang, Sihan and Zhang, Ke and Chen, Yinyin and Yang, Shan and Zhuang, Xiahai},
  journal={Medical image analysis},
  volume={84},
  pages={102694},
  year={2023},
}

 @article{ding2023aligning,
  title={Aligning multi-sequence CMR towards fully automated myocardial pathology segmentation},
  author={Ding, Wangbin and Li, Lei and Qiu, Junyi and Wang, Sihan and Huang, Liqin and Chen, Yinyin and Yang, Shan and Zhuang, Xiahai},
  journal={IEEE Transactions on Medical Imaging},
  year={2023},
}

@article{ding2025cinemyops,
  title={CineMyoPS: Segmenting Myocardial Pathologies from Cine Cardiac MR},
  author={Ding, Wangbin and Li, Lei and Qiu, Junyi and Lin, Bogen and Yang, Mingjing and Huang, Liqin and Wu, Lianming and Wang, Sihan and Zhuang, Xiahai},
  journal={IEEE Transactions on Medical Imaging},
  year={2025},
}
```


<script defer src="{{ '/assets/js/leaderboard_sort.js' | relative_url }}"></script>
