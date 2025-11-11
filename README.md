# Trait Judgements of Faces - Online Experiment

By **Yue Xu** · <yxu7@caltech.edu>

_Last verified: **Nov 10, 2025**_

---

## Overview

This repository hosts HTML-based code built with JsPsych for the online experiment described in the manuscript "Trait judgments of faces using a task without word labels" ([OSF preprint](https://osf.io/preprints/psyarxiv/ne6w2_v2)). 

The repository demonstrates:
* Consent form collection
* Participants' physical screensize measurement
* Instruction reading and comprehension quizzes with response-based feedback
* Participant prescreening and eligibility gating
* Several end-task questionnaires in multiple formats
* Gatekeeping is implemented at each step: participants must meet specific criteria to proceed to the next stage.

> **Note:** 
> - The **Cambridge Face Memory Test (CFMT)** and **Multi-Arrangement (MA) task** are not included here due to external hosting.  
> - See *Experimental_Paradigm.pdf* for a detailed walkthrough, screenshots, and demo links.  
> - Data analysis scripts and datasets are available on the [OSF project files](https://osf.io/nm7y8/files) and the [Github repo](https://github.com/hyue723/Trait_judgments_task_without_word).

---

## Experiment Flow

Each section of the experiment consists of HTML files hosted on a web server. URL parameters are passed between sections to maintain participant identifiers and task performance data.

### Stage 1 - Prescreening and Qualification:
1. **Part 1: Consent Form and Screen Calibration**  
   **File:** `Stage1_Part1_intro-and-calibration.html`  
   - Demo Link: [https://www.yxu.caltech.edu/experiment_demo/MA_experiment_demo/Stage1_Part1_intro-and-calibration.html](https://www.yxu.caltech.edu/experiment_demo/MA_experiment_demo/Stage1_Part1_intro-and-calibration.html)
   - Obtain consent and ensure that participants use an adequate screen size (≥7-inch diagonal) and laptops/destops instead of cellphones/tablets.  
   - Parameters read (these are passed forward to subsequent tasks):
        ```
        ?participantId=XXXX1&assignmentId=XXXX2&projectId=XXXX3
        ```
   
2. **Part 2: Cambridge Face Memory Test (CFMT)**  
   **Not included in this repository.**  
   - Hosted on [Testable.org](https://www.testable.org/library). This link provides a short demo and allows researchers to request access to this portion of the task. 
   - We modified the original CFMT into a shortened version as described in the manuscript. On Testable.org, the task was further adapted to :
        - Update a variable to accumulate the total number of correctly answered questions after each trial, and
        - Automatically pass the result (as a URL parameter) to the next section of the experiment. 
            ```
            &CFMT=XX
            ```
    - If you are interested in implementing a similar customization, please follow the [testable manual](https://help.testable.org/kb/en/feature-manual-57706) and feel free to contact the authors for details.

3. **Part 3: Instruction Reading and Quiz**  
   **File:** `Stage1_Part3_instruction-and-quiz.html`  
   - Demo Link: [https://www.yxu.caltech.edu/experiment_demo/MA_experiment_demo/Stage1_Part3_instruction-and-quiz.html](https://www.yxu.caltech.edu/experiment_demo/MA_experiment_demo/Stage1_Part3_instruction-and-quiz.html)
   - Participants read detailed instructions and complete a 7-question comprehension quiz.  
   - If the following criteria are not met, participants are redirected to an end screen:
        - CFMT score must be **≥33/48**, and  
        - Quiz score must be **≥6/7**.

---

### Stage 2 – Main Task and End Questionnaire

1. **Part 1: Multi-Arrangement Task (MA Task)**  
   **Not included in this repository.**  
   - Hosted on [meadows-research.com](https://meadows-research.com/)  
   - A toy demo available at: [https://meadows-research.com/demos/multiarrange/](https://meadows-research.com/demos/multiarrange/)  

2. **Part 2: End-Task Questionnaire (modified version for Experiment 2)**  
   **File:** `end_task_questionnaire.html`  
   - Demo Link: [https://www.yxu.caltech.edu/experiment_demo/MA_experiment_demo/end_task_questionnaire.html](https://www.yxu.caltech.edu/experiment_demo/MA_experiment_demo/end_task_questionnaire.html)  
   - An additional URL parameter is passed from the previous section:
     ```
     &mead_name=XXXXXX
     ```
     which stores the participant’s assigned Meadows ID.

---

## Technical Setup

### URL Parameters

Ensure that URL parameters are correctly passed to maintain continuity between parts of the experiment and record participant data accurately.

Typical parameters:
| Parameter | Description |
|------------|--------------|
| `participantId` | Participant unique ID |
| `assignmentId` | MTurk assignment ID |
| `projectId` | Internal project or study ID |
| `CFMT` | CFMT score (used for gating only after the CFMT section) |
| `mead_name` | Meadows system participant ID (added in Stage 2) |

If any are missing, they default to `"XXXXXXXnotValid"`.

---

### Data Saving and Permissions

#### File Permissions
- Make sure to update the file permissions each time after adding or updating files:
    ```bash
    chmod -R 755 *       # all files
    chmod 733 data/      # write-only, not listable
    ```

#### Data Saving Mechanism

- Data are saved asynchronously to the `/data/` folder via POST requests, at the end of each section.  
- **Known issue:** rare save failures.  
  This is yet to be implemented: a robust implementation should include a retry loop that waits briefly before resubmitting until a `"success"` response is received.

---

### Hosting and Deployment

- The server must support dydnamic requests (not a static-only host).

---

## How to Cite
If you use this experiment framework or adapt its code, please cite the associated manuscript(s) from this project ([osf preprint](https://osf.io/preprints/psyarxiv/ne6w2_v2)).

---

## Contact
Yue Xu: **yxu7@caltech.edu**


