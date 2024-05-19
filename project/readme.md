# PST: Task
- Identify reference sources (ref-sources) from full texts of a given paper
- “Ref-source”: Most important reference (source paper) that greatly inspires the paper
- Each paper can have one or more ref-sources, or none
- Rate importance of each reference within [0, 1]
- Source paper definition:
- Is the main idea inspired by the reference?
- Is the core method derived from the reference?
- Is the reference essential for the paper?
- **Input: XML format file of the paper generated using Grobid API**
- **Output: Importance score of each reference in the paper**

## Data:
- training set is list of papers with ref_source already determined
- validation set is list of papers with ref_source undetermined
### Data format
Training and validation sets are lists of dictionaries, each corresponding to a paper
- "_id": unique ID value of the paper
- "title": paper title
- "refs_trace": list of source papers
- "authors.name": author name of the paper
- "authors.org": organization of the author
- "venue": published journal or conference
- "year": year of publication
- "referenced_serial_number": serial number of the important reference in the reference list of the paper
- "references": all references in the paper

## Submission example: submission_example_valid.json
- Full text of papers: Located in the paper-xml folder
- Each paper’s XML file is named {paper ID}.xml
- Additional data: paper_source_gen_by_rule.json (4,854 papers)
    - Key: paper ID
        - Value: dictionary of its source papers
    - Key: serial number of the reference in the paper reference list
        - Value: corresponding paper's title
    - Collected using a rule-based approach (not annotated by experts, correctness not guaranteed)

## Task
Your task: predict an importance score for each reference in the papers in the validation set

paper_source_trace_train_ans.json
```paper_source_trace_train_ans.json
[
    {
        "_id": "5db80dc83a55acd5c14a24b9",
        "title": "CONNA: Addressing Name Disambiguation on The Fly",
        "refs_trace": [
            {
                "_id": "599c7968601a182cd263a485",
                "title": "End-to-End Neural Ad-hoc Ranking with Kernel Pooling",
                "authors": [
                    {
                        "name": "Chenyan Xiong",
                        "org": "Carnegie Mellon University, Pittsburgh, PA, USA"
                    },
                    {
                        "name": "Zhuyun Dai",
                        "org": "Carnegie Mellon University, Pittsburgh, PA, USA"
                    },
                    {
                        "name": "Jamie Callan",
                        "org": "Carnegie Mellon University, Pittsburgh, PA, USA"
                    },
                    {
                        "name": "Zhiyuan Liu",
                        "org": "Tsinghua University, Beijing, China"
                    },
                    {
                        "name": "Russell Power",
                        "org": "Allen Institute for AI, Seattle, WA, USA"
                    }
                ],
                "venue": "IR",
                "year": 2017,
                "referenced_serial_number": 52
            }
        ],
        "references": [
            "5bdc316717c44a1f58a06f07",
            "58d82fcbd649053542fd67e0",
            "53e9a525b7602d9702e4a2f9",
            "58437722ac44360f1082f5bd",
            "5a9cb60d17c44a376ffb3c4c",
            "5bdc31b417c44a1f58a0b8c2",
            "53e9ae89b7602d97038a8a5b",
            "53e9b457b7602d9703f54cf4",
            "53e9bafbb7602d970473014e",
            "53e9b9dab7602d97045d5eb7",
            "53e9affab7602d9703a4f291",
            "53e9a7feb7602d9703140daa",
            "5b8c9f4a17c44af36f8b72cf",
            "573697556e3b12023e63e8e4",
            "5d270c39275ded87f9541e2b",
            "5736973c6e3b12023e62b744",
            "53e9bbcfb7602d970481a6ec",
            "573696016e3b12023e514a63",
            "573697556e3b12023e63e9e3",
            "53e9acc4b7602d97036a1037",
            "573698636e3b12023e729d7c",
            "5dea04309e795e693620e97c",
            "53e9baecb7602d970471fc05",
            "558b4cb5612c41e6b9d48858"
        ],
        "authors": [
            {
                "name": "Chen Bo",
                "org": "Zhipu.AI, Co., Ltd, Beijing, China"
            },
            {
                "name": "Zhang Jing",
                "org": "Zhipu.AI, Co., Ltd, Beijing, China"
            },
            {
                "name": "Tang Jie",
                "org": "Information School, Renmin University of China, Beijing, China"
            },
            {
                "name": "Cai Lingfan",
                "org": "Zhipu.AI, Co., Ltd, Beijing, China"
            },
            {
                "name": "Wang Zhaoyu",
                "org": "Tsinghua-Bosch Joint ML Center, Department of Computer Science and Technology, Tsinghua University, Beijing, China"
            },
            {
                "name": "Zhao Shu",
                "org": "Tsinghua-Bosch Joint ML Center, Department of Computer Science and Technology, Tsinghua University, Beijing, China"
            },
            {
                "name": "Chen Hong",
                "org": "Zhipu.AI, Co., Ltd, Beijing, China"
            },
            {
                "name": "Li Cuiping",
                "org": "Zhipu.AI, Co., Ltd, Beijing, China"
            }
        ],
        "venue": "IEEE Transactions on Knowledge and Data Engineering",
        "year": 2022
    },
    {
        "_id": "5eede0b091e0116a23aafbd3",
        "title": "GCC: Graph Contrastive Coding for Graph Neural Network Pre-Training",
        "refs_trace": [
            {
                "_id": "5dcd263a3a55ac58039516c5",
                "title": "Momentum Contrast for Unsupervised Visual Representation Learning",
                "authors": [
                    {
                        "name": "He Kaiming",
                        "org": "Facebook"
                    },
                    {
                        "name": "Fan Haoqi",
                        "org": "Facebook"
                    },
                    {
```
paper_source_trace_train_wo_ans.json
```paper_source_trace_train_wo_ans.json
[
    {
        "_id": "61dbf1dcd18a2b6e00d9f311",
        "title": "Automated Unsupervised Graph Representation Learning",
        "references": [
            "58437722ac44360f1082efeb",
            "5b67b45517c44aac1c860876",
            "5e8d8e6d9fced0a24b5d669e",
            "53e9b253b7602d9703cf4028",
            "5736977f6e3b12023e66632b",
            "57aa28de0a3ac518da9896d5",
            "5a260c8117c44a4ba8a30f54",
            "62376b725aee126c0f0a7412",
            "5bdc31b417c44a1f58a0b4e9",
            "5b8c9f4a17c44af36f8b6a96",
            "5d9edc8347c8f76646042a37",
            "5d4d46fb3a55acff992fde2b",
            "603e2f2191e01129ef28fecc",
            "5bdc319c17c44a1f58a0a1b7",
            "558ba88be4b00c3c48ddc0f3",
            "53e9b254b7602d9703cf70bb",
            "6001711bd4150a363c49b450",
            "5d3ed25a275ded87f97deba4",
            "5d3ed25a275ded87f97deb56",
            "5db929b747c8f766461fa94f",
            "53e9b527b7602d970405d9f8",
            "53e9b3fdb7602d9703ef0efb",
            "5e5e18b393d709897ce28ad3",
            "5e5e189a93d709897ce1e760",
            "53e9b3f5b7602d9703ee3407",
            "5cf48a40da56291d582a2f8e",
            "5e9661119fced0a24bb3f157",
            "53e9bd82b7602d9704a283df",
            "605058cc9e795e84274fd10f",
            "53e9b2ffb7602d9703dc29f7",
            "53e9a5afb7602d9702edacce",
            "53e9b6b4b7602d97042394bc",
            "53e9acc4b7602d97036a1037",
            "53e9b108b7602d9703b85b88",
            "58d82fcbd649053542fd67e0",
            "573695fd6e3b12023e511373",
            "57a4e91aac44365e35c97c6e",
            "5cfa5b985ced2477cb3c5175",
            "5b67b47917c44aac1c8637c6",
            "5ce2d032ced107d4c635260c",
            "5da2f8aa3a55ac3402d8c165",
            "5f993af691e011a3fbe2fb01",
            "60bdde338585e32c38af4f97",
            "5f6b5b0f91e011bf6740cc4a",
            "53e9b873b7602d9704442198",
            "5cede10eda562983788eea63",
            "58d82fc8d649053542fd59b8"
        ],
        "authors": [
            {
                "name": "Zhenyu Hou",
                "org": "Tsinghua University"
            },
            {
                "name": "Yukuo Cen",
                "org": "Tsinghua University"
            },
            {
                "name": "Jie Tang"
            }
        ],
        "year": 2021
    },
    {
        "_id": "61dbf06b6750f87b50ecd224",
        "title": "CogKR: Cognitive Graph for Multi-hop Knowledge Reasoning",
        "references": [
            "53e9ab78b7602d970351a734",
            "53e9b991b7602d970457fe44",
            "5bdc315017c44a1f58a05c3c",
            "5a73cbc317c44a0b3035ec7e",
            "5d9edc0047c8f7664602f362",
            "5c04967517c44a2c74708b3b",
            "5d9edb8047c8f7664601c6a5",
            "5c8bc2804895d9cbc6a927cc",
            "5aed14d117c44a443815899c",
            "555048d045ce0a409eb71a69",
            "59ae3be32bbe271c4c71b8ba",
            "5cede105da562983788e48c5",
            "53e9b798b7602d9704342398",
            "5c2348ceda562935fc1d57e2",
            "5bbacb9e17c44aecc4eaff6b",
            "53e997fcb7602d9702005ad4",
            "53e9981db7602d970203e595",
```
submission_example_valid.json
```submission_example_valid.json
{
    "61dbf1dcd18a2b6e00d9f311": [
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0
    ],
    "61dbf06b6750f87b50ecd224": [
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
```

PST: Dataset
- The full text is given in the Electronic Text Encoding and Interchange (TEI) XML format
- The <text> section, especially the <body>, which contains the main content of the paper. This is where the model will look for references to the paper’s sources.
- The <ref> tags within the <body>, which indicate references to bibliography entries. These tags can help identify the location of source references in the text.
- The <listBibl> section in the <back>, which contains the bibliography entries.
- Each <biblStruct> represents a referenced work and provides details that can be used to match with the source papers.


