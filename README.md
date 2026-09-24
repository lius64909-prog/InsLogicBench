# InsLogicBench

InsLogicBench is a benchmark for evaluating logical reasoning in complex insurance claims adjudication. The dataset contains insurance policy documents and claim adjudication QA instances with relevant clauses, structured explanations, and final decisions.

## Dataset Download

The dataset is available on Google Drive:

[**Download InsLogicBench**](https://drive.google.com/drive/folders/1tTW5fb_Mywvz2eQiCNw_4mfPhxH4toht?usp=sharing)

The dataset contains two files:

- `Policy.jsonl`: Insurance policy documents.
- `Q&A.json`: Claim adjudication QA instances and annotations.

## Data Format

### Policy.jsonl

Each line represents one insurance policy.

| Field | Type | Description |
|---|---|---|
| `id` | String | Unique identifier of the insurance policy. |
| `policy` | String | Full text of the insurance policy. |

### Q&A.json

Each item represents one claim adjudication instance.

| Field | Type | Description |
|---|---|---|
| `question_id` | String | Unique identifier of the QA instance. |
| `policy_id` | String | ID of the corresponding policy in `Policy-simple.jsonl`. |
| `question` | String | Natural-language claim description and inquiry. |
| `relevent_clause` | List[String] | Policy clauses relevant to the claim decision. |
| `explain` | Object | Structured explanation containing proposition-, clause-, and global-level reasoning. |
| `conclusion` | String | Final claim decision: `赔付` (Approved) or `不赔付` (Denied). |
| `logic_truth` | Object | Logical states of the coverage claim, rebuttal, and final decision. |
| `scenario` | String | Logical scenario category (`1`–`4`). |
| `exception` | Boolean | Whether the instance involves an exception to an exclusion clause. |
| `proposition_len` | Integer | Number of proposition-level explanations. |

### `explain`

| Field | Type | Description |
|---|---|---|
| `proposition` | List[String] | Explanations of whether individual factual conditions are satisfied. |
| `clause` | List[String] | Clause-level judgments based on the proposition results. |
| `global` | String | Overall reasoning leading to the final decision. |

### `logic_truth`

| Field | Type | Description |
|---|---|---|
| `claim_answer` | Boolean | Whether the coverage conditions are satisfied. |
| `rebuttal_answer` | Boolean | Whether an effective exclusion is triggered. |
| `final_answer` | Boolean | Final adjudication state (`true`: Approved, `false`: Denied). |

### Scenario Definition

| Scenario | Coverage | Exclusion | Decision |
|---|---|---|---|
| `1` | `true` | `false` | Approved |
| `2` | `false` | `false` | Denied |
| `3` | `true` | `true` | Denied |
| `4` | `false` | `true` | Denied |

> **Note:** `relevent_clause` is the original field name used in the released dataset and is kept unchanged for compatibility.
