You are a cloud certification exam content expert and technical quiz author. You have deep knowledge of AWS and Azure certification exams, their domains, question styles, and the level of difficulty candidates should expect. Your task is to create a quiz content repository for the QuizPlay quiz-player app (live at https://quizplay.io). The repository will contain 36 original practice questions for a cloud certification exam.

## Reference Repository

Use this sample quiz repo as your structural reference:
https://github.com/quizplay-io/quiz-player-sample-quiz

Clone or browse it to understand the exact file structure, JSON schemas, naming conventions, and formatting before you begin. Your output must follow the same patterns.

## IMPORTANT: Plan First

Before writing any files, generate a detailed plan that includes:

1. Which exam modules/domains you will cover and how many questions each gets (ensure proportional representation of all official exam domains)
2. Which 4 case study scenarios you will create, what companies they describe, and which 3 questions each scenario will have
3. The question type assigned to each of the 36 questions
4. A mapping of question numbers to their topics, types, and whether they belong to a case study

Present the plan as a table and wait for my approval before proceeding.

## Target Exam

I am creating questions for:

- AWS Certified Solutions Architect – Associate (SAA-C03)

## Content Integrity Rules — READ CAREFULLY

- Every question MUST be original. Do NOT reproduce or closely paraphrase any question from actual certification exam dumps, brain dumps, practice test sites, or leaked exam content.
- Questions must test the same skills and knowledge domains as the real exam but must be written from scratch with unique scenarios, wording, and answer choices.
- All company names used in case studies and question scenarios must be FICTIONAL. Do NOT use:
  - Names from actual Microsoft official practice assessments: "Contoso", "Fabrikam", "Tailwind Traders", "Northwind Traders", "Adventure Works", "Wingtip Toys", "Litware", "Proseware", "Humongous Insurance", "Trey Research", "A. Datum", "VanArsdel", "Wide World Importers", "Fourth Coffee", "Adatum", "Relecloud", "Munson's Pickles", "Best For You Organics"
  - Names from actual AWS official practice assessments: "AnyCompany", "Example Corp"
  - Names already used in existing QuizPlay repos: "GaleWind", "NovaBright", "RidgePoint", "HarborView", "IronClad", "NovaBridge", "Wavelength", "AtlasForge", "QuantumLeap", "Velocity Streams", "Zenith", "CryptoVault", "Sentinel", "ShieldWall", "Vanguard", "Glacier Logistics", "IronBridge", "Skyline", "TerraBound", "Crestline", "Meridian", "Pinnacle", "Solaris"
- Instead, invent completely fresh company names. Some examples: "ClearVault", "ArcTide", "Heliosphere", "VoltEdge", "BrightForge", "NexaTier", "Pulsewave", "CoralShift", "TerraSync", "SkyLoom", "EmberStack", "FrostByte Analytics", "LunarGrid", "OceanForge", "CedarPoint Systems", "DriftNet", "AeroVault", "ChromaScale", "ThunderPeak", "MossGate"

## Repository Structure

Create the following file structure:

```
├── quiz.json                    # Manifest file
├── questions/                   # 36 question JSON files
│   ├── 01-<name>.json
│   ├── 02-<name>.json
│   └── ... through 36-<name>.json
├── scenarios/                   # 4 case study scenario files
│   ├── case_study_<name>.json
│   ├── case_study_<name>.json
│   ├── case_study_<name>.json
│   └── case_study_<name>.json
├── assets/
│   └── images/                  # SVG files for hotspot/hotspot-dropdown questions and preview
├── README.md
└── LICENSE                      # AGPL v3.0
```

## quiz.json Manifest Format

```json
{
    "title": "<Exam Code> Practice Section 1",
    "description": "<Full Exam Name> (<Exam Code>) - 36 Practice Questions (12 case study-linked + 24 standalone)",
    "slug": "<exam-code-lowercase>-practice-section-1",
    "category": "<EITHER 'AWS Certification' OR 'Azure Certification'>",
    "preview_image": "assets/images/preview_<exam_code>.svg",
    "questions": [
        "questions/01-<name>.json",
        "questions/02-<name>.json",
        ...
        "questions/36-<name>.json"
    ]
}
```

## Question Distribution

### Case Study vs Standalone: 12 case study + 24 standalone

- Create exactly 4 case study scenarios with 3 questions each = 12 case study questions
- The remaining 24 questions are standalone (no case study reference)
- **CRITICAL: All questions belonging to the same case study MUST be consecutive.** Group them together (e.g., questions 01-03 share scenario A, 04-06 share scenario B, etc.). Do NOT scatter case study questions throughout the quiz.

### Question Type Distribution (across all 36 questions)

Provide a good mix of all supported question types:

- **single** (single-choice, ~14 questions): One correct answer from 4 options. This is the DEFAULT type — do NOT include a `"type"` field for these.
- **multi** (multiple-choice, ~8 questions): Two or more correct answers. Add `"type": "multi"`. The question text must state how many to choose, e.g., "(Choose two.)"
- **ordering** (~5 questions): Arrange steps in correct sequence. Add `"type": "ordering"`.
- **matching** (~3 questions): Match source items to target slots. Add `"type": "matching"`.
- **fill-blank** (~3 questions): Complete statements by selecting correct terms. Add `"type": "fill-blank"`.
- **hotspot-dropdown** (~2 questions): Image with dropdown selectors. Add `"type": "hotspot-dropdown"`.
- **hotspot** (~1 question): Click on the correct zone in an image. Add `"type": "hotspot"`.

These counts are approximate — adjust slightly as needed, but ensure all 7 types are represented and the distribution is reasonable.

## JSON Schemas for Each Question Type

### single (DEFAULT — no type field needed)

```json
{
  "id": "<exam>-<topic-slug>",
  "question": "Question text with **markdown** support.",
  "options": [
    { "text": "Option A", "correct": false },
    { "text": "Option B", "correct": true },
    { "text": "Option C", "correct": false },
    { "text": "Option D", "correct": false }
  ],
  "explanation": "Detailed explanation with **markdown** support.\n\n**Why not the other options:**\n- ...",
  "category": "Exam Domain/Module Name"
}
```

### multi

```json
{
  "id": "<exam>-<topic-slug>",
  "type": "multi",
  "question": "Question text. (Choose two.)",
  "options": [
    { "text": "Option A", "correct": true },
    { "text": "Option B", "correct": false },
    { "text": "Option C", "correct": true },
    { "text": "Option D", "correct": false }
  ],
  "explanation": "Explanation...",
  "category": "Exam Domain/Module Name"
}
```

### ordering

```json
{
  "id": "<exam>-<topic-slug>",
  "type": "ordering",
  "question": "Arrange the following steps in the correct order.",
  "items": [
    "Step shown in shuffled order A",
    "Step shown in shuffled order B",
    "Step shown in shuffled order C",
    "Step shown in shuffled order D"
  ],
  "correctOrder": [
    "Actual first step",
    "Actual second step",
    "Actual third step",
    "Actual fourth step"
  ],
  "explanation": "Explanation of the correct order...",
  "category": "Exam Domain/Module Name"
}
```

Note: `items` is what the user sees (shuffled). `correctOrder` is the right sequence.

### matching

```json
{
  "id": "<exam>-<topic-slug>",
  "type": "matching",
  "question": "Match each item on the left to its correct target on the right.",
  "sourceItems": [
    "Description of item 1",
    "Description of item 2",
    "Description of item 3",
    "Description of item 4",
    "Description of item 5"
  ],
  "targetSlots": ["Target A", "Target B", "Target C", "Target D", "Target E"],
  "correctMapping": [0, 3, 1, 2, 4],
  "explanation": "Explanation of each mapping...",
  "category": "Exam Domain/Module Name"
}
```

Note: `correctMapping[i]` is the index in `targetSlots` that `sourceItems[i]` maps to.

### fill-blank

```json
{
  "id": "<exam>-<topic-slug>",
  "type": "fill-blank",
  "question": "Complete each statement by selecting the correct term.",
  "blanks": [
    {
      "id": "blank-1-slug",
      "label": "Statement with a ___ to fill.",
      "options": ["Option A", "Option B", "Option C"],
      "correctIndex": 0
    },
    {
      "id": "blank-2-slug",
      "label": "Another statement with a ___.",
      "options": ["Option X", "Option Y", "Option Z"],
      "correctIndex": 2
    }
  ],
  "explanation": "Explanation of each blank...",
  "category": "Exam Domain/Module Name"
}
```

### hotspot-dropdown

```json
{
  "id": "<exam>-<topic-slug>",
  "type": "hotspot-dropdown",
  "question": "Select the correct option for each scenario.",
  "image": "assets/images/<descriptive_name>.svg",
  "dropdowns": [
    {
      "label": "Scenario 1: Description of the scenario.",
      "position": { "x": 55, "y": 36 },
      "options": ["Choice A", "Choice B", "Choice C", "Choice D"],
      "correctIndex": 2
    },
    {
      "label": "Scenario 2: Description of another scenario.",
      "position": { "x": 55, "y": 58 },
      "options": ["Choice A", "Choice B", "Choice C"],
      "correctIndex": 0
    }
  ],
  "explanation": "Explanation...",
  "category": "Exam Domain/Module Name"
}
```

Note: You must also create the referenced SVG image file. The SVG should be a simple diagram or table layout that provides visual context for the dropdowns.

### hotspot

```json
{
  "id": "<exam>-<topic-slug>",
  "type": "hotspot",
  "question": "Click on the correct area in the diagram.",
  "image": "assets/images/<descriptive_name>.svg",
  "zones": [
    { "x1": 0, "y1": 17, "x2": 30, "y2": 22, "label": "Zone A" },
    { "x1": 30, "y1": 17, "x2": 49, "y2": 22, "label": "Zone B" },
    { "x1": 49, "y1": 17, "x2": 67, "y2": 22, "label": "Zone C" },
    { "x1": 67, "y1": 17, "x2": 90, "y2": 22, "label": "Zone D" }
  ],
  "correctZone": 2,
  "explanation": "Explanation of why Zone C is correct...",
  "category": "Exam Domain/Module Name"
}
```

Note: Coordinates are percentages (0-100) of the image dimensions. You must also create the referenced SVG image file.

## Case Study Scenario File Format

```json
{
  "id": "case_study_<company_name_lowercase>",
  "tabs": [
    {
      "title": "Company Overview",
      "content": "**CompanyName** is a ... (markdown formatted description of the company, its business, and its current IT environment)"
    },
    {
      "title": "Requirements",
      "content": "**Technical Requirements:**\n- Requirement 1\n- Requirement 2\n\n**Security Requirements:**\n- Requirement A\n- Requirement B"
    }
  ]
}
```

Each scenario should have 2-3 tabs providing rich context. The content should be detailed enough that 3 different questions can each focus on a different aspect of the scenario.

## Adding caseStudy Reference to Questions

For questions that belong to a case study, add a `"caseStudy"` field pointing to the scenario file:

```json
{
    "id": "...",
    "question": "Based on the requirements for CompanyName, which ...",
    "caseStudy": "scenarios/case_study_<name>.json",
    ...
}
```

## File Naming Conventions

- Question files: `NN-<descriptive-kebab-case-name>.json` (e.g., `01-voltedge-iam-roles.json`, `25-vpc-peering-design.json`)
- Case study questions: use the company name as prefix (e.g., `01-brightforge-networking.json`)
- Standalone questions: use the topic as the name (e.g., `25-vpc-peering-design.json`)
- Scenario files: `case_study_<company_name_lowercase>.json`
- Question IDs: `<exam-code-short>-<descriptive-slug>` (e.g., `saa-c03-s3-lifecycle`, `az305-vnet-peering`)

## Category Field

The `category` field on each question must match one of the official exam domains/modules. Look up the actual exam guide for the target certification and use its domain names. Every domain should be represented roughly in proportion to its weight on the actual exam.

## Quality Standards

- Explanations must be thorough (at least 3-5 sentences) — explain why the correct answer is right AND why each wrong answer is wrong. A good explanation teaches the concept, not just states the answer.
- Use markdown formatting in questions and explanations (bold for key terms, code blocks for CLI commands/JSON, bullet lists for multi-point explanations)
- Questions should test real architectural decision-making and practical knowledge, not trivia or rote memorization
- Ordering questions should have 4-6 steps
- Matching questions should have 4-5 items
- Fill-blank questions should have 2-4 blanks
- Each question should have 4 options (for single/multi types) unless the question type dictates otherwise
- Difficulty: aim for exam-level difficulty — not too easy, not unreasonably tricky

## SVG Image Files

For hotspot and hotspot-dropdown questions, create simple, clean SVG files that serve as the visual context. These can be:

- Architecture diagrams
- Table/matrix layouts
- Network topology diagrams
- Dashboard mockups

Keep SVGs simple and functional. Use a viewBox of "0 0 800 600" or similar, with readable text and clear visual zones.

### Preview Image

Create a visually appealing preview image SVG at `assets/images/preview_<exam_code>.svg` that is representative of the exam and its cloud platform. Look at the sample repo's `assets/images/event_loop_diagram.svg` for the style and quality level. The preview image should:

- Be a meaningful diagram or visual related to the exam's subject matter (e.g., a cloud architecture diagram for a Solutions Architect exam, a CI/CD pipeline diagram for a DevOps exam, a network topology for a networking exam)
- NOT be a simple text card — it should look like an actual technical illustration
- Use a viewBox of "0 0 800 600" with clean lines, readable labels, and professional colors that match the cloud provider's brand palette (Azure blue, AWS orange/navy, etc.)
- Work well as a thumbnail when displayed at smaller sizes on the quizplay.io storefront

Reference this image in `quiz.json` as the `"preview_image"` value.

## README.md

Create a README.md following the same structure as the sample repo. It must include:

1. **An "Open in Quiz Player" badge** at the top that links to the quiz on quizplay.io. Use this exact badge format (replace the source path with your repo's `<owner>/<repo-name>`):

```markdown
[![Open in Quiz Player](https://img.shields.io/badge/Open_in-Quiz_Player-blue?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAxMDAgMTAwIj48cmVjdCB3aWR0aD0iMTAwIiBoZWlnaHQ9IjEwMCIgcng9IjIwIiBmaWxsPSIjMDg5MWIyIi8+PHRleHQgeD0iNTAlIiB5PSI1MCUiIGRvbWluYW50LWJhc2VsaW5lPSJtaWRkbGUiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iNjAiIGZpbGw9IndoaXRlIiBmb250LWZhbWlseT0iQXJpYWwsc2Fucy1zZXJpZiIgZm9udC13ZWlnaHQ9ImJvbGQiPlE8L3RleHQ+PC9zdmc+)](https://quizplay.io/quiz.html?source=<owner>/<repo-name>)
```

2. **The preview image** embedded below the badge: `![Preview](assets/images/preview_<exam_code>.svg)`

3. **A short description** of the exam and what the questions cover

4. **A "Content Overview" section** listing the total question count, question types used, and a breakdown of topics/domains with question counts

5. **A "What This Does Not Cover" section** clarifying scope limitations

6. **A disclaimer** using a GitHub alert block:

```markdown
> [!IMPORTANT]
> These questions are **AI-generated** for study and practice purposes. They are **not** exam dumps and do not contain actual questions from the certification exam. Use them to test your understanding of concepts, not as a substitute for official study materials.
```

7. **A "Usage" section** that says: `This repository is designed to be used with the [Quiz Player](https://quizplay.io). Click the badge above to launch the quiz directly.`

8. **A "License" section** referencing AGPL v3.0

## Summary Checklist

Before finishing, verify:

- [ ] quiz.json lists exactly 36 question file paths
- [ ] 36 question JSON files exist in questions/
- [ ] 4 scenario JSON files exist in scenarios/
- [ ] 12 questions have a `caseStudy` field (3 per scenario)
- [ ] Case study questions are grouped consecutively
- [ ] 24 questions have no `caseStudy` field
- [ ] All 7 question types are represented
- [ ] All exam domains/modules are represented proportionally
- [ ] No real exam dump questions — all content is original
- [ ] No banned company names (Contoso, Fabrikam, Tailwind Traders, etc.)
- [ ] All IDs are unique
- [ ] All file references in quiz.json match actual filenames
- [ ] SVG files exist for hotspot and hotspot-dropdown questions
- [ ] Preview image SVG exists and is referenced in quiz.json
- [ ] Category values match official exam domain names
- [ ] README.md includes the "Open in Quiz Player" badge linking to quizplay.io
- [ ] README.md includes the AI-generated disclaimer
- [ ] LICENSE file exists (AGPL v3.0)

Now generate the plan and wait for my approval before creating the files.

---

## After All Files Are Created

Once all files are generated and the checklist passes, output the following instructions to the user so they can test and publish their quiz:

### Step 1: Test Locally First

Before publishing, test your quiz locally on quizplay.io to catch any issues:

1. Open https://quizplay.io
2. Use the **"Upload Quiz"** option on the storefront
3. Select your local quiz folder
4. Play through several questions — test at least one of each question type (single, multi, ordering, matching, fill-blank, hotspot, hotspot-dropdown)
5. Verify that case study scenarios load correctly and display their tabs
6. Check that the preview image renders properly
7. Fix any JSON formatting errors, broken file references, or rendering issues before publishing

### Step 2: Create a GitHub Repository

1. Go to https://github.com/new
2. Name the repo following the convention: `quiz-player-quizzes-<exam-code>-question-set-<N>` (e.g., `quiz-player-quizzes-saa-c03-question-set-1`)
3. Set it to **Public**
4. Do NOT initialize with a README (you already have one)
5. Create the repository

### Step 3: Push Your Content

```bash
cd your-quiz-folder
git init
git add .
git commit -m "feat: add 36 practice questions for <Exam Code>"
git branch -M main
git remote add origin https://github.com/<your-username>/<repo-name>.git
git push -u origin main
```

### Step 4: Set the Repository Description and Topic

1. Go to your repository page on GitHub
2. Click the gear icon next to "About" in the top-right of the repo
3. In the **Description** field, set a description that clearly states the content is AI-generated and not an exam dump. Follow this format:
   `<Exam Code> <Exam Name> — AI-generated practice questions (not exam dumps) for study and self-assessment`
   For example: `AZ-305 Azure Solutions Architect Expert — AI-generated practice questions (not exam dumps) for study and self-assessment`
4. In the **Topics** field, type `quizplay` and press Enter — this is **required** for your quiz to appear on quizplay.io
5. Click **Save changes**

### Step 5: Verify on QuizPlay

Your quiz will now be discoverable at https://quizplay.io. You can play it directly at:

```
https://quizplay.io/quiz.html?source=<your-username>/<repo-name>
```

For example:

```
https://quizplay.io/quiz.html?source=janedoe/quiz-player-quizzes-saa-c03-question-set-1
```